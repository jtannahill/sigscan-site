---
version: alpha
name: SigScan Site
description: Single-page marketing site for the SigScan iPhone app, styled as a dark radar console with a live scan log.
colors:
  ink: "#050810"
  line: "#16223F"
  cyan: "#00CDEE"
  cyan-hover: "#33DBFF"
  green: "#35E07C"
  text: "#C7D3E8"
  text-strong: "#EDF3FF"
  dim: "#7A8AA8"
typography:
  sans:
    fontFamily: Space Grotesk
  mono:
    fontFamily: IBM Plex Mono
---

## Overview

SigScan is an iPhone app that shows nearby Bluetooth devices in augmented reality, flags unknown trackers and reads NFC, Wi-Fi and HomeKit details on the device. The marketing page presents it as a radar instrument: a full-bleed animated radar sweep behind the hero, and the feature list written as a terminal scan log where each row pairs a monospaced readout with a plain-language explanation.

## Colors

The page is dark only. `ink` is the single page background; there are no raised panels, and sections are separated by hairline rules in `line` rather than by surface changes.

Color carries meaning, so assign it by role:

- `cyan` marks what the reader can act on or what belongs to the instrument: links, the primary button fill, the ghost button outline, focus rings, the hero kicker and inline code. Primary buttons hover to `cyan-hover`; ghost buttons hover to a faint cyan wash, not a fill.
- `green` is reserved for signal readouts: the value line in each scan log meta column, the event count in section labels and the radar blips. Do not use it for links, buttons or decoration.
- `text-strong` is for headings only; body copy stays in `text`.
- `dim` is for secondary metadata: section labels, scan log meta lines, the ghosted second line of the hero headline and the footer. It was lifted to its current value so small monospaced labels stay legible on `ink`; do not darken it.

Text on a `cyan` fill uses `ink`.

The radar canvas draws with translucent versions of `cyan` (grid rings and sweep), `green` (blips) and `text` (blip labels). Keep canvas colors derived from these tokens so the illustration and the page read as one palette.

## Typography

`sans` (Space Grotesk) sets headings and body prose. `mono` (IBM Plex Mono) is the instrument voice: the hero kicker, section labels, scan log meta, buttons, inline code, radar labels and the footer. Any text that reads as data, a label or a control uses `mono`; any sentence meant to be read as explanation uses `sans`.

Monospaced labels are small, uppercase and widely tracked. Numeric readouts use tabular figures so values align down the log. Headings use balanced wrapping and prose uses pretty wrapping; prose is capped at a comfortable measure rather than spanning the full content width.

## Layout

Content sits in a single centered column with a fixed maximum width and a side gutter on all viewports. The hero fills most of the first viewport, with copy on the left and the radar centered toward the right edge so blips and labels do not collide with the headline.

Each feature is a scan log row: a narrow meta column (category, green readout, qualifier) beside the heading and paragraph, with hairline rules between rows. Below the mobile breakpoint the row collapses to one column and the meta line flattens to a single wrapped line. Radar blip labels are drawn only on wide viewports and only where they fit inside the canvas.

## Shapes

Corners are nearly square. Buttons and focus rings use a small radius; nothing on the page is pill-shaped or heavily rounded, which keeps the console character.

## Components

- **Primary action**: the App Store badge. Hover dims its opacity; press scales it down slightly.
- **Secondary action**: the ghost button, `mono` text in `cyan` with a `cyan` outline and a transparent fill. A filled `cyan` button with `ink` text is the variant for a primary action that is not the App Store badge.
- **Scan log row**: the pattern for any new feature entry. Every row needs all three meta lines, with only the middle line in `green`.
- **Section label**: an `h2` styled as a small `mono` label in `dim`, optionally ending in a `green` count.

## Motion

Motion is limited to the radar sweep and short press and hover feedback on actions. The sweep runs at the same speed regardless of display refresh rate and stops repainting when the hero scrolls out of view. Hover effects apply only on devices that support hover.

When the viewer prefers reduced motion, the radar is drawn once as a static frame with no sweep and evenly lit blips, and it redraws only on resize or font load. Any new animation must honor the same preference.
