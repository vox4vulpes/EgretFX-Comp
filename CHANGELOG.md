# Changelog

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
