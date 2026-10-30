# Golf Is Fun

A golf scorecard for you and your friends. Score each hole with faces or numbers, flip to the full card, share a live round code, and keep past rounds on your phone. It installs to the home screen like an app.

**Faces:** 🤯 albatross · 🤩 eagle · 😁 birdie · 🙂 par · 😐 bogey · 😬 double · 😩 triple · 😭 quad · 💀 worse · ⛄ any 8 (snowman) · ☠️ 9 or more

## What's in this folder

| File | What it does |
|---|---|
| `index.html` | The whole app |
| `config.js` | Your Firebase settings for live sharing (empty until you set it up) |
| `manifest.webmanifest`, `icons/` | Lets phones install it as an app |
| `sw.js` | Keeps the app working with no signal on the course |
| `database.rules.json` | Security rules to paste into Firebase |

## 1. Put it on GitHub Pages

1. Create a new **public** repository on GitHub, for example `golf-is-fun`.
2. Upload every file in this folder to the root of the repo, keeping the `icons` folder.
3. In the repo, go to **Settings > Pages**. Under "Build and deployment", choose **Deploy from a branch**, pick `main` and `/ (root)`, and save.
4. After a minute or two the app is live at `https://YOUR-USERNAME.github.io/golf-is-fun/`.

The app works at this point. Each phone keeps its own scores and history. Round codes stay off until step 2.

## 2. Turn on live sharing (one time, about 10 minutes)

Live round codes use Firebase Realtime Database. The free Spark plan should be plenty for a group of friends, but check Firebase's current limits and pricing.

1. Go to the Firebase console and **create a project**. Google Analytics is optional; you can turn it off.
2. **Realtime Database:** open Build > Realtime Database > Create database. Pick a location near you and start in **locked mode**.
3. **Rules:** in the database's **Rules** tab, replace everything with the contents of `database.rules.json`, then Publish.
4. **Sign-in:** open Build > Authentication > Get started > Sign-in method, and enable **Anonymous**. Friends never create accounts; this just keeps random bots out.
5. **Allow your site:** in Authentication > Settings > Authorized domains, add `YOUR-USERNAME.github.io`.
6. **Get your settings:** open Project settings (gear icon) > Your apps > the web icon `</>`. Register an app (no hosting needed) and copy the `firebaseConfig` values.
7. Open `config.js` in your repo, replace `window.FIREBASE_CONFIG = null;` with your values, and make sure it includes `databaseURL`. Commit the change.

Menu names in the Firebase console change from time to time, so the labels above may differ slightly.

**Is it safe to put the Firebase config in a public repo?** Firebase treats these values as identifiers, not passwords; the database rules are what protect your data. Anyone who has a round code can view and edit that round, so only share codes with your group.

## 3. Install it on your phone

- **iPhone (Safari):** open the link, tap Share, then **Add to Home Screen**.
- **Android (Chrome):** open the link, tap the ⋮ menu, then **Install app** or **Add to Home screen**.

## Playing a round with friends

1. One person taps **Menu**, enters the course, date, and players, then taps **Tee off**.
2. Tap **Share** to get a 6-character code and an invite link.
3. Friends open the link, or type the code under **Join a friend's round**.
4. Anyone can enter scores for anyone, and every phone updates live. Scores entered with no signal sync once the phone reconnects.
5. Tap **Save round** at the end to keep it in your History. Each person saves to their own phone.

## Course search

Typing a name searches OpenStreetMap, and **Near me** lists courses within about 25 miles using your location. Both are free and need no key. Smaller courses are sometimes missing from OpenStreetMap, so you can always keep whatever you typed.

## Updating the app

Edit the files on GitHub and commit. Phones pick up the new version the next time they open the app with a signal.
