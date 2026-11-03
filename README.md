# Our Bucket List 🧡

A free, single-page bucket list for two people (or friends, or family) to plan what they want to do together, stamp it when it's done, and keep the memories.

Dark, gold-and-purple ticket design. Works on any phone browser. No account needed to use it. Optional live sync lets two phones share one list.

**Live page:** https://izzy-10.github.io/our-bucket-list/

---

## Features

- **Ticket list:** an example list of 10 tickets. Tap a ticket to stamp it **DONE**.
- **Edit your own plan:** edit or delete any ticket, add new ones, or start with a blank list.
- **Templates:** load a ready-made list for **Couples**, **Besties** or **Family**.
- **Categories and filter:** Food, Music, Travel, Adventure, Chill, Together.
- **Budget:** optional cost per ticket, with a "still to budget / spent" total.
- **Place:** optional location with a Google Maps link.
- **Plan dates and countdown:** pick a date for a ticket, see a "Next up" banner and add it to your calendar (`.ics` download with a reminder the day before).
- **Live now:** do one ticket with a timer and simple steps.
- **Memories:** a date, a one-line note, a song and a photo for each finished ticket.
- **Our Story:** a recap of all your memories, a photo gallery, and a button to save it as one image.
- **Stats:** tickets done, planned, memories saved, days together.
- **Celebration:** gold confetti when the last ticket is stamped.
- **isiZulu and English:** switch language from the ☰ menu.
- **Getting started card and menu:** explains how to use the page.
- **Live sync (optional):** both phones see the same list, using Firebase.

## How it's built

- One file: [`index.html`](index.html). HTML, CSS and vanilla JavaScript, no build step.
- Fonts: Fraunces and DM Sans from Google Fonts.
- Data is saved in the browser (`localStorage`) on each device.
- Optional sync: Firebase **Anonymous Authentication** and **Cloud Firestore** (free Spark plan).

## Use it

### Open locally
Download `index.html` and open it in a browser. It works straight away, saving to that device only.

### Put it online with GitHub Pages
1. Make the repository **Public**.
2. Go to **Settings → Pages**.
3. Under **Build and deployment → Source**, choose **Deploy from a branch**.
4. Choose branch `main` and folder `/ (root)`, then save.
5. After a minute, your page is at `https://<your-username>.github.io/<repository-name>/`.

## Turn on live sync (optional)

Sync is off until you add your own Firebase project.

1. Create a project at [console.firebase.google.com](https://console.firebase.google.com).
2. **Authentication → Sign-in method:** enable **Anonymous**. Under **Settings → Authorized domains**, add your GitHub Pages domain (for example `your-username.github.io`).
3. **Firestore Database → Create database:** keep the database ID `(default)`, choose a location, and start in **Production mode**.
4. In Firestore, open **Rules**, replace everything with the rules below and **Publish**:

   ```
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /rooms/{room}/{document=**} {
         allow read, write: if request.auth != null;
       }
     }
   }
   ```

5. In **Project settings → Your apps**, register a **Web app** and copy the config.
6. In `index.html`, find the line starting `var FIREBASE_CONFIG=` and fill in your values.
7. Upload the file again. Open the page, tap **☰ → Sync your phones**, type a secret code of at least 8 characters, and tap **Connect**. Send the invite link to your partner.

When the status line under the names says **● Synced live**, both phones are connected.

## Privacy and limits

- Without sync, everything stays on your own device.
- With sync, your list, notes and photos are stored in a private "room" in your own Firebase project. **Anyone who has your secret code can see and edit that room.** Use a long code and only share it with people you trust.
- Firebase web config values identify your project. They are not secret, but your Firestore rules and room code protect your data.
- Photos are shrunk before saving. Without sync, around 20 to 30 photos fit on one device. With sync, they are also stored in Firebase.
- Tickets people write themselves, and the Besties and Family template tickets, are not translated.

## Customise

- **Example tickets:** edit the `items` list near the top of the main script in `index.html`, or just use **Edit** and **Delete** on the page.
- **Colours:** change the `--maroon`, `--navy`, `--purple` and `--gold` values at the top of the style block.
- **Footer links:** search for `tiktok.com` and `wa.me` in `index.html` and replace them with your own.

## Author

Built by **Sizwe Sicelimilo Sibiya** in Durban, South Africa.

TikTok: [@sizwesibiya7](https://tiktok.com/@sizwesibiya7)

© 2026 Sizwe Sicelimilo Sibiya. All rights reserved.
