# CT Transit Pass — Web Clone

A single-page web clone of the CT Transit mobile pass, built for a class project.
Demonstrates a live, animated transit ticket UI that runs entirely in the browser —
no build step, no server, no dependencies.

## Live Demo

**[Open on your phone →](https://jaimin001607.github.io/transit-ticket-app/)**

Works in mobile Safari, Chrome, and any modern browser.

## What It Does

- **Passes list** — tap a pass to activate it
- **Bottom-sheet reveal** — the active pass slides up over a dimmed list
- **Live ticking clock** — proves the ticket is not a screenshot
- **Pulsing pink ring** — outer disc grows and shrinks continuously around the logo,
  timing and geometry measured directly from the real CT Transit app
- **Dynamic expiration** — a 31-day pass computed as "today + 31 days" at page load,
  so the date is always fresh
- **Brightness boost** — requests the Screen Wake Lock and enters fullscreen on
  activation so the pass stays readable at max brightness

## File Structure

```
transit-ticket-app/
├── index.html      # the entire app, self-contained (HTML + CSS + JS + embedded logo)
├── pass-logo/
│   └── logo.png    # source logo (already embedded as base64 in index.html)
└── README.md
```

`index.html` has no external dependencies — the CT Transit logo is base64-embedded
inline, so the file works offline and hosts perfectly on GitHub Pages.

## Running Locally

Just open `index.html` in any browser. No install, no build.

```bash
open index.html
```

Or serve it with any static file server if you want the wake-lock / fullscreen APIs
to work (those require a proper origin):

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Notes on Brightness

A web page **cannot** directly control the hardware screen brightness — that's a
native-OS API (`UIScreen.brightness` on iOS). This clone gets as close as the web
platform allows:

1. **Wake Lock API** keeps the screen from auto-dimming while the pass is open
2. **Fullscreen API** hides the browser chrome for maximum screen real estate
3. **CSS `filter: brightness(1.08)`** slightly boosts perceived brightness

For true 100% hardware brightness like the real CT Transit app, the page would need
to be wrapped in a native shell (Capacitor, React Native, or a native iOS build).

## Built With

Plain HTML, CSS, and JavaScript. No frameworks, no build tools.
