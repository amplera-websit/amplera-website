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
| `index.html` | Home |
| `services.html` | Services (includes Who we serve + the case study) |
| `research.html` | Research & Innovation |
| `technology.html` | Technology |
| `about.html` | About |
| `contact.html` | Contact (branching enquiry form) |
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
Copy an existing page, replace the content between `<main>` and `</main>`, then add the link to the nav and footer of every page.

---

## Deploying

Drag this folder onto <https://app.netlify.com/drop> — you'll get a live URL in about a minute. Sign in first (free) so the site persists and you can redeploy after edits.

Cloudflare Pages works the same way.

---

## Contact form

The form on `contact.html` is wired for **Netlify Forms** — it works the moment you deploy to Netlify, with no extra setup:

- The `<form>` carries `data-netlify="true"` and a hidden `form-name` field, which is how Netlify detects it at deploy time.
- Submissions appear under **Site configuration → Forms** in your Netlify dashboard. Add your email under **Form notifications** to get them in your inbox.
- A hidden honeypot field (`bot-field`) catches most spam bots.
- It submits by AJAX, so the visitor stays on the page and sees an inline confirmation.
- Running locally it will **not** send — it shows "this will send for real once the site is deployed" instead, so you can test the validation without firing off real enquiries.

**Using a different host?** Change one attribute. For Formspark, Web3Forms or Basin, set the form's `action` to the endpoint they give you and remove `data-netlify="true"`.

---

## Still to do

- **Team photos** are not on the site yet.
- Institution names (Harvard Medical School, University of Hyderabad) appear as text, not logos — add logos only with permission.
- Consider adding `<meta name="robots" content="noindex">` while the site is a private draft, so it stays out of Google.
