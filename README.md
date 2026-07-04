# Financial Tracker Firebase Auto-Connect

This package contains a Firebase auto-connected version of Financial Tracker.

## What is preconfigured

The app is already configured for Firebase project:

- Project ID: `fintracker-8bb82`
- Default Data Key: `gwf-phase3-financial-tracker`

Users do not need to paste the Firebase configuration into the app.

## Firestore setup

1. Open Firebase Console.
2. Select project `fintracker-8bb82`.
3. Go to **Build → Firestore Database**.
4. Create a Firestore database if one does not already exist.
5. Go to **Rules** and publish a rule matching this package's `firestore.rules` for testing.

For production, do not leave the rules open. Use Firebase Authentication and role-based rules.

## Where data is stored

The app stores shared tracker data here:

```text
financialTrackerProjects/{Data Key}/state/current
```

The default Data Key is:

```text
gwf-phase3-financial-tracker
```

Change the Data Key only if you want a separate tracker workspace.

## Deploy with Firebase Hosting

Install Firebase CLI:

```bash
npm install -g firebase-tools
```

Login:

```bash
firebase login
```

Initialise hosting in this folder:

```bash
firebase init hosting
```

Choose this folder as the public directory, or place `index.html` in the generated public folder.

Deploy:

```bash
firebase deploy
```

## Deploy with GitHub Pages

1. Create a GitHub repository.
2. Upload `index.html` to the root of the repository.
3. Go to **Settings → Pages**.
4. Publish from the main branch root folder.
5. Open the GitHub Pages URL.

## Important

This auto-connect version is still a static HTML app with a single Firestore state document. It is suitable for pilot/shared PM use. For enterprise use, create separate Firestore collections for forecast lines, actual lines, invoices, audit log, users and permissions.
