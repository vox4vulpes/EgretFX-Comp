# Changelog

## [0.2.0]

### Added
- Seven **Style** characters (Clean, Classic, Opto, Vocal, Mastering, Bus,
  Punch): each its own detector blend, knee behaviour and feed-forward or
  feedback topology, switched with a click-free crossfade.
- A draggable threshold and knee, right on the curve.
- **Range**, **Lookahead** (with real latency reporting), stereo **Link**.
- **Auto Release** (program-dependent) and **Auto Gain**.
- An external **Sidechain** input (pick a source in the player) with its
  own high-pass + bell filter and a **Listen** audition.
- Factory presets, **Undo**/**Redo** and **A**/**B**.
- The egret mascot: now a swan (白鳥), with its own curled-neck icon.

### Fixed
- The sidechain filter's own frequency/gain/Q knobs weren't reaching the
  engine (only their defaults were ever used).
- Auto Gain's sign was backwards — it was quietening the output instead of
  compensating for lost loudness.

## [0.1.0]

### Added
- The core compressor: threshold, ratio, a soft knee, attack, release,
  makeup gain and a dry/wet mix, running in the browser via an
  AudioWorklet.
- A Pro-C3-style main display, one field: a scrolling history of input
  and output level with the transfer curve overlaid on it (threshold
  marked), and a meter showing input, output and gain reduction.
- Bypass, light/dark theme, fullscreen.
- The test player: a demo loop, your own file, microphone/line input, pink
  noise, and a track list from `music/playlist.json`.
