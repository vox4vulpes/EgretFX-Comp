# Egret Comp

**[Use it in your browser](https://vox4vulpes.github.io/EgretFX-Comp/)** ·
part of the [Egret FX Bundle](https://github.com/vox4vulpes/EgretFX)

翡翠 · Compressor, in the style of FabFilter Pro-C3: threshold, ratio, a soft
knee, attack and release, makeup gain and a dry/wet mix, with a live
transfer-curve display and a gain-reduction meter. It runs entirely in the
browser via the Web Audio API — no plugins, no install. Open `index.html` in
any modern browser.

This is an early (0.1.x) release: the core compressor is real and playable,
but it's not yet close to Pro-C3's full feature set. See
[Roadmap](#roadmap) below for what's coming, and
[CHANGELOG.md](CHANGELOG.md) for what's shipped so far.

## How it works

The detector blends the instantaneous peak with a short (~10 ms) RMS window,
so it reacts to transients without being fooled by a single sample. The
knee is the standard log-domain quadratic knee (in dB: flat below the
threshold minus half the knee width, the textbook ratio line above it, a
smooth quadratic blend in between — the same family described in academic
references like Giannoulis/Massberg/Reiss's *Digital Dynamic Range
Compressor Design*, implemented independently here). The attack and
release times shape how fast the gain-reduction *envelope* follows that
target — not the detector itself — which is what gives a compressor its
character. Every knob glides into its new value over about 50 ms, so
turning them while the sound plays never clicks or zippers.

## Controls

- **THRESH** — the level above which the compressor starts turning things
  down, −60 to 0 dB
- **RATIO** — how much: input dB above the knee turns into this many fewer
  output dB, 1:1 (off) to 20:1
- **KNEE** — how gradually the ratio kicks in around the threshold, 0 (hard)
  to 24 dB (soft)
- **ATTACK** / **RELEASE** — how fast gain reduction grabs and lets go,
  0.1 ms to 300 ms / 20 ms to 3 s
- **MAKEUP** — trims the output after compression, ±24 dB
- **MIX** — blends the compressed signal back with the dry one; below 100%
  this is parallel ("New York style") compression
- **BYPASS** — hear the source without the compressor
- **Source** (browser and standalone app) — a demo loop, a file (or drop one
  on the player), your microphone or line in, or pink noise; `Space` plays

Click a knob's value to type one: `-18`, `4`, `6.5`.

## Display

One field, like Pro-C3's: a scrolling history of the last few seconds —
input level behind (filled, dim), output level in front (bright), the
clearest way to see how hard the compressor is actually working on the
sound right now — with the compressor's own input/output curve overlaid on
top (green), the threshold marked on it. The meter on the right shows
input and output level, and gain reduction (GR) filling down from the top.

## Roadmap

Planned next, roughly in order: a draggable threshold/knee on the curve
itself; seven FabFilter-style **Style** modes (Clean, Classic, Opto, Vocal,
Mastering, Bus, Punch) that change the detector and topology; an external
**sidechain** input with its own high-pass/bell filter; **Lookahead**;
**Auto Release** (program-dependent) and **Auto Gain**; stereo **Link**;
factory presets with undo/redo and A/B; and a VST3 plugin and standalone
app (JUCE, matching the [Egret EQ](https://github.com/vox4vulpes/EgretFX-EQ)
plugin's build).

## License

[GNU AGPLv3](LICENSE). Copyright (c) 2026 vox4vulpes
