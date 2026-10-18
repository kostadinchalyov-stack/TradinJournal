# Enable website trade sync

The website now stores each signed-in user's trades and accounts in Cloud Firestore. Local saves continue to work when the device is offline. To turn on sync for the public GitHub Pages site, enable Firestore and publish the included security rules.

## 1. Create the database

1. Open the [Firebase Console](https://console.firebase.google.com/) and select project `tradelog-575b8`.
2. Open **Build → Firestore Database** and choose **Create database**.
3. Choose a database location and finish creation. Keep production rules selected; do not enable public test mode.

## 2. Publish the included rules

From this repository folder, run:

```powershell
npx firebase-tools login
npx firebase-tools deploy --only firestore:rules --project tradelog-575b8
```

The rules in `firestore.rules` restrict all trade and account documents to the matching Firebase Authentication UID. The website does not need an admin key.

## 3. Publish the website

Commit and push the updated `index.html`, `firebase.json`, and `firestore.rules` to the GitHub repository. GitHub Pages will serve the updated sync controls after its deployment finishes.

Then open the site over HTTPS, sign in, and press **Sync now**. The first sync merges the journal already on that device with the signed-in account's cloud journal. Later saves sync automatically. A signed-in account only loads that account's local cache when switching users on the same device.

If the sync badge says **Setup required**, create the Firestore database. If it says **Rules needed**, deploy `firestore.rules` and retry. Review Firebase's current usage and billing settings before a public launch.
