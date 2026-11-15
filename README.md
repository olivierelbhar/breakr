# BREAKR

**A beat slicer for your browser. Chop a drum break into pieces, then put the pieces back in the wrong order, on purpose.**

People have been doing this to the same six seconds of drumming since roughly 1989, with excellent results and very little remorse. BREAKR lets you join in without buying a sampler, reading an 800-page manual, or explaining to anyone why you need a third drum machine.

> **Live demo:** _add your GitHub Pages link here_

---

## What it does

You load a drum loop. BREAKR cuts it into slices. You play the slices from your keyboard, rearrange them on a step sequencer, and let a modest amount of controlled chaos improve things. That's it. That's the whole idea, and it's served the jungle community for over thirty years, so we saw no reason to complicate it.

It's a single HTML file. Nothing is installed, nothing is uploaded, and your audio never leaves your machine. Frankly, it has better manners than most websites.

## Features

### Slicing
- **Three ways to cut:**
  - **Grid** cuts into equal slices: 6, 8, 16, 32, 64 or 128 of them.
  - **Transient** cuts on the hits themselves.
  - **Manual** leaves the cutting to you.
- **Sensitivity** sets how fussy Transient mode is. Turn it down and only the big hits get their own slice. Turn it up and every ghost note gets one too, which some ghost notes absolutely do not deserve.
- **Hand-placed cuts:**
  - Double-click the waveform to add a cut. It snaps to the nearest hit, because we assume you meant to.
  - Hold Shift to place a cut exactly where you clicked, if you insist.
  - Right-click a flag to remove it. Drag a flag to move it.
- **Gate or Thru playback.** Gate stops each slice at its cut, for a clipped, slightly nervous feel. Thru lets each slice run on until the next hit, so empty steps don't turn into awkward silences.
- **Warp as 1, 2 or 4 bars.** Tell BREAKR how long your loop is and it works out the original tempo. Then set your own. Speeding a break up raises its pitch, as tradition demands, and that's the entire sound of 1994.

### Pads
- One pad per slice. Play them with the keys shown, either AZERTY or QWERTY, since we're not here to judge.
- Drag a pad onto another to swap their sounds, or onto a step to place it in the sequence. **Reset order** puts everything back if your rearrangement goes the way most rearrangements go.

### Per-slice effects
Each slice gets its own small toolkit:
- **Transp**: ±12 semitones.
- **Volume**: for the slices that need humbling.
- **Delay**: an echo locked to the tempo.
- **Reverb**: about two seconds of room tone, for a slice that wants to sound expensive.
- **Stretch**: 25–400 %, longer or shorter without changing pitch. Proper time-stretching (WSOLA, if you must know), not just playing it slowly and hoping.
- **Reverse**: the classic.
- **Random FX**: rolls the dice on pitch, delay, reverb and stretch. Musically sensible intervals only, so nothing ends up a quarter-tone flat by accident.
- **FX each hit**: new random effects every time the slice plays. Use with care, or don't, as the case may be.

### Sequencer
- 16, 32 or 64 steps.
- **Original** plays the whole file exactly as recorded, every slice at its true position. Useful for reminding yourself what it sounded like before you got involved.
- **Random** rewrites the pattern starting from the original. **Mutate** rewrites whatever is there now, so it drifts a bit further with each click. **Variation** sets how drastic either one is.
- **Clear** starts again. No hard feelings.

### Live Random
An improviser that plays along while you play, without ever touching your steps.
- **Chance** sets how often it intervenes.
- **Moves** sets how:
  - **Swap** plays another slice.
  - **Roll** repeats the hit 2 to 4 times inside one step.
  - **Skip** drops the hit.
  - **Fill** adds a hit on an empty step.
- **Choices**, **Scale**, **Mode** and **Sign** fine-tune the swaps, along the lines of a well-known random MIDI device.
- Every step it changes gets a dashed outline, and a counter keeps score. Nothing is hidden. We are not that sort of software.

### Skins
- **Mono**, the default, in tasteful black and white.
- **Tracker**: beige and green, like the samplers of 1993.
- **Phosphor**: green-on-black, for anyone who misses squinting.
- **Paper**: for people who work in daylight.

## Keyboard

| Key | Does |
| --- | --- |
| `Space` | Play / stop |
| `1`–`8`, top three letter rows | Play slices 1–32 |
| Arrow keys on a focused knob | Nudge it |
| Double-click a knob | Reset it |

## Running it

Open `index.html` in any modern browser. That's the installation guide in full.

To host it, push the repo and switch on GitHub Pages. There's no build step, no framework and no `node_modules` folder the size of a small county. The only outside requests are for three Google Fonts.

## How it works, briefly

- **Audio:** the Web Audio API does all the work. Each slice is a buffer source with its own gain stage, plus sends to a shared tempo-synced delay and a convolution reverb whose impulse response is generated on the spot.
- **Timing:** the sequencer uses a look-ahead scheduler, so timing comes from the audio clock rather than the browser's very relaxed attitude to `setTimeout`.
- **Transient detection:** energy rises are measured over 512-sample hops, then the strongest peaks are kept, with a minimum gap between them.
- **Time-stretch:** a compact WSOLA implementation. Overlapping windows are read at one speed, written at another, and nudged until the joins stop complaining.
- **Demo break:** synthesised in the browser on load, so the demo uses nobody's recording but ours.

## About the samples

BREAKR ships with no breaks. You bring your own, and you're responsible for what you bring. The famous ones are famous partly because they were sampled without asking, and that's a tradition best admired rather than continued. If you plan to release something, clear your samples or record your own. Your future self, and possibly their solicitor, will thank you.

## Roadmap, loosely

- [ ] Export the pattern as WAV
- [ ] A guided first run for people who've never touched a sampler
- [ ] A cut button that works on touchscreens
- [ ] Two sounds per step, so the kick and the snare can finally share

## Credits

Designed and built by **Olivier Elbhar**, a product manager who'd rather ship something than describe it in a slide deck.

Inspired by the slicing samplers that taught a generation to rearrange other people's drummers, notably Ableton's Simpler and the Amigo sampler. BREAKR isn't affiliated with either. It just admires them from a respectful distance.

## Licence

MIT. Do what you like with it. Attribution is appreciated, though not enforced; we're British about it.
