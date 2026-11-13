# Hira & Hamza – BARAT-ONLY INVITATION VERSION

> **This is the Barat-Only Invitation Version.** It is a separate copy of the latest full
> wedding invitation (with the Jashn-e-Bahaaraa song and event timings), for guests invited
> only to the Baraat. The full invitation is a different folder / ZIP and is unchanged.

## Guest flow (this version)

**Opening page → Open Invitation (song starts) → Couple Introduction → Baraat → Thank You.**

* "Open Invitation" opens the **Couple Introduction** page (Hira Rasul & Hamza Azhar and their
  parents) and starts the song (it begins at the original track's 00:22 and keeps playing,
  never restarting, through every page).
* Scrolling/swiping forward goes to **Baraat** (date, timings Arrival 6:00 PM · Dinner 8:00 PM ·
  Rukhsati 10:00 PM, venue, map link, client message) and then to **Thank You**.
* The side dots show three pages: Couple, Baraat, Thank You.
* The **Mehndi** and **Walima** pages are skipped: their code and images are still in the
  project (marked `hidden data-skipped="barat-only"`) but are never displayed, reachable, or
  downloaded.

The page order is set in one place: search `index.html` for **PAGE_SEQUENCE**
(`['scene-0', 'scene-1', 'scene-3', 'scene-5']`). The page title / link-preview title say
"Baraat Invitation".

Pure HTML + CSS + vanilla JavaScript. No build step, no external dependencies
(fonts are self-hosted), so it loads fast on mobile data in Pakistan and the UK.

## Folder structure

```
wedding-invitation/
├── index.html                  ← the whole website (HTML + CSS + JS)
├── README.md
└── assets/
    ├── images/
    │   ├── scene-0-opening.webp    Opening page: lace envelope card (new)
    │   ├── scene-1-couple.webp     Bride & groom
    │   ├── scene-2-mehndi.webp     Mehndi & Qawali   (new image, from 2.png)
    │   ├── scene-3-baraat.webp     Baraat            (new image, from 3.png)
    │   ├── scene-4-walima.webp     Walima            (approved image, unchanged)
    │   ├── scene-5-thankyou.webp   Thank you
    │   └── share.jpg               WhatsApp / social link preview
    ├── audio/jashn-e-bahaaraa.mp3  Wedding song (starts at the original's 00:22)
    └── fonts/                      Great Vibes, Cormorant Garamond, Jost, Amiri Quran (woff2)
```

## Run locally

Open `index.html` in a browser, or serve the folder:

```
cd wedding-invitation
npx http-server -p 8000        # or any static server that supports Range requests
```
(Python's built-in `http.server` does not support audio seeking, so use another
static server when testing the audio loop locally. Every real web host is fine.)

## Host online (free options)

Upload the **whole folder** (keep `index.html` and `assets/` together):
Netlify (drag & drop at app.netlify.com/drop), Cloudflare Pages, GitHub Pages,
Vercel, or any normal web hosting. Always use **https**.

## Event details (all kept in the file; only Baraat is shown in this version)

| Event | Date | Venue | Schedule |
|---|---|---|---|
| Mehndi & Qawali | Wednesday, 23rd December 2026 | MXVP+8CR, Main Margalla Road, NPF E-11/4, E-11, Islamabad, 45000, Pakistan | Rasm-e-Mehndi 6:00 PM · Dinner Served 8:00 PM · Qawali Event Starting 9:30 PM |
| Baraat | Friday, 25th December 2026 | The La Quinta Glass Marquee, Main Boulevard, Phase 7, Bahria Town, Rawalpindi, 46620, Pakistan | Arrival Time 6:00 PM · Dinner Served 8:00 PM · Rukhsati 10:00 PM |
| Walima | Saturday, 26th December 2026 | Aura Grande Arena (View on Map link: https://share.google/Ifg3RmkhfBxaBlJZP) | Arrival Time 7:00 PM |

The schedule appears right under the date. To change a time, search `index.html` for
`class="times` (one list per event) and edit the `t-label` / `t-time` text.

Each event page shows the heading, date and venue on the first screen; scroll down
(or swipe up) to read the client's invitation message. At the end of the message,
the next swipe/scroll moves on to the next page.

To edit an event message or venue, open `index.html` and search for the event
(e.g. `scene-4` for Walima). The message is inside `<div class="ev-message">`.

## Opening page (Page 0)

The lace envelope card is `assets/images/scene-0-opening.webp`. The text on the card
("Wedding Ceremony Of / Hira with Hamza"), the Quranic Ayat (Surah Ar-Rum 30:21,
set in the Amiri Quran font) and the **Open Invitation** button are live HTML on top of
the image. Search `SCENE 0` in `index.html` to edit them. The button starts the
music and opens the next page, exactly as before.

## After hosting

* In `<head>`, replace `https://YOUR-DOMAIN.com` in the `og:image` tag with your real
  address so WhatsApp shows the link preview image.

## Changing speeds and darkness (beginner-friendly)

Open `index.html` in any text editor, press Ctrl+F (Cmd+F on Mac) and search for
**CUSTOMIZATION SETTINGS**. Everything is in that one block. Change a number, save,
refresh. 1000ms = 1 second.

| Setting | Now | Bigger number = | Smaller number = |
|---|---|---|---|
| `--event-overlay-opacity` | 0.6 | darker event images | lighter |
| `--event-scrim-opacity` | 0.26 | darker shade behind headings | lighter |
| `--text-duration` | 1600ms | slower text fade-in | faster |
| `--text-start-delay` | 400ms | longer wait before first line | quicker start |
| `--text-stagger` | 250ms | bigger gap between lines | lines appear closer together |
| `--text-rise` | 6 | text floats up further | 0 = only fades |
| `--fog-duration` | 500ms | slower white mist | faster |
| `--scene-fade-duration` | 400ms | slower image fade | faster |
| `--button-pulse-duration` | 2200ms | slower button pulse | faster |
| `--image-drift-duration` | 18s | slower background zoom | faster |

## Music — "Jashn-e-Bahaaraa"

* One audio player for the whole visit. It starts only when the guest taps **Open Invitation**
  (browsers require a tap) and is never touched by page navigation or the fog transitions,
  so it never restarts between pages.
* **The song begins at the original's 00:22.** `assets/audio/jashn-e-bahaaraa.mp3` is the
  original track with its first 22 seconds (the intro) already removed. This is deliberate:
  asking a phone to "jump to 22 s" inside a large MP3 is unreliable (the song would not play
  on many phones). With the intro removed from the file, nothing has to jump, so it starts
  instantly and reliably on every phone and computer.
* Pause/play and mute/unmute are in the top-right corner after opening.
* When the song ends it repeats from its start (= the original's 00:22).
* If the song file ever fails to load, the music controls are hidden and the invitation
  keeps working silently. If a very slow connection leaves it stuck for 6 seconds, the page
  automatically retries once.
* Hosting: use any normal host (Netlify, Cloudflare Pages, GitHub Pages, Vercel, cPanel…).

### Changing the start point or the song
Make a new file with ffmpeg (replace 22 with the second you want the song to start at) and
overwrite `assets/audio/jashn-e-bahaaraa.mp3`:

```
ffmpeg -i original-song.mp3 -ss 22 -af "afade=t=in:st=0:d=0.05" -c:a libmp3lame -b:a 128k jashn-e-bahaaraa.mp3
```
* The Quranic Ayat on the opening page is text and is not part of the audio.
