# designverse
# DesignVerse 2026 — landing page

A landing page for **DesignVerse**, a fictional two-day Student Design & Innovation Fest, built for the Nirvana (IGDTUW) website task. The page explains the event, shows the schedule and gets students to register.

**Live site:** _add your deployment link here_ (see [Deploy](#deploy))

## What's on the page

| Section | Content |
| --- | --- |
| Hero | Event name, one-line introduction, date, time, venue, two calls to action |
| About | What the fest is, who can come, what it costs, what to bring, what you take home |
| Highlights | Six activities, each shown as an "artboard" on the canvas |
| Schedule | Day-by-day timeline with tabs |
| Register | Countdown to doors opening and a registration form that issues a ticket |
| Footer | Date, venue, contact, social links, page navigation |

## Technologies used

- **HTML5** — semantic landmarks (`header`, `main`, `section`, `footer`), ARIA for the menu, tabs and form errors
- **CSS3** — custom properties (design tokens), Grid and Flexbox, `clamp()` type scale, keyframe animations, `prefers-reduced-motion`
- **Vanilla JavaScript (ES2015+)** — no frameworks, no build step; the hero scene is drawn with the Canvas 2D API
- **Google Fonts** — [Cormorant Garamond](https://fonts.google.com/specimen/Cormorant+Garamond) (display) and [Jost](https://fonts.google.com/specimen/Jost) (body)

No dependencies, no bundler. Open the HTML file and it runs.

## Functional interactions

1. **Navigation menu** — a fixed header with a hamburger that opens a full-screen menu with oversized links and the event facts; the link for the section in view is highlighted (IntersectionObserver); Escape closes it and focus returns to the button.
2. **Interactive schedule** — Day 1 / Day 2 tabs with full keyboard support (arrow keys, Home, End), built on the WAI-ARIA tabs pattern.
3. **Registration form** — client-side validation with inline error messages, then a ticket with a generated registration ID, the chosen tracks and an "Add to Google Calendar" link. "Register someone else" resets the form.
4. **Live countdown** — days, hours, minutes and seconds to doors opening.
5. **Generated scene** — the hero artwork is not an image. The sky is a gradient with value-noise (fBm) haze and cloud bands rendered live on a `<canvas>` at low resolution and screened over it; the moon is a gradient disc with a noise texture; the ridges are 1D noise silhouettes in three layers of atmospheric perspective; the water is the sky copied upside down in thin slices with sinusoidal ripple offsets, with a glitter path under the moon; birds flap across on quadratic curves; stars twinkle and lanterns rise. It is drawn once and left still under `prefers-reduced-motion`, and it pauses when scrolled out of view.
6. **Fireflies** — three named lights drift across the sky, and a gold "You" firefly follows your pointer across the scene (mouse only). The wordmark's reflection shimmers.
7. **Ticker** — a scrolling strip of the six tracks between the hero and the about section; pauses on hover.

## Design decisions

**Concept.** The name is taken literally: DesignVerse is a quiet, surreal universe. The hero is a nocturne painted live in code: a twilight sky that runs from deep indigo to a rose-violet horizon with drifting haze and moonlit cloud bands, a giant cream moon with a mottled surface against the cool sky, misty mountain ridges fading into the distance, a still horizon that mirrors the whole scene in slowly rippling water with the moon's path glittering across it, a band of mist on the water line, a small flight of birds crossing the sky, and lanterns and motes of gold light rising through the frame. The wordmark stands on the water line with its own reflection shimmering beneath it, vertical taglines run along both edges, and other students appear as named fireflies drifting across the sky (one follows your pointer). The event panel floats over the scene as frosted glass with a tracked eyebrow, a two-weight serif title, the facts stacked and the call to action. Everything below is glass, hairlines and glow on midnight, with a fine film grain over the whole page. The direction takes its cues from the Nirvana site (dark, cinematic, vertical type, big wordmark) without reusing any of its artwork.

**Hierarchy and layout.** The hero holds everything a student needs to decide (what, when, where, register) before any scrolling: the scene fills the frame and the information sits in one glass panel on the right, which drops below the scene on phones. Below it, one left-aligned column, 1120px wide, generous vertical space, and the only boxed elements are the ones that behave like objects: the fact tiles, the highlight panels, the form and the ticket, all rendered as glass.

**Typography.** Cormorant Garamond at light weight for the wordmark, headings, countdown and timeline titles: a high-contrast serif whose italic carries the mood, used for the second line of each heading and the "Verse" in the wordmark. Jost, a light geometric sans, for body copy and controls, with tracked uppercase for the small labels. The scale is fluid (`clamp()`), so the wordmark runs from about 150px on desktop to 52px on a phone.

**Colour.** Midnight with a blue-violet bias, pale lavender-white ink, and six luminous pastels (lavender, periwinkle, rose, aqua, peach, pale gold) that glow rather than sit flat, used for the fireflies, panel blooms, tile dots and schedule tracks. The call to action is the one iridescent element, a rose-to-lavender-to-aqua gradient with a soft halo, so "register" always reads as the brightest thing nearby. Hairlines are white at low opacity rather than grey, which keeps edges light. The sky and the moon are tuned to the same family so scene and interface never fight.

**Motion.** Everything is slow. One orchestrated moment on load (the wordmark fades in, the panel rises), ambient loops that are easy to ignore (the haze drifts, the water ripples, stars twinkle, motes rise, the ticker glides), and micro-interactions that answer the user (panels lift and bloom on hover, menu links slip into italic, the "You" firefly follows the pointer). Everything is switched off under `prefers-reduced-motion`.

**Responsive.** The hero stacks under 820px (scene on top, the glass panel overlapping its lower edge) and the horizon line moves with it; grids collapse from three columns to two to one; timeline rows and form rows stack under 600px; extra cursors and the vertical taglines are hidden on small screens; the ticket's stub moves from the side to the bottom.

**Accessibility.** Skip link, visible focus states, labelled form controls with `aria-describedby` errors, `aria-expanded` on the menu button, tabs with roving tabindex, the scene, reflection and fireflies hidden from assistive tech, `prefers-reduced-motion` respected throughout.

## Project structure

```
designverse/
├── index.html          # all content
├── css/style.css       # tokens, layout, components, responsive rules
├── js/main.js          # menu, active link, dimension label, cursor tag, tabs, countdown, form
├── assets/favicon.svg
├── README.md
└── VIDEO_SCRIPT.md     # 1-minute walkthrough script
```

## Run locally

Clone the repository and open `index.html` in a browser. That's it.

For a local server (recommended so fonts and relative paths behave exactly as on the live site):

```bash
# Python 3
python -m http.server 8000
# or Node
npx serve .
```

Then visit `http://localhost:8000`.

## Deploy

The site is static, so any static host works.

- **Vercel:** import the GitHub repo at vercel.com/new, leave the framework as "Other", deploy. No build command, output directory is the repo root.
- **Netlify:** drag the folder onto app.netlify.com/drop, or connect the repo with no build command and publish directory `/`.
- **GitHub Pages:** repo Settings → Pages → Source: "Deploy from a branch" → branch `main`, folder `/ (root)`.

## Customising

- Event date and time: `EVENT_START` at the top of `js/main.js`, the `<time>` elements in the hero, the schedule tabs, the ticket and the footer in `index.html`, and the `dates=` parameter in the Google Calendar link.
- Colours and fonts: the `:root` block at the top of `css/style.css`. The six pastels are `--lavender`, `--periwinkle`, `--rose`, `--aqua`, `--peach` and `--gold`; the call-to-action gradient is `--signal-grad`.
- Horizon line: the `--horizon` custom property on `.hero-art` in `css/style.css` (64% on desktop, 68% on phones); the canvas reads it, so the wordmark and the water always meet.
- Sky colours and the moon: `paintSky` and `drawMoon` in `js/main.js`; the numbers there set the hue balance and the moon's size and position.
- Activities and schedule: edit the `.artboards` list and the two `.timeline` lists in `index.html`.

## Connecting the form to a real backend

The form currently validates in the browser and shows a ticket; nothing is sent anywhere. To collect registrations, post the form data from the `submit` handler in `js/main.js` to a service such as [Formspree](https://formspree.io), [Getform](https://getform.io), a Google Apps Script web app writing to a Sheet, or your own API, and show the ticket only after the request succeeds.

## Credits

Designed and built by Harshit Pal. Fonts by Google Fonts. Inspiration: the [Nirvana website](https://nirvanaigdtuw.vercel.app/).
