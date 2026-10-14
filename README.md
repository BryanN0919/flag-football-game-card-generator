# 🏈 Flag Football Game Card Generator

A lightweight, browser-based tool for creating professional, printable flag football officiating game cards for **3-person and 4-person crews**. Enter game information, assign officials, customize association logos, and print or download four matching cards on a standard US Letter page.

**Developer:** Bryan Norfleet  
**Platform:** Static web application (HTML, CSS, JavaScript)

## Features

- **Crew selection:** Switch between 3-person and 4-person officiating crews. The 4-person crew includes Referee, Line Judge, Back Judge, and Field Judge; the Field Judge is omitted from the 3-person layout.
- **Game details:** Enter home and away teams, game date, optional kickoff time, and optional location.
- **Live preview:** Automatically updates four matching cards in a two-column layout on an 8.5 × 11-inch page.
- **Custom logos:** Replace either default association logo with an uploaded image, or reset it to the default.
- **Appearance options:** Light/dark interface toggle and light-pink/gray card information bands. The printable cards remain white in dark mode.
- **Browser persistence:** Saves entered details, preferences, and uploaded logo data using `localStorage`.
- **Printing and PDF export:** Print directly or generate a downloadable PDF in the browser.
- **Responsive layout:** Adapts the editing interface and preview to narrower screens.

## Live site

When GitHub Pages is enabled for this repository, visit the URL shown under **Settings → Pages**.

## Technology

| Technology | Purpose |
| --- | --- |
| HTML5 | Form, game-card template, and page structure |
| CSS3 | Layout, responsive design, print formatting, and themes |
| Vanilla JavaScript | State, event handlers, preview rendering, and browser storage |
| [html2canvas 1.4.1](https://html2canvas.hertzen.com/) | Captures the card sheet for PDF generation |
| [jsPDF 2.5.1](https://github.com/parallax/jsPDF) | Produces and downloads the PDF |
| `localStorage` | Retains preferences and game details in the current browser |

The two PDF-related libraries are loaded from cdnjs, so an internet connection is normally needed to load them unless already cached.

## Project structure

```text
flag-football-game-card-generator/
├── index.html
├── img/
│   ├── cffo-logo-trade-mark-orig.png
│   └── CHSAA_new-logo.webp
└── README.md
```

> Keep the exact filenames and capitalization of the two default images: the application references these relative paths directly. HTML, CSS, and JavaScript are contained in `index.html`.

## Getting started

1. Clone the repository or download its files.
2. Keep `index.html` and the `img/` directory together in the structure shown above.
3. Open `index.html` in a modern browser. Alternatively, serve the directory with a local static web server, for example:

   ```bash
   python3 -m http.server 8000
   ```

4. If using the local server, navigate to `http://localhost:8000`.

No package manager, build step, or backend is required.

## How to use

1. **Choose crew size:** Select **3-PERSON** or **4-PERSON**.
2. **Enter game information:** Supply the home and away teams and date; kickoff time and location are optional.
3. **Enter officials:** Fill in the names of the officials for the selected crew.
4. **Customize logos:** Use **Change** for either logo, or **Reset** to restore its default.
5. **Select the card band color:** Choose **Light Pink** or **Grey**. Optionally switch the editing interface between light and dark mode.
6. **Review the preview:** Four copies of the card appear on a US Letter-sized sheet.
7. **Export:** Select **Print** to open the browser print dialog, or **Download PDF** to save the sheet.

**Clear All** clears game and official text fields. It does not reset the selected crew size, appearance, card band color, or uploaded logos.

### PDF filename

The current implementation generates a filename using this format:

```text
YYYY-MM-DD-Home-Team-Away-Team-ff-game-card.pdf
```

For example:

```text
2026-10-18-Bulldogs-Titans-ff-game-card.pdf
```

Spaces in team names become hyphens; unsupported punctuation is removed. If the date is empty or invalid, `undated` is used. Missing team names fall back to `Home` and `Away`.

## Printing notes

- Page size: **US Letter, portrait (8.5 × 11 inches)**.
- Layout: **four identical cards per page**, arranged in two columns.
- For browser printing, choose Letter paper, use 100% scale where available, and enable background graphics if the card band color is missing.
- The PDF export uses `html2canvas` and `jsPDF`. If PDF generation fails, the application opens the browser print dialog as a fallback.

## Browser storage and privacy

The application saves its state locally under the `localStorage` key:

```text
flag_football_card_generator_v2
```

Game details and uploaded logo images are stored in the browser, not sent to an application backend. Clearing browser storage or using a different browser/device may remove saved settings. Large uploaded images may exceed browser storage limits.

## Deploy with GitHub Pages

1. Push `index.html`, `img/`, and `README.md` to the repository's publishing branch.
2. On GitHub, open **Settings → Pages**.
3. Under **Build and deployment**, select **Deploy from a branch**.
4. Select the branch (commonly `main`) and **/(root)**, then save.
5. Open the published URL displayed by GitHub after deployment.

Because this is a static application, no server-side deployment configuration is required.

## Developer notes

The implementation uses a single `state` object to manage form values, themes, crew size, and logos. The primary functions in `index.html` include:

| Function | Responsibility |
| --- | --- |
| `loadState()` / `saveState()` | Read/write browser-local settings |
| `updateThemeUI()` | Apply appearance and card band colors |
| `renderInputs()` | Populate form inputs and crew-size visibility |
| `renderSheet()` | Build four cards from the HTML template |
| `syncStateFromInputs()` | Update state and refresh the preview |
| `setupEventListeners()` | Connect controls, printing, PDF export, and uploads |

### Known considerations

- The code currently retains a commented-out older PDF export handler; the active handler uses the date/team-based filename.
- The 3-person crew hides the Field Judge row while preserving its layout space.
- Uploaded images are stored as data URLs in browser storage.
- External PDF libraries are loaded via CDN.
- If a deployed page behaves differently from local code, verify the published branch, asset paths, and browser cache.

## Contributing

Issues and pull requests are welcome where repository permissions allow. For changes, test both crew sizes, both card colors, light/dark mode, print output, PDF filenames, and logo replacement/reset before submitting.

## License

No project license is specified here. Add a `LICENSE` file if you intend to grant reuse or redistribution rights. Association logos may be subject to their respective owners' usage requirements.
