# 🍫 Chocolate Rhythm

A lightweight, single-file web app for practicing **rhythm reading**. Place notes and rests on a musical staff, hear them played back, and get instant visual feedback on whether your measure adds up correctly.

It's not a full music notation editor — no key signatures, ties, chords, or export formats. The goal is simply to make it easy to build a short rhythmic phrase, see it notated correctly, and hear it, as a practice/teaching aid.

**Live demo:** https://damianribichescu.github.io/chocolate-rhythm/

---

## Features

**Notation**
- Treble or bass clef, switchable at any time (notes keep their staff position and are reinterpreted under the new clef, just like real notation)
- 1 or 2 measures (4/4 time), switchable on the fly
- Whole, half, quarter, eighth, and sixteenth notes and rests, plus a **dotted** modifier for any of them
- Sharps, flats, and naturals
- Automatic **beaming**: consecutive eighth/sixteenth notes of the same length beam together automatically, capped at 4 notes per beam group (standard notation practice)
- Live validation: each measure's beat total is checked and flagged (✓ complete / ⚠ short) as you build it

**Playback**
- Real synthesized audio via the Web Audio API — no audio files, works fully offline
- Adjustable tempo (40–208 BPM)
- Loop playback, with gapless looping (audio is scheduled precisely on the Web Audio clock, not via naive timers)
- Metronome click track with an accented downbeat, independent volume control
- **Swing** toggle with selectable intensity (60% / 70% / 80%), for practicing a swung eighth-note feel
- Independent volume sliders for notes vs. the metronome click

**Interface**
- Tap/click directly on the staff to place a note at a given pitch, or a rest; tap an existing note/rest to delete it
- Undo and clear-all controls
- Compact, icon-only control toolbar optimized for reachability on mobile, with a responsive layout that adapts to small/portrait screens
- Chocolate-themed Material Design styling (custom SVG icons, no external icon fonts required beyond Google Fonts for text/rest glyphs)

## Usage

1. Open the page (locally or via the hosted link).
2. Pick a clef and how many bars you want (1 or 2).
3. Optionally turn on **Dotted** and/or pick an accidental (♭ / ♮ / ♯) — these apply to the *next* note or rest you place, then reset automatically.
4. Pick a note or rest duration from the icon row, then tap the staff at the pitch you want (rests ignore vertical position).
5. Tap an existing note/rest to remove it, or use the undo/clear buttons.
6. Hit ▶ to hear it back. Toggle loop, metronome, and swing as needed, and adjust tempo/volume with the sliders.

## Running locally

This is a single self-contained HTML file — no build step, no dependencies to install, no server required.

```bash
git clone https://github.com/yourusername/chocolate-rhythm.git
cd chocolate-rhythm
open index.html   # or just double-click the file
```

It only relies on an internet connection for Google Fonts (Roboto + Material Symbols); everything else — layout, audio synthesis, notation rendering — runs entirely client-side.

## How it works

- **Staff rendering** is done with hand-drawn SVG (noteheads, stems, flags, beams, ledger lines) generated on the fly from the current composition state. Rests use the actual Unicode music-font glyphs rather than hand-drawn shapes, for notational accuracy.
- **Audio** uses the Web Audio API: each note is a triangle-wave oscillator with a simple attack/release envelope; the metronome click is a short square-wave blip. Playback timing is computed directly from the audio context's own clock rather than `setTimeout`-driven polling, which is what keeps looping and swing timing tight and gap-free.
- **No frameworks** — plain HTML, CSS, and vanilla JavaScript in one file.

## Browser support

Requires a modern browser with Web Audio API support (all current versions of Chrome, Firefox, Safari, and Edge, on both desktop and mobile). No Internet Explorer support.

## Known limitations

This app intentionally stays scoped to rhythm-reading practice rather than full notation authoring. It does not currently support: key signatures, time signatures other than 4/4, ties, tuplets, chords/multiple voices, MIDI/keyboard input, saving or exporting a composition, or instrument/timbre choices beyond the single synthesized tone.
