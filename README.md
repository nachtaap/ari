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
the beat. A.R.I.'s expression shifts with the moment — happy by default, briefly
surprised when a request lands, quietly "in the zone" during a solo or breakdown,
and comically deflated if a guest lets the mic droop.

**The music** is fully generative. Each track (1–3 minutes) picks a genre — boom
bap, trap, jerk, drum n bass, 2000s rnb, or house — and a scale (mostly minor, but
sometimes dorian, major, or phrygian), which together with the BPM range, drum
patterns, swing, bass synthesis (saw / 808 / sub / round) and harmony style (pads,
keys, or house stabs) keep tracks from blurring into each other. Every track has a
real arrangement (one of several intro/main/breakdown shapes, not always the same
skeleton), with voice-led chords and a bass that follows the chord root. Drums,
bass, chords and leads are all synthesized per-note with the Web Audio API and
scheduled on a driftless clock, so playback survives the tab being backgrounded
without stuttering.

**The guests** arrive at random, each with a generated look (color, height,
build, headwear) and a coiled cable plugged into the rig. A guest requests a
genre — spoken out loud in a retro robotic voice, with A.R.I. answering back —
then A.R.I. crossfades into a fresh track in that style, and the guest performs:
9 out of 10 times on the mic, occasionally on sax, flute, acoustic or electric
guitar, or (rarely) a violin or a spacy e-violin. Sometimes it's a duo. Every
guest sticks around for at least one full track before wrapping up, and often
leaves with a flat-out fake "follow me on [invented platform]" shout-out and a
speech bubble to match — occasionally with a wave goodbye.

**Other details worth noticing:** a street sign fades in as the crew roams to a
new block; a rare reverse-shot camera flip reveals the cameraman — Dill-2000
(model Z); roughly
every 10–15 tracks the rig "runs out of battery" for a short, charming
intermission; and a small status line quietly shows NYC's current weather
(fetched live, fails silently if offline) alongside the rig's battery level,
color-coded from green to red.

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

Keep `index.html`, `manifest.webmanifest`, `sw.js`, `apple-touch-icon.png`,
`icon-192.png`, `icon-512.png`, `icon-maskable-192.png`, `icon-maskable-512.png`,
`favicon-32.png` and `favicon-16.png` together in the same directory.

## Current version

- **Version 77** — the cameraman now has his own fictional name on-screen too,
  Dill-2000 (model Z), matching the disclaimer's no-real-names policy.
- **Version 76** — track info now sits in fixed, predictable rows (track
  number + time, title, genre/tempo, guest info) instead of a couple of long
  strings that wrapped differently depending on content length.
- **Version 73** — a pass of small-but-real fixes:
  - Fixed a rare "dentist drill" glitch: leads occasionally rolled several
    same-direction steps in a row, producing a fast ascending run. Melody
    movement is now run-limited so that can't happen.
  - Fixed audible crackle on lower notes: the electric-guitar distortion had
    no oversampling, which aliases in Web Audio. Added 4× oversampling.
  - The mic is now always cyan instead of matching the guest's own color, so
    it doesn't disappear against certain outfits.
  - Track names got a much bigger word pool, more phrasing shapes, and a
    no-immediate-repeat rule.
- **Version 60–62** — guest behavior overhaul: renamed "visitor" to "guest",
  arms no longer pump to the beat (was distracting), farewell speech bubbles
  show up far more often, and every guest now finishes at least one full
  track before leaving. Widened track variety (arrangement shapes, scale
  modes, root range, more chord progressions) and then re-tuned the audio
  comfort pass so the wider variety never drifts into harsh territory.
  Guest "follow me on…" handles were rebuilt to look like real usernames
  instead of URL-like strings.
- **Version 66–71** — added a small, quiet status line under the header:
  NYC's live weather (via Open-Meteo, fails silently offline) and the rig's
  battery level, color-coded per condition and from green to red.
- **Version 36–41** — the rear speaker was fixed to the backpack; a
  battery-swap intermission now runs every 10–15 tracks; a slow-blinking
  status LED sits by "live from the grid"; A.R.I. gained real facial
  expressions (happy / surprised / in-the-zone / comically-deflated-at-a-drooping-mic).
- **Version 18–33** — adopted a cleaner hidden-line rendering technique
  (painter's-algorithm occluders) for a calmer, more solid-reading wireframe;
  gave guests feet and a second arm; rebuilt the background-audio lifecycle
  around a driftless clock so playback survives the tab being minimized
  without stuttering or drifting out of sync.
- **Version 13–17** — fixed a PWA identity bug: the manifest and service
  worker now use an explicit, unique scope, so the installed app can no
  longer be confused with an unrelated app on the same device.
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
- Visible footer tribute: `version 77`.
- Service worker cache: `ari-v77`.

## License

Code: MIT. The tribute nature of the project (see disclaimer) applies to the
concept and inspiration; everything in this repository is original work.
