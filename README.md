# Amplera Biosciences — website

Static site. Plain HTML, CSS and a little vanilla JavaScript. **No build step, no dependencies, nothing to install.**

---

## Run it locally

Pick whichever you like — all three do the same thing.

### 1. Live Server (best for editing)
Install the **Live Server** extension (VS Code will offer it when you open this folder), then right-click `index.html` → **Open with Live Server**.
The browser reloads automatically every time you save. Runs on <http://localhost:5500>.

### 2. One key in VS Code
Press **Ctrl + Shift + B** (**Cmd + Shift + B** on Mac).
That runs the "Serve site (Python)" task. Then open <http://localhost:8000>.
Stop it with **Ctrl + C** in the terminal panel.

### 3. Terminal
Open the terminal with **Ctrl + `** (**Cmd + `** on Mac) and run:

```bash
python3 -m http.server 8000     # Mac / Linux
python -m http.server 8000      # Windows
```

or, if you prefer Node:

```bash
npm start
```

Then visit <http://localhost:8000>.

> You can also just double-click `index.html` — it works over `file://`. A local server is still worth it because it behaves exactly like the deployed site.

**If the page looks like plain unstyled text**, you're running from the wrong folder. Run the command from the directory that contains `index.html` and `styles.css`. Check with `ls` (or `dir` on Windows).

---

## What's in here

| File | What it is |
|---|---|
| `index.html` | Home (`/`) |
| `services/index.html` | Services — `/services/` (includes Who we serve + the case study) |
| `research/index.html` | Research & Innovation — `/research/` |
| `technology/index.html` | Technology — `/technology/` |
| `about/index.html` | About — `/about/` |
| `contact/index.html` | Contact (branching enquiry form) — `/contact/` |

Each inner page lives in its own folder as `index.html` so the URL has no `.html` extension (`amplera.bio/services/` instead of `amplera.bio/services.html`). The old flat `about.html`, `services.html`, `research.html`, `technology.html` and `contact.html` files still exist at the root as thin redirect stubs, so any old bookmark or indexed link forwards to the new clean URL instead of 404ing.
| `styles.css` | **All** styling, including the colour tokens |
| `amplera-logo-white.svg` | Logo used in the nav and footer |
| `amplera-logo-white-lower.svg` | Lowercase "amplera" alternative |
| `amplera-logo-dark.svg` | Logo for light backgrounds |
| `amplera-mark.svg` | The mark on its own |
| `amplera-favicon-*.png` | Favicon / Apple touch icon |
| `amplera-hero-graphic.svg` | Standalone hero curve graphic |

Each page has its JavaScript inline at the bottom: sticky-nav shading, the mobile menu, scroll reveals, and (on Contact) the form branching.

---

## Editing

### Colours
Everything is driven by CSS variables at the top of `styles.css`. Change one value and it updates across all six pages:

```css
:root{
  --lab-black:#0B140F;   /* dark section background */
  --paper:#F6F8F3;       /* light section background */
  --sybr:#3DE07A;        /* primary accent */
  --teal:#00D9A5;
  --emerald:#0EA968;
  /* ... */
}
```

The signal gradient is `linear-gradient(103deg, #0EA968, #3DE07A 52%, #00D9A5)`.

### Text
Open the relevant `.html` file and edit between the tags. The nav and footer are repeated on each page, so if you change a nav link, change it in all six.

### Adding a page
Create a new folder with an `index.html` inside (e.g. `pricing/index.html`) so it gets a clean `/pricing/` URL, copy an existing page's structure into it, replace the content between `<main>` and `</main>`, then add the link (`/pricing/`) to the nav and footer of every page. Since the file is one level down from the root, its asset links (`styles.css`, `favicon.ico`, etc.) and its logo `src` need a leading `/` (e.g. `href="/styles.css"`) — copy that pattern from an existing inner page like `about/index.html`, not from the root `index.html`.

---

## Deploying

This site is deployed via **GitHub Pages**, with a custom domain (`amplera.bio`) set by the `CNAME` file at the root. Deploying is just:

```bash
git add -A
git commit -m "your change"
git push origin main
```

GitHub rebuilds and republishes automatically within a minute or two of a push to `main`. No Netlify/Cloudflare account is involved — the `_redirects` file in this repo is inert on GitHub Pages (it's Netlify/Cloudflare-only syntax) and only matters if the site is ever moved to one of those hosts.

---

## Contact form

The form on `contact/index.html` submits via **FormSubmit.co** (no account/API key needed — just an email address):

- The email it sends to is set in one place: the `CONTACT_EMAIL` constant near the top of the `<script>` block at the bottom of `contact/index.html`.
- The **first submission** after the inbox goes live triggers a one-time "Activate Form" confirmation email from FormSubmit to that address — someone needs to click it once. Every submission after that lands directly in the inbox.
- A hidden honeypot field (`_honey`) catches most spam bots; `_captcha` is disabled since the AJAX flow already has its own validation.
- It submits by `fetch()`, so the visitor stays on the page and sees an inline confirmation.
- Until `CONTACT_EMAIL` is changed from its placeholder, or when running locally, submitting just shows "this will send for real once the site is deployed and the inbox is connected" — so you can test the validation without needing a live inbox yet.

**Using a different service?** Swap the `fetch()` target in that same script block for whatever endpoint your provider (Web3Forms, Formspree, Basin, etc.) gives you.

---

## Still to do

- **Team photos** are not on the site yet.
- Institution names (Harvard Medical School, University of Hyderabad) appear as text, not logos — add logos only with permission.
- Consider adding `<meta name="robots" content="noindex">` while the site is a private draft, so it stays out of Google.
