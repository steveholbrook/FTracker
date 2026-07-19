# Financial Tracker v3.1 Multi-Project

This version updates the v3.0 multi-project app for the FTracker repository.

## Changes in v3.1

- Removed the visible Shared Cloud Database panel from the Dashboard.
- The selected project is now the cloud workspace key automatically.
- When the user selects GWF, Blackmores, or an added project, the app loads/saves that project's cloud state automatically.
- Invoice Print Draft Preview now uses the logged-in project context and role and no longer injects or displays the login screen in the print/PDF window.
- Customer report print output was also cleaned so it does not include login-screen markup.

## Firestore path

Each project saves to:

```text
financialTrackerProjects/{projectKey}/state/current
```

Examples:

```text
financialTrackerProjects/gwf/state/current
financialTrackerProjects/blackmores/state/current
```

## Firestore test rules

For testing only:

```js
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /financialTrackerProjects/{projectKey}/state/{documentId} {
      allow read, write: if true;
    }
  }
}
```

Replace with authenticated rules before production/customer use.

## GitHub Pages deployment

Put `index.html` at the root of the FTracker repository, then set GitHub Pages to deploy from `main` branch `/root`.
