# Setup (about 10 minutes, all free)

The site now stores accounts and trade data online with Firebase, so every
device sees the same users and data, and password-reset emails are sent for you.

## 1. Create the Firebase project
1. Go to https://console.firebase.google.com and sign in with a Google account.
2. **Add project** -> name it (e.g. basket-pnl-tracker) -> continue (Analytics can be off).

## 2. Turn on login
1. **Build -> Authentication -> Get started -> Sign-in method -> Email/Password -> Enable -> Save**.
2. **Users tab -> Add user** and create the MAIN ADMIN first, before sharing the website:
   - Email: `indexreturns@gmail.com`
   - Password: your admin password
   (Doing this first stops anyone else from registering that email.)
3. **Settings tab -> Authorized domains -> Add domain**: your Vercel address,
   e.g. `basket-pnl-tracker.vercel.app` (and your own domain if you add one).

## 3. Create the database
1. **Build -> Firestore Database -> Create database** -> region `asia-south1 (Mumbai)` -> **Production mode**.
2. Open the **Rules** tab, delete everything, paste the contents of `firestore.rules`, click **Publish**.

## 4. Connect the website
1. **Project settings (gear icon) -> Your apps -> Web (`</>`)** -> register the app.
2. Copy the `firebaseConfig` values.
3. Open `index.html`, find `const FIREBASE_CONFIG={...}` near the bottom, and paste
   `apiKey`, `authDomain`, `projectId`, `storageBucket`, `messagingSenderId`, `appId` between the quotes.
   (These values are meant to be public; the Firestore rules are what protect your data.)

## 5. Publish
Upload the updated files to GitHub; Vercel redeploys automatically.

## Notes
- Existing trade data: the first time the main admin logs in on the browser that holds
  your old data, it is uploaded automatically.
- Password reset emails come from Firebase (noreply@<project>.firebaseapp.com) and may
  land in spam. You can customise them under Authentication -> Templates.
- Two admins editing at the same moment: the last save wins.
