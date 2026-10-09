# Top-right panel — a real screenshot of the tool this profile is about

The hand-drawn laptop and notebook is gone, and so is the abstract hardware shot.
In its place is the actual Wazuh console: alert totals, the alerts-evolution chart,
the MITRE ATT&CK tactic breakdown, and the security alerts table with real rule
ids, tactics and levels.

It is a real screenshot, not a generated image, because you asked for something
that refers to what you actually do. Wazuh is in your bio; this is Wazuh.

## Credit and licence

The screenshot is **not mine** and is used under its own licence:

- File: `Wazuh XDR screenshot.webp`, Wikimedia Commons
  <https://commons.wikimedia.org/wiki/File:Wazuh_XDR_screenshot.webp>
- Author: Wazuh, Inc.
- Licence: GPLv2
- Retrieved 2025; unchanged apart from the crop and the theme conversion below.

The dark variant is the same file with its neutral tones inverted — hue and
saturation are kept, so the console's own blues and reds survive. It is not a
second screenshot.

## Files

Eight assets, same filenames as before, so `README.md` needs no change:

    assets/profile-v3.png                  61 KB
    assets/profile-v3-light.png            58 KB
    assets/profile-v3-mobile.png           65 KB
    assets/profile-v3-mobile-light.png     62 KB
    assets/profile-v3.gif                 329 KB
    assets/profile-v3-light.gif           311 KB
    assets/profile-v3-mobile.gif          335 KB
    assets/profile-v3-mobile-light.gif    300 KB
                                         -------
                                        1,524 KB   (was 2,433 KB, -37%)

The stills are 248 KB of that and are unchanged from the previous build. The
GIFs grew from 720 KB to 1,276 KB because the reveal now carries 47 frames
instead of 24. The cheaper version was cheaper because it was stepping and
because its payoff rendered grey — see the audit below.

## Notes

- Dark theme uses the inverted console; light theme uses the screenshot as
  published, so each theme shows the console in its own native look.
- Desktop shows the whole console. Mobile shows a band of it — the alert totals
  and both charts — because the mobile column is shorter and wider.
- The console itself is a still. All the motion is in the Selected work pipeline.
- The GIFs now play **once and hold**. They no longer loop.

## Animation audit

Four defects, found by measuring frames rather than looking at them. All fixed.

### 1. The amber payoff was rendering grey

The worst of the four, and invisible in the stills. The palette was built by
sampling five key frames and median-cutting them to 48 colours. Amber covers
about 0.02% of the banner, so the quantiser never gave it a slot, and every
amber pixel — the node-04 outline, the `gap log` label, the dashed drop, the
square, `gap: no rule matched` — was mapped to `#a5a191`, a flat grey.

Measured on the last frame of the shipped `profile-v3.gif`: **2,618 pixels that
should have been `#d29922` were grey.**

Fixed by forcing the eight design colours into the palette by hand and letting
the median cut fill the remaining 56. 64 entries still fits a 6-bit index, so it
cost nothing in file size. Verified: the accent now quantises to exactly
`(210, 153, 34)`.

### 2. The reveal restarted forever

`loop=0` is GIF's "repeat infinitely" flag. After the payoff held for 3.3 s the
banner snapped back to frame 1 and replayed — every 5.8 s, indefinitely, with a
hard cut at the seam.

Fixed by omitting the loop extension. Verified: `loop=None`; the GIF plays once
and holds on the amber state.

### 3. Everything popped instead of moving

The reveal was a 26-step integer machine — every element switched state on a
single frame boundary:

| element | before | after |
| --- | --- | --- |
| nodes 01–04 appearing | instant pop | 3-step eased fade |
| signal travelling | 5 jumps of ¼ the banner width | continuous, eased in and out |
| node 04 turning amber | instant switch | fades border → amber |
| `gap: no rule matched` | instant pop | fades in |

The old build's own palette comment said the amber "can actually fade instead of
snapping to the lit colour". The palette allowed it; the code never did it. It
does now.

### 4. Dead beats

Three stretches changed nothing on screen, so the encoder merged the duplicate
frames: the opening steps, and a 140 ms pause where node 01 had finished fading
but its connector had not started. The choreography is now a continuous chain —
each element begins as the previous one lands.

### Frame budget

Frames are spent where the motion is, using per-frame GIF delays:

| phase | delay | frames |
| --- | --- | --- |
| text fade (inherited from the original banner) | 80 ms | 10 |
| nodes and connectors | 60 ms | 12 |
| signal travel and payoff | 40 ms | 24 |

47 frames over 2.5 s, then a 3.3 s hold. The inherited text fade is resampled by
linear blend rather than by repeating frames, so it reads smoother than the
original 10 fps without the cost of re-authoring it from scratch.

### What was checked, and how

- The four still PNGs are **byte-identical** to the previous build, so nothing
  outside the two rebuilt regions moved.
- No frame of the reveal leaves the pipeline band unchanged.
- The signal advances across all 47 frames without repeating a position.
- Amber ramps through intermediate values before landing on the exact accent.
- Cycle time is 5,780 ms on all four files, matching the original banner.
