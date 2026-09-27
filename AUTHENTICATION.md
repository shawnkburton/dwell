# Listed authentication

Firebase project: `dwell-d6c55` (Spark plan). The website uses Firebase's modular JavaScript SDK 12.19.0 and Google OAuth popup sign-in. The public Firebase web configuration is embedded in `index.html` in `auth-config`.

Google is enabled. Microsoft and Apple have client integration code but remain disabled until their provider registrations are configured. No OAuth client secret, Apple private key, service-account key, or user token belongs in this repository.

## Provider setup still needed

### Microsoft

Register an application in Microsoft Entra. For a consumer website, choose support for organizational directories and personal Microsoft accounts. Register this Web redirect URI:

`https://dwell-d6c55.firebaseapp.com/__/auth/handler`

Enter the application's client ID and client secret in Firebase Authentication → Sign-in method → Microsoft. Keep the secret in Firebase and track its expiry. After enabling the provider, set `providers.microsoft` to `true` in `auth-config` and test with a Microsoft account.

[Official Microsoft-provider setup](https://firebase.google.com/docs/auth/web/microsoft-oauth)

### Apple

An Apple Developer Program membership and Sign in with Apple configuration are required. Configure the primary App ID, web Services ID, domain `dwell-d6c55.firebaseapp.com`, and return URL:

`https://dwell-d6c55.firebaseapp.com/__/auth/handler`

Supply the Services ID, Apple Team ID, key ID and private key in the Firebase Apple provider configuration, following Apple's requirements. Keep the private key out of this repository. Enable the provider, set `providers.apple` to `true`, and test the flow, including Hide My Email.

[Official Apple-provider setup](https://firebase.google.com/docs/auth/web/apple)

## Behavior and limits

- GitHub Pages domain `shawnkburton.github.io` is authorized in Firebase. `localhost` is also authorized for development.
- Firebase manages session persistence. Only Firebase auth-state callbacks change the signed-in UI.
- Favorites, criteria and browsing history remain in browser storage, separated by Firebase user ID. Guest data stays separate. There is no cloud sync or private listing API.
- Clearing site data removes local favorites/history. Signing out restores the guest's local list.
- The phone-frame preview directs sign-in to the full website. Use Safari, Chrome, or another supported browser with pop-ups enabled.
- If private data is added later, protect it with server-side authorization or Firebase security rules. Hiding controls in this static page is not authorization.
- Full end-to-end provider sign-in must be verified with a real account before treating this as a production authentication system.

## Verification

Local checks covered guest/account separation, switching accounts, restoring guest data on sign-out, rendering names as text, and rejecting malformed saved preferences. The mobile account dialog was reviewed at 390px. Firebase configuration and SDK initialization were checked in the browser.
