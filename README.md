# Präpositionen-Trainer

A browser trainer for German **verbs with prepositions** (A1–C2). You don't pick the preposition from a list: you type it straight into the sentence, in the form the sentence needs (*zum*, *am*, *darauf*, *miteinander* …).

**Live demo:** `https://<your-username>.github.io/<repo-name>/` <!-- replace after enabling GitHub Pages -->

## Features

- **882 verbs** across six levels (A1 19 · A2 67 · B1 245 · B2 394 · C1 131 · C2 26), each with a full example sentence and the case (Akk. / Dat.).
- **Three topics, trained separately:**
  - **Prepositions**: sentence mode, plus a small-talk mode with 65 short dialogues where you fill every gap.
  - **da-/wo-words** (176 cards): *dafür, dagegen, davon, darauf, worüber, wovon* …
  - **-einander** (48 cards): *miteinander, voneinander, aufeinander, ineinander* …
- **Three views:**
  - **Cards**: one sentence at a time.
  - **Sheet**: every sentence of the chosen levels on one page.
  - **Verbs**: a searchable list with your learning status.
- **Spaced repetition** (Leitner boxes): known cards come back after 1, 3, 7, 14 and 30 days; mistakes come back in the same round.
- **Forgiving answer check:**
  - `ue/ae/oe` count as umlauts.
  - *zu dem* counts for *zum*, with a hint that the contracted form is more common.
  - Colloquial *drauf, dran, drüber* are accepted.
  - Where two prepositions are both correct, the second one is accepted too.
  - Targeted hints for typical mistakes: missing contraction, wrong case, *auf das* instead of *darauf*, missing *-r-* in *dar-*.
- **Keyboard-first**: you never need the mouse (see below).
- **Five interface languages**: Russian, Ukrainian, English, German (German meaning instead of a translation) and Arabic (right-to-left layout).
- Light and dark theme, works on phones.

## Keyboard shortcuts

| Key | Cards | Sheet |
|---|---|---|
| `Enter` | check the answer / next card | check the row and jump to the next one |
| `Esc` | "I don't know": show the answer | show the answer for this row |
| `1` / `2` | choose Akk. / Dat. (also submits) | — |
| `Tab` | next gap in a dialogue | next gap |

A correct answer moves on automatically after about a second. You can switch this off on the start screen.

## How progress is saved

Everything stays in your browser, in `localStorage`, so nothing is sent anywhere:

| Key | Content |
|---|---|
| `praep-trainer-progress-v1` | learning progress for every card |
| `praep-trainer-settings-v1` | language, levels, topic, round length, toggles |

For each card the trainer stores `[box, next review, reviews, mistakes, last answer]` under the key `mode|card-id`, for example `s|A2:warten auf`. The modes are `s` (sentence), `d` (small talk), `pa` (da-/wo-words) and `ei` (-einander), so each topic has its own progress.

| Event | Effect |
|---|---|
| Correct answer | the card moves up one box (max. 5); next review after 1, 3, 7, 14 or 30 days |
| Mistake | back to box 0; the card returns three cards later in the same round |
| Card reaches box 3 | it counts as learned |

Progress lives in one browser on one device. Private windows, clearing site data or opening the page from another domain start from zero. The **Reset progress** button on the start screen erases it on purpose.

When the page runs as a Claude artifact on claude.ai, it also syncs progress to the viewer's Claude account. If that isn't available, it falls back to the browser.

## Run locally

No build step and no server needed. Download `index.html` and open it in a browser.

## Deploy to GitHub Pages

1. Create a repository and upload `index.html` and `README.md`.
2. Go to **Settings → Pages**, choose **Deploy from a branch**, then branch `main` and folder `/ (root)`.
3. After a minute the trainer is live at `https://<your-username>.github.io/<repo-name>/`.

Netlify Drop, Cloudflare Pages and Vercel work the same way: it is a single static file.

## Project structure

```
index.html   the whole app: markup, styles, script and data
README.md
```

The card data is embedded in `index.html` as JSON inside `<script type="application/json" id="data">`, with three arrays: `cards`, `da` and `ei`. One card looks like this:

```json
{
  "id": "A2:warten auf",
  "l": "A2",
  "b": "warten",
  "p": "auf",
  "c": "A",
  "ex": ["0Wir ", "1warten", "0 ", "2auf", "0 den Bus."],
  "ru": "ждать", "uk": "чекати", "en": "to wait for", "ar": "ينتظر", "de": "bleiben, bis jemand oder etwas kommt"
}
```

| Field | Meaning |
|---|---|
| `l` | level |
| `b` | verb |
| `p` | preposition |
| `c` | case (`A` / `D`) |
| `ex` | the example sentence, split into segments |
| `st` | optional small-talk dialogue, in the same segment format |
| `alt` | optional list of other accepted prepositions |

Each segment in `ex` starts with a flag:

| Flag | Meaning |
|---|---|
| `0` | plain text |
| `1` | highlighted verb |
| `2` | the gap (its text is the expected answer) |

Card ids never change, so saved progress survives updates to the data.

## Sources

The verb lists were compiled from several learning materials: the exercises on deutschlernerblog.de, the *Kontext C1* verb list (Klett), the PONS list *Verben mit Präpositionen*, easy-deutsch.de *137 Deutsche Präpositionen*, and a verb government (Rektion) list. Duplicates and purely literal combinations were removed. All example sentences, dialogues and translations were written for this project.

## Tech

Plain HTML, CSS and JavaScript, with no frameworks and no dependencies. The only external resources are the Onest, IBM Plex Sans Arabic and JetBrains Mono fonts from Google Fonts.
