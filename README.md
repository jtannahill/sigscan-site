# sigscan-site

Static marketing page for SigScan, the iPhone app listed on the App Store as
[SigScan: Signal Radar](https://apps.apple.com/app/sigscan-signal-radar/id6806315838)
(id6806315838).

Live: https://jtannahill.github.io/sigscan-site/

## Preview locally

There is no build step and no test suite. GitHub Pages serves the site under `/sigscan-site/`, and `404.html` uses URLs absolute to that path, so serve the parent folder:

```sh
cd .. && python3 -m http.server 8000
# then open http://localhost:8000/sigscan-site/ (and /sigscan-site/missing for the 404 page)
```

## Deploy

GitHub Pages serves the repo from `main`. Pushing to `main` publishes the site.

## Files

- `index.html`: the whole page, with inline CSS (color tokens on `:root`) and an inline script that draws the radar on a canvas.
- `app-store-badge.svg`: the official Apple App Store badge used in the hero.
- `icon.svg`: favicon.
- `apple-touch-icon.png`: 180px home screen icon rendered from `icon.svg` on `ink`.
- `og.png`: 1200x630 social card (ink background, wordmark, hero headline, radar), generated with Pillow from the self-hosted fonts.
- `fonts/`: self-hosted Latin subsets of Space Grotesk (variable) and IBM Plex Mono 400/500/600, with `fonts/LICENSE` (SIL OFL 1.1).
- `404.html`: branded not-found page served by GitHub Pages for any missing path.
- `DESIGN.md`: colors, type, layout and motion rules. Read it before changing the page: [DESIGN.md](DESIGN.md).

## Notes

- **Radar motion.** The beam turns clockwise with a hard leading edge and a trail fading behind it; blips flare as the beam passes and then fade. With `prefers-reduced-motion: reduce` (read live, not only at load) the radar draws one static frame. Otherwise the sweep runs frame-rate independent (same speed at 60Hz and 120Hz), stops repainting when the hero scrolls off screen, and has a visible Pause radar control. A ResizeObserver redraws the canvas on any size change, including while paused.
- **Radar labels** draw only on wide screens (900px and up) and only where they fit inside the canvas.
- **Metadata.** The head carries a canonical URL, Open Graph and Twitter card tags, and a `MobileApplication` JSON-LD block. `og:image` and `twitter:image` point at this site's own `og.png` (absolute URL, as the scrapers require). Keep the JSON-LD facts (name, iOS version, category, price, App Store URL) in sync with the App Store listing.
- **Claims must match the app.** Bluetooth devices are shown in AR. Wi-Fi, cellular, NFC and HomeKit details are shown in the app, not in AR. Wi-Fi covers the joined network only. Scans are stored on the device. The only thing sent anywhere is an Ask AI question, and only when the user asks one: the question, a summary of up to 20 devices (make, model, signal type, category, silicon, average RSSI, seen count, risk flags, evidence, moving flag, location-point count) and the last 30 events with name, time and RSSI. In 1.3 those events also carry the latitude and longitude where they were logged (`SigScanML.swift` in the 1.3 build); 1.4 drops them (commit 3e758a0 in the app repo). Keep this paragraph and the page's Privacy section in step with `SigMLEngine.query` in `~/SigScan/SigScanML.swift`.
- **Counts are generated, not typed.** The product count is the number of distinct products in `~/SigScan/tools/products/switchbot.yaml` and `xiaomi.yaml`, not the number of keys (SwitchBot lists most products under two keys). Recount when the tables change.
- **Shipped features only.** Describe what the App Store version does. Check `https://itunes.apple.com/lookup?id=6806315838` before describing a new version's features.
- House style: no em-dashes and no emojis in copy.

## Restore when 1.4 ships

The page describes the App Store version, which is 1.3 as of October 1, 2026. Three pieces of 1.4 copy are kept in `index.html` as HTML comments marked `Restore when 1.4 ships` (`grep -n "Restore when 1.4" index.html`). Once the lookup above reports 1.4:

1. Uncomment the SHARE scan log row (sharing, widget, tab customisation, appearance) and change the section count from `11 events` to `12 events`.
2. Uncomment the device-class sentences at the end of the TRACE row paragraph.
3. In the Privacy section, replace "In version 1.3, those events also include the coordinates where they were logged." with "Never your location.", and update the Claims note above.

## License

The page source is MIT, see [LICENSE](LICENSE). The fonts in `fonts/` are under the SIL Open Font License 1.1 (`fonts/LICENSE`), and the App Store badge and Apple marks belong to Apple.
