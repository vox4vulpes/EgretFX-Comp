# Egret Comp

**[Use it in your browser](https://vox4vulpes.github.io/EgretFX-Comp/)** ·
part of the [Egret FX Bundle](https://github.com/vox4vulpes/EgretFX)

白鳥 · Compressor, in the style of FabFilter Pro-C3: threshold, ratio, a soft
knee, attack and release, makeup gain and a dry/wet mix; seven **Style**
characters; an external **sidechain** with its own filter; **Lookahead**;
**Auto Release** and **Auto Gain**; stereo **Link**; a draggable
threshold/knee right on the curve; presets, undo/redo and A/B. It runs
entirely in the browser via the Web Audio API — no plugins, no install.
Open `index.html` in any modern browser.

See [CHANGELOG.md](CHANGELOG.md) for what's shipped. A VST3 plugin and
standalone app (matching [Egret EQ](https://github.com/vox4vulpes/EgretFX-EQ)'s
JUCE build) is next.

## How it works

The detector blends an instantaneous peak with a short RMS window — how much
of each depends on the **Style** (below). The knee is the standard
log-domain quadratic knee (in dB: flat below the threshold minus half the
knee width, the textbook ratio line above it, a smooth quadratic blend in
between — the same family described in academic references like
Giannoulis/Massberg/Reiss's *Digital Dynamic Range Compressor Design*,
implemented independently here). The attack and release times shape how
fast the gain-reduction *envelope* follows that target, not the detector
itself. Every knob glides into its new value over about 50 ms, so turning
them while the sound plays never clicks or zippers, and switching Style
fades through a brief silence rather than snapping, for the same reason.

## Controls

- **THRESH** — the level above which the compressor starts turning things
  down, −60 to 0 dB. Drag its dot right on the curve, or type a value.
- **RATIO** — how much: input dB above the knee turns into this many fewer
  output dB, 1:1 (off) to 20:1
- **KNEE** — how gradually the ratio kicks in around the threshold, 0 (hard)
  to 24 dB (soft). Drag its dot on the curve, just past the threshold.
- **ATTACK** / **RELEASE** — how fast gain reduction grabs and lets go
- **MAKEUP** — trims the output after compression, ±24 dB, or let **AUTO
  GAIN** work it out from the threshold and ratio
- **MIX** — blends the compressed signal back with the dry one; below 100%
  this is parallel ("New York style") compression
- **STYLE** — Clean, Classic, Opto, Vocal, Mastering, Bus or Punch: each is
  a different detector blend, knee behaviour and topology (feed-forward or
  feedback), not a separate algorithm — see the table below
- **RANGE** — caps how much gain reduction can happen, 0 to 60 dB
- **LOOKAHEAD** — delays the signal a little (up to 20 ms) so the detector
  catches a transient before it's heard, instead of just after
- **LINK** — how much the two channels' detectors are tied together, 0
  (independent) to 100% (both follow the louder one)
- **AUTO RELEASE** — blends in a program-dependent release (a fast and a
  slow stage, chosen by how long the sound's been loud) on top of RELEASE
- **SIDECHAIN** — the detector listens to another sound instead of the
  input (pick one in the player's Sidechain row), filtered by its own
  **HPF** and bell (**Freq**/**Gain**/**Q**); **LISTEN** auditions what the
  filter actually hears
- **BYPASS** — hear the source without the compressor
- **Source** (browser and standalone app) — a demo loop, a file (or drop one
  on the player), your microphone or line in, or pink noise; `Space` plays
- **Presets**, factory and your own; **UNDO**/**REDO** (`Ctrl+Z`,
  `Ctrl+Shift+Z`) and **A**/**B** to compare two settings

Click a knob's value to type one: `-18`, `4`, `6.5`.

### Style

| Style | Topology | Detector | Knee | Character |
|---|---|---|---|---|
| Clean | Feed-forward | mostly peak | as set | fully manual, the plain transfer curve |
| Classic | Feedback | RMS-leaning | widened | a little auto-release always blended in — vintage VCA glue |
| Opto | Feed-forward | strongly RMS | wide | attack floor, auto-release always on — an optical cell's slow, program-dependent response |
| Vocal | Feed-forward | peak-leaning | as set | catches sibilance quickly; sidechain bell defaults near 3 kHz |
| Mastering | Feed-forward | RMS-leaning | floored (gentle) | auto-release biased long, for already-mixed material |
| Bus | Feedback | RMS-leaning | widened | glue compression, slow program-dependent release |
| Punch | Feed-forward | mostly peak | tightened | attack floor lets the transient through before it bites |

## Display

One field, like Pro-C3's: a scrolling history of the last few seconds —
input level behind (filled, dim), output level in front (bright), the
clearest way to see how hard the compressor is actually working on the
sound right now — with the compressor's own input/output curve overlaid on
top (green). The meter on the right shows input and output level, and gain
reduction (GR) filling down from the top.

## Roadmap

A VST3 plugin and standalone app, matching
[Egret EQ](https://github.com/vox4vulpes/EgretFX-EQ)'s JUCE build.

## License

[GNU AGPLv3](LICENSE). Copyright (c) 2026 vox4vulpes
