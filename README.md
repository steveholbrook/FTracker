# Financial Tracker v3.3 Multi-Project

## Fix included

This build corrects the project selection issue on the opening login page.

Changes:
- Always initialises the login project dropdown with default projects: GWF and Blackmores.
- Sanitises and merges any cloud project registry with the default projects.
- Prevents an empty or invalid cloud registry from wiping the project dropdown.
- Sets a safe default selected project.
- Widens the project dropdown for usability.

## Deploy to FTracker repository

1. Open this ZIP.
2. Copy `index.html` into the root of the FTracker GitHub repository.
3. Commit and push.
4. Wait for GitHub Pages deployment to complete.
5. Open the app and confirm that GWF and Blackmores appear on the login screen.

## Admin login

Default admin password:

```text
admin
```

Viewer mode does not require a password and is read-only.
