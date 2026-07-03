# Financial Tracker v2.10 Firebase Index

This package contains a single-file HTML version of **Financial Tracker v2.10 Blank** updated to save and load shared tracker data from **Firebase Cloud Firestore**.

The app still runs as a static `index.html`, so it can be deployed to GitHub Pages, Firebase Hosting, SharePoint static hosting, or any basic web host. Firebase is used as the central database.

## Files

| File | Purpose |
|---|---|
| `index.html` | The Financial Tracker app with Firebase cloud database support. |
| `gwf_forecast_upload_template_blank.xlsx` | Blank forecast upload template used by the app. |
| `firestore.rules` | Starter Firestore security rules requiring Firebase Authentication. |

## What changed from the local version

The original app saved to browser `localStorage`. This version still keeps a local browser backup, but the main save/load process can now use Firestore.

The app stores the full tracker state in:

```text
financialTrackerProjects/{DATA_KEY}/state/current
```

Where `{DATA_KEY}` is the value entered in the app, for example:

```text
gwf-phase3-financial-tracker
```

All users who open the deployed app and use the same Firebase project and same Data Key will see the same shared tracker state.

## Important limitation

This is a practical static-HTML Firebase version, not the final enterprise architecture. It stores the whole tracker state in one Firestore document. That is suitable for small to medium tracker use, but Firestore documents have size limits. For a large multi-project enterprise rollout, convert the app to a normalized Firestore model with separate collections for forecast lines, actual lines, invoices, audit logs and upload history.

## Beginner Firebase setup

### Step 1 — Create a Firebase project

1. Go to the Firebase Console.
2. Click **Add project**.
3. Enter a project name, for example `financial-tracker`.
4. Complete the setup wizard.

### Step 2 — Create a Firestore database

1. In Firebase Console, open your project.
2. Go to **Build → Firestore Database**.
3. Click **Create database**.
4. Choose a location.
5. For first testing, you can start in test mode, but do not leave customer data in test mode.

### Step 3 — Enable Authentication

1. Go to **Build → Authentication**.
2. Click **Get started**.
3. Open the **Sign-in method** tab.
4. Enable **Anonymous** sign-in.

The app attempts anonymous sign-in so the starter Firestore rules can require `request.auth != null`.

### Step 4 — Add a Web App and copy config

1. In Firebase Console, click the gear icon next to Project Overview.
2. Choose **Project settings**.
3. Under **Your apps**, click the web icon `</>`.
4. Register the app, for example `financial-tracker-web`.
5. Copy the Firebase config object.

It will look like this:

```js
const firebaseConfig = {
  apiKey: "...",
  authDomain: "your-project.firebaseapp.com",
  projectId: "your-project",
  storageBucket: "your-project.appspot.com",
  messagingSenderId: "...",
  appId: "..."
};
```

In the Financial Tracker app, paste only the JSON object into the **Firebase Web Config JSON** box, for example:

```json
{
  "apiKey": "...",
  "authDomain": "your-project.firebaseapp.com",
  "projectId": "your-project",
  "storageBucket": "your-project.appspot.com",
  "messagingSenderId": "...",
  "appId": "..."
}
```

### Step 5 — Deploy starter Firestore rules

Use the Firebase Console Rules tab or Firebase CLI to apply `firestore.rules`.

Starter rule included in this package:

```text
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /financialTrackerProjects/{projectKey}/state/{docId} {
      allow read, write: if request.auth != null;
    }
  }
}
```

This is still broad. For production, add user roles, project membership checks and separate customer-safe views.

## Deploy to GitHub Pages

### Step 1 — Create a GitHub repository

1. Create a new GitHub repository, for example `financial-tracker`.
2. Upload these files to the repository root:
   - `index.html`
   - `gwf_forecast_upload_template_blank.xlsx`
   - `README.md`

### Step 2 — Enable GitHub Pages

1. Open the repository in GitHub.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, select **Deploy from a branch**.
4. Select branch `main` and folder `/root`.
5. Click **Save**.
6. Wait for GitHub Pages to publish the site.

The app will be available at a URL similar to:

```text
https://YOUR-GITHUB-USER.github.io/financial-tracker/
```

### Step 3 — Connect the app to Firebase

1. Open the published app URL.
2. Go to the Dashboard.
3. Paste your Firebase config JSON.
4. Enter a Data Key, for example:

```text
gwf-phase3-financial-tracker
```

5. Click **Connect Firebase**.
6. Load a forecast and click **Save Dashboard Inputs** or **Save Actuals**.
7. Open the app in another browser or device, use the same Firebase config and Data Key, and click **Load Cloud Data**.

## Optional: Deploy to Firebase Hosting instead

If you prefer Firebase Hosting:

```bash
npm install -g firebase-tools
firebase login
firebase init hosting
firebase deploy
```

When prompted for the public directory, use the folder containing `index.html`.

## Operating model

Recommended process:

1. Admin/PM opens Dashboard.
2. Connects Firebase.
3. Enters Start Date.
4. Loads Forecast.
5. Saves Dashboard Inputs.
6. PM enters or uploads Actuals.
7. Saves Actuals.
8. Finance creates invoices.
9. Other users open the same app and click **Load Cloud Data**.

## Production warnings

Before using this for formal customer or finance control:

- Do not leave Firestore in test mode.
- Do not treat the Data Key as secure access control.
- Add real user roles and project membership controls.
- Move from one-document storage to normalized Firestore collections.
- Add immutable audit records.
- Add server-side export generation if invoice PDFs become contractual records.

