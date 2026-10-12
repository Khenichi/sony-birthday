# Sony Birthday — Firebase Setup

1. Go to https://console.firebase.google.com/ and **Add project**.
2. Project Overview > gear icon > Project settings > **Your apps** > **Web** (`</>`). Register a web app. Copy its Firebase config into `firebase-config.js`.
3. Build > **Firestore Database** > Create database > select a region near your guests > create. Open **Rules**, paste `firestore.rules` and replace `PASTE_ADMIN_USER_UID` with your admin account UID. Publish.
4. Build > **Authentication** > Get started > Sign-in method > enable **Email/Password**.
5. Authentication > **Users** > Add user (admin email and strong password). Copy this user's **UID** into `firebase-config.js` as `ADMIN_UID`. Use the same UID in Firestore rules.
6. Authentication > Settings > Authorized domains: add your production domain if needed.
7. Host the entire folder via Firebase Hosting, Netlify, Vercel or another HTTPS static host. Do NOT open index.html using `file://`: JavaScript modules require a web server. For local testing, from this folder run `python -m http.server 8080`, then visit http://localhost:8080.
8. Open the website, RSVP with a test name, then use **Organizer login** in the footer. The dashboard lists guests and exports CSV.

IMPORTANT:
- Firebase web config is safe to include client-side. Never put an Admin SDK service account or private key in the website.
- Firestore rules are the security boundary; hiding the admin UI is NOT access control.
- Public unauthenticated RSVP creation can be spammed. For a larger/public event, enable App Check and/or implement rate limiting through a server or Cloud Function.
- Each submission creates a new entry; this simple version does not deduplicate names or support editing.
- Admin list is fetched on login; sign out and sign in again to refresh.
- RSVP data is private and should only be collected as needed.
