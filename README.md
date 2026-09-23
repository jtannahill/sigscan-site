# sigscan-site

Static marketing page for SigScan, the iPhone app listed on the App Store as
[SigScan: Signal Radar](https://apps.apple.com/app/sigscan-signal-radar/id6806315838)
(id6806315838).

Live: https://jtannahill.github.io/sigscan-site/

## Preview locally

There is no build step and no test suite. Serve the folder and open the page:

```sh
python3 -m http.server 8000
# then open http://localhost:8000/
```

## Deploy

GitHub Pages serves the repo from `main`. Pushing to `main` publishes the site.

## Files

- `index.html`: the whole page, with inline CSS (color tokens on `:root`) and an inline script that draws the radar on a canvas.
- `app-store-badge.svg`: the official Apple App Store badge used in the hero.
- `icon.svg`: favicon.
- `DESIGN.md`: colors, type, layout and motion rules. Read it before changing the page: [DESIGN.md](DESIGN.md).

## Notes

- **Radar motion.** With `prefers-reduced-motion: reduce` the radar draws one static frame and redraws only on resize or font load. Otherwise the sweep runs frame-rate independent (same speed at 60Hz and 120Hz), stops repainting when the hero scrolls off screen, and has a visible Pause radar control.
- **Radar labels** draw only on wide screens (900px and up) and only where they fit inside the canvas.
- **Metadata.** The head carries a canonical URL, Open Graph and Twitter card tags, and a `MobileApplication` JSON-LD block. `og:image` and `twitter:image` reuse `https://jamestannahill.com/og-venture-sigscan.png?v=2`. Keep the JSON-LD facts (name, iOS version, category, price, App Store URL) in sync with the App Store listing.
- **Claims must match the app.** Bluetooth devices are shown in AR. Wi-Fi, cellular, NFC and HomeKit details are shown in the app, not in AR. Wi-Fi covers the joined network only. Scans stay on the device; the only thing sent anywhere is an Ask AI question with a short summary of scanned device names.
- House style: no em-dashes and no emojis in copy.
