# toDOmorrow.

A calm, dependency-free workspace for tasks, notes, and Pomodoro sessions. The complete application is in `index.html`; double-click it to start. For consistent browser storage behavior, use an HTTP origin such as the deployed site or an optional local static server:

```sh
python3 -m http.server 8080 --bind 127.0.0.1
```

Open `http://127.0.0.1:8080`. Python is an optional development convenience, not an application dependency. No install, build command, API key, or backend is required.

## Features

- Tasks: add, edit in place, delete with confirmation, complete, filter, search, set priority, and reorder. **Drag and drop the ⠿ handle beside a task to reorder it.** Optional accessible controls: click the handle to reveal **Move up / Move down** buttons, or focus it with Tab and press the keyboard’s **Arrow Up / Arrow Down** keys. The move buttons are hidden until you click the handle. Order persists across refreshes and JSON backups. With search or filters active, only visible tasks move; hidden tasks keep their slots.
- Notes: standalone scratchpads with explicit saving, title/body search, bold/italic/headings/lists, and a safe formatted preview. Raw HTML is displayed as text.
- Focus: task-linked Pomodoro timer with configurable focus/break durations under **Durations**, pause/resume/reset, and persistent deadlines. Choose Short break when a focus session finishes.
- Backup: JSON export and schema-validated replacement import with confirmation.
- Light/dark themes, responsive navigation, labeled controls, visible keyboard focus, and reduced-motion support.

Saved tasks, notes, settings, and timer state live in LocalStorage on this browser and origin. They do not synchronize across devices. Changing the hostname, browser, or HTTP/HTTPS origin gives a separate workspace. Clearing browser data removes it; export regular backups. File-URL storage behavior varies by browser. Notes have an explicit **Save note** button; unsaved drafts are not exported and can be lost on a crash. Multiple tabs use last-writer-wins snapshots, not conflict-free collaboration. The timer uses the system clock and finishes visibly when the app is running again; it has no OS notification or background alarm service.

Limits: 2,000 tasks, 2,000 notes; task titles 200 characters, note titles 120, note bodies 20,000; backups up to 4 MiB. Browser quotas can be lower. Invalid saved data is preserved and normal writes are blocked; use Export for raw recovery and import a repaired, valid backup. Backups contain unencrypted personal data. This app makes no external requests.

## Verification

Click **Run self-tests** under **Diagnostics**, or use the browser console:

```js
const report = await Tomorrow.runTests();
console.table(report.results);
```

The 18 isolated cases exercise CRUD, reload persistence, validation and size limits, quota/read failures, corruption recovery, safe rendering, timer calculations, export/import schema, mock API responses, and cross-tab snapshot refresh. They never modify your actual saved workspace. `AGENTS.md` contains the full architecture contract and manual acceptance checklist.

## Netlify Drop deployment

1. Put `index.html` at the root of a folder, such as `todomorrow`. The current project folder is ready; `AGENTS.md` and this README are optional public documentation. Exclude personal JSON backups or secrets. For an app-only upload, copy just `index.html` into a clean folder.
2. Visit [Netlify Drop](https://app.netlify.com/drop). Sign in if you want the deployment associated with your account.
3. Drag that folder into the drop zone. This is a finished static application: no dependency installation or build command is needed.
4. Wait for deployment to finish and open the generated `https://…netlify.app` URL. Claim/manage the project if Netlify prompts you. Copy the actual public URL for your HNG submission.
5. To update the same site, open its project in Netlify and use the manual deploy drop zone on its Deploys page with the updated folder. A new unrelated Drop upload may create a separate project and URL.

These steps follow [Netlify's Drop quickstart](https://docs.netlify.com/start/quickstarts/netlify-drop-quickstart/) and [manual deployment documentation](https://docs.netlify.com/deploy/create-deploys/).

### Quick live checks before submission

- Open the HTTPS URL in a fresh/private window and on your phone; verify Tasks, Notes, Focus, and theme switching.
- Add and edit a task, set its priority, complete it, filter/search, and confirm deletion on disposable test data.
- Save a formatted note, preview it, search it, then refresh and confirm it remains.
- Link a task to the timer, start/pause/resume it, refresh, and confirm the deadline continues.
- Export your synthetic data and import that backup; check counts and content. Confirm invalid JSON is rejected without changes.
- Run self-tests and require **18/18 passed**. Check the browser console for uncaught errors and verify there are no third-party runtime requests.
- Open the URL from another browser to confirm public access. Expect its LocalStorage workspace to be empty; that is normal.

No live deployment is performed by generating these files. The public submission URL is created when you complete Netlify Drop.

## Verification performed

The current app passed **18/18** embedded tests in the Codex in-app browser on 2026-09-29. JavaScript syntax validation passed. Browser checks covered task creation/editing/completion, filtering/search, pointer drag-to-reorder, keyboard and click-to-move alternatives, order persistence after refresh, notes saving/formatting, and timer start/pause/refresh. Desktop, 390 px, and 320 px layouts and dark mode were checked; no captured console errors or horizontal overflow appeared.

Live Netlify deployment, physical touchscreen gestures, full screen-reader/contrast auditing, cross-browser coverage, and file-picker download/import round trips remain manual release checks. Import/export schema round trips and reordering persistence are covered by the embedded tests.
