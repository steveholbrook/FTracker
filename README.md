# Financial Tracker v3.0 Multi-Project

Static HTML deployment package.

## What changed
- Login screen with project selection.
- Admin / Viewer mode.
- Admin password defaults to `admin`.
- Admin can add projects from the login screen.
- Each project stores its own data in the shared cloud database path: `financialTrackerProjects/{projectKey}/state/current`.
- Viewer mode is read-only.

## Firestore rules for quick testing

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

For production, add Firebase Authentication and role-based rules. The default `admin` password is only a prototype control.
