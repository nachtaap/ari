# A.R.I. — Audiological Roaming Intelligence

A minimalist, generative web experience. An isometric neon android roams the grid
with a wearable synth rig, making beats on the spot. Every now and then a visitor
steps up on A.R.I.'s right side, requests a genre — and performs on it.

**Live demo:** https://nachtaap.github.io/A.R.I./  
**Best experienced with sound on.**

![A.R.I. preview](icon-512.png)

Everything is a single HTML file. No build step, no dependencies, no samples.

## ⚠️ Disclaimer

**This is an unofficial fan tribute inspired by [ARIatHOME](https://www.youtube.com/@ARIatHOME),
the NYC street musician and streamer.** It is not affiliated with, endorsed by, or
connected to ARIatHOME in any way. No music, recordings, samples, footage, names,
or likenesses from ARIatHOME are used — all audio is synthesized live in the
browser with the Web Audio API, and all visuals are original line art.

If you enjoy this, go watch the real thing. It's better.

## How it works

**The scene** is procedural SVG line art in an isometric projection: A.R.I. with
headphones and headset mic, a hip-mounted flightcase rig (jog wheel, pads, keys,
faders, the corner monitor), backpack speakers, and comic sound dashes pulsing on
the beat.

**The music** is fully generative. Each track (1–3 minutes) picks a genre — boom
bap, trap, jerk, drum n bass, 2000s rnb, or house — which sets the BPM range,
drum patterns, swing, bass synthesis (saw / 808 / sub / round) and harmony style
(pads, keys, or house stabs). Drums, bass, chords and leads are all synthesized
per-note with the Web Audio API and scheduled with a 25 ms lookahead loop.

**The visitors** arrive at random, each with a generated look (color, height,
outfit, headwear) and a coiled cable plugged into the rig. A visitor requests a
genre — spoken out loud in a retro robotic voice, with A.R.I. answering back —
then A.R.I. crossfades into a fresh track in that style, and the visitor
performs: 9 out of 10 times on the mic, occasionally on sax, flute, acoustic or
electric guitar, or (rarely) a violin or a spacy e-violin. Sometimes it's a duo.

The speech is [SAM (Software Automatic Mouth)](https://github.com/discordier/sam),
the 1982 C64 speech synthesizer ported to JavaScript by Christian Schiffler (MIT),
inlined so everything stays a single file.

## Running it

Open `index.html` in a browser. That's it.

For the screen wake lock to work (keeps the display on during a stream), serve it
over `https` or `localhost` — for example:

```bash
npx serve .
```

Tap A.R.I. to start the stream. Space toggles play/pause.

## Installing as an app

Served over https (GitHub Pages works), A.R.I. is an installable PWA:

- **Android / Chrome**: menu → "Install app" (or the install prompt). The
  `manifest.webmanifest`, icons and `sw.js` service worker make it installable
  and cache the app shell for offline-ish startup.
- **iOS / Safari**: share sheet → "Add to Home Screen". Runs standalone with the
  dark status bar.

Keep `index.html`, `manifest.webmanifest`, `sw.js`, `icon-192.png` and
`icon-512.png` together in the same directory.

## Current version

- **Version 12** — the breakdown now keeps the core kick+snare groove (stripped
  of hats, bass and extras) instead of dropping to near-silence, so the flow
  carries through and the main sections land harder when everything returns.
- **Version 11** — headphone-comfort audio pass:
  - Track roots sit lower, and all leads dropped an octave (the second visitor
    was two octaves too high); flute/violin/e-violin no longer secretly play an
    octave up.
  - A hard lead ceiling plus a gentle master high-shelf keep melodies out of the
    piercing register — the low end comes through far more often now.
- **Version 10** — reworked generative music engine for consistent depth:
  - **Arrangement**: every track now has a real structure (intro → main →
    breakdown → main → outro) with elements entering and leaving on bar
    boundaries, plus small fills on section transitions.
  - **Voice-leading**: chords now move smoothly (each voice stays near the
    previous one) and the bass follows the chord root instead of wandering.
  - **Section-aware interaction**: drums, hats, leads and A.R.I.'s own vocals
    respect the arrangement — sparse in the intro, open in the breakdown, full
    in the main sections.
  - No shrill/"modem" tones: nothing was added that can become harsh; depth
    comes from existing sounds playing at the right moments.
- Visible footer tribute: `version 10`.
- Service worker cache: `ari-v26`.

## License

Code: MIT. The tribute nature of the project (see disclaimer) applies to the
concept and inspiration; everything in this repository is original work.
