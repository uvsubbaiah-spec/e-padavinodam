# ఈ-పద వినోదం — website and phone app

A phone-first web app for **telugupadavinodam.blogspot.com**. It reads every padavinodam post straight from the blog's feed, turns it into a playable crossword with a Telugu akshara keypad, and works offline after the first visit. It can be installed on Android from Chrome like a normal app.

No server, database or payment card is needed: these are plain static files.

## What's in the folder

| File | Purpose |
|---|---|
| `index.html` | The whole app (layout, styles and code in one file) |
| `puzzles.json` | Extra posts made in the Claude studio (uploads, corrections). Starts empty. |
| `rain.webp` | Animated rain for the black squares (from the blog's GIF, compressed) |
| `sw.js` | Offline support |
| `manifest.webmanifest`, `icon-*.png`, `apple-touch-icon.png` | App name and icons for "Install app" |
| `.nojekyll` | Tells GitHub Pages to serve the files as they are |

## Put it online with GitHub Pages (free, no card)

1. Sign in to github.com and create a new **public** repository, for example `padavinodam`.
2. On the repository page choose **Add file → Upload files**, drag in **every file from this folder** (not the folder itself), and press **Commit changes**.
3. Open **Settings → Pages**. Under *Build and deployment* choose **Deploy from a branch**, branch **main**, folder **/ (root)**, and press **Save**.
4. After a minute or two the site is live at `https://<your-github-name>.github.io/padavinodam/`.

Other no-card options that work the same way: **Netlify Drop** (app.netlify.com/drop — drag the folder in) and **Cloudflare Pages** (upload the folder as a project).

The site must be served over **https** for offline support and installing; all three hosts above do that automatically.

## Install on an Android phone

Open the site in **Chrome** → menu (⋮) → **Install app** (or **Add to Home screen**). It opens full-screen with its own icon, like any other app.

## Typing answers

A bar above the keyboard switches between **తెలుగు** (the in-app Telugu akshara keypad, one akshara per tap) and **ENG** (type the whole word on any phone keyboard), and **దాచు** hides the keyboard to show the whole grid.

In ENG, type the complete answer and press space, Enter or **పెట్టు**: the app splits it into aksharas and puts them in the selected word's squares. A full-length word always starts from the word's first square, wherever the cursor is; a shorter piece goes from the selected square. While you type, the word's squares are shown right above the box (and in the grid, dashed) so you see where each akshara will land, and the board stays visible above the phone keyboard. `kamalam` → కమలం, `sankraanti` → సంక్రాంతి, `amma` → అమ్మ. Capitals give the harder sounds (T ట, D డ, N ణ, L ళ, Sh ష, E ఏ, O ఓ) and `aa`/`ee`/`oo` give long vowels; the app also offers the likely alternatives to tap. A Telugu phone keyboard works in the same box. On a computer, just start typing letters while a puzzle is open.

Answer colours follow the blog: a right letter turns grey with a green border and blue letter, a wrong one gold with a red border and red letter. A right letter is frozen: typing and delete pass over it. The selected square has a blue frame.

**ఆటో** (next to సులభం / కష్టం, on puzzles that have answers) fills the answers by itself, one clue at a time: it selects each clue, shows it on the clue bar and writes its answer letter by letter, so the player learns every answer. Pause, next clue, stop and three speeds are under the board. Auto-filled letters count as hints; afterwards **గడి ఖాళీ చేసి మీరే ఆడండి** empties the grid to play it yourself.

A puzzle opens at the biggest zoom (200%) with the keyboard hidden; the first tap on a square brings the keyboard back. The bar above the clue scrolls the board sideways (drag it or use its arrows). On a computer the arrow keys move the selected square across and down, and the board scrolls along.

## Look

Settings (అమరికలు) has six Telugu font sets (బ్లాగ్ శైలి is the default: Ramabhadra in the squares, Anek Telugu for clues, as on the blog) and separate choices for the squares, the clues and the headings, from about 25 Telugu fonts on Google Fonts. Only the chosen fonts are downloaded; after the first load they work offline.

The black squares show small animated scenes (a dancing peacock, the roaring sea, a roaring lion, rain with a paper boat, flowers blooming, fireflies, a cat watching the moon, koi, a bird at dusk, a butterfly, an owl, a parrot, falling leaves). Each post uses one of them in all its black squares, as the blog uses one picture; weekly posts take the scenes in turn.

## Recording a game

On a computer (Chrome or Edge), the red circle on the puzzle's top bar records the screen, as the blog's రికార్డు చేయండి button does. The browser asks which tab or screen to share; pick this tab. Press the red button again, or the floating "ఆపు" pill, to stop; the video is saved to Downloads named after the puzzle date (for example `180525.mp4`). Phones' browsers cannot record the screen, so on a phone use the phone's own screen recorder (Android: quick settings → Screen record). The blog's rain picture or plain black can be chosen instead. Phones set to reduce motion get still pictures.

The magnifier buttons on the puzzle's top bar zoom the grid from 100% to 200% (it then scrolls sideways); pinch-zoom on the phone works too.

## Keeping posts up to date

- **New blog posts appear on their own.** Every time the app opens it reads the blog's feed (the blog must stay public).
- **Posts made in the Claude studio** (from a newspaper photo or PDF, or a corrected blog post) live in `puzzles.json`. In the studio's admin page press **puzzles.json సేవ్ చేయండి**, then upload that file to the repository in place of the old one. A post in `puzzles.json` replaces the blog post with the same date.
- **Correcting a clue's Telugu text:** in the Claude studio, open the puzzle, select the clue and tap the pencil on the clue bar (or use **మార్చు** in the admin list for the full editor). Type the fix in Telugu, or in English and it converts. Save publishes it in the studio at once; export `puzzles.json` as above to update the website. For blog posts, import them into the studio first (admin page → బ్లాగ్ నుంచి దిగుమతి) so there is a copy to correct.

## Admin on the website and in the app

Settings → **నిర్వాహకుడి ప్రవేశం** (at the bottom). Sign in once per device with a GitHub fine-grained token for this repository (Contents: Read and write); the page shows how to make one. After that:
- **కొత్త పద వినోదం**: start from an empty 12×12 grid, set black squares, numbers, clues and answers, and publish;
- **ఫైల్ నుంచి దిగుమతి**: a `puzzles.json` saved in the Claude studio (for posts read from newspaper photos), a blog feed or a post page;
- **మార్చు / తొలగించు** on any post, including blog posts (to add answers or fix clues), and the pencil on the clue bar to correct one clue while playing.

Publishing writes `puzzles.json` in this repository through GitHub's API; the site picks it up within a minute or two. The token stays on that device only; revoke it on GitHub if a device is lost. Reading newspaper photos with AI is only in the Claude studio.

## The Android app (APK)

The APK built in Android Studio opens this site full-screen. Name the signed release file **`e-padavinodam.apk`** and upload it to this repository next to `index.html`. It is then always the latest one at `https://uvsubbaiah-spec.github.io/e-padavinodam/e-padavinodam.apk`:
- the site shows an **Android యాప్ డౌన్‌లోడ్ (APK)** card on Android phones (home page and Settings), and never inside the app itself;
- the blog shows a **⬇ Android యాప్** button in its phone bar and a download pill on computers;
- both appear only once the file is really there.

For an update, raise `versionCode` (and `versionName`) in `app/build.gradle.kts`, build with the **same keystore**, and upload with the same file name. Content changes never need a new APK: the app always shows the live site.

## Putting it on the Play Store (optional)

Go to **pwabuilder.com**, enter your site's address and choose **Package for stores → Android**. It produces:
- an **APK** you can install directly or share with people, with no store and no fee, and
- an **AAB** for the Play Store. Publishing there needs a Google Play developer account, which has a one-time registration fee paid by card.

## Try it on your computer first (optional)

From this folder run `python -m http.server 8000` and open `http://localhost:8000`. Offline support works on localhost too.

## Notes

- Puzzle content comes from the blog; the crosswords themselves are Eenadu's. Check permission before publishing the app widely or on a store.
- Progress, settings and the chosen theme are kept on each phone only.
