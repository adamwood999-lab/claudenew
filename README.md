# Fretwork

A guitar chord progression builder that runs entirely in the browser. Build a
progression bar by bar, choose a strumming pattern, and hear it played back on a
synthesised acoustic guitar. No accounts, no server, no data leaves the device.

**Live:** https://adamwood999-lab.github.io/claudenew/

## What it does

- **Chords** — 12 roots x 19 qualities (maj, min, 7, m7, maj7, sus2, sus4, add9,
  6, m6, 9, m9, maj9, dim, dim7, aug, m7b5, 7sus4, 5), each rendered as a real
  fretboard diagram with open strings, muted strings and barres marked.
  Classic open voicings are used where they exist; everything else falls back to
  movable E-shape and A-shape barre forms, picked for the lowest comfortable
  position.
- **Mood search** — describe how it should feel and get progressions back.
  74 progressions are tagged across 57 canonical moods, and a vocabulary of
  ~1,300 terms maps onto those tags, so feelings ("melancholic", "defiant",
  "bittersweet"), genres ("bossa nova", "grunge", "gospel", "city pop"),
  scenes ("rainy night", "road trip", "boss fight", "funeral") and loose phrases
  ("something chilled but a bit sad") all resolve. Matching handles plurals and
  participles, multi-word phrases, and typos, and every result explains why it
  feels the way it does and can be previewed without disturbing what you are
  already working on.
- **More like this** — the mood search can also work from whatever is already
  on screen. It reads the progression's character out of its own harmony (minor
  tonic, sevenths, power chords, suspensions, borrowed chords), its tempo and
  its strumming pattern, then offers neighbours — or nudges: darker, jazzier,
  calmer, heavier, weirder, dreamier and so on. Typing "more like this, but
  sadder" does the same thing.
- **Key awareness** — pick a key and the seven diatonic chords appear as
  one-tap buttons. Every bar is labelled with its roman numeral, so the shape of
  the progression is readable at a glance.
- **Chord lengths** — each chord lasts anywhere from one to eight beats. Select
  it and use the stepper to shorten or extend; the card's width and its row of
  beat pips show how long it holds, and a running total gives the length of the
  whole progression. The strumming pattern stays a bar-long rhythm underneath
  rather than restarting on every chord, so two two-beat chords share one bar of
  strumming the way they would if you were playing it.
- **Strumming** — an eight-slot grid per bar. Each slot can be a downstroke,
  upstroke, muted chuck, bass note or top-string stab, so the same grid covers
  strumming, boom-chick and Travis-style picking. Nine presets to start from,
  plus a swing control.
- **Playback** — a Karplus-Strong plucked-string synth, one voice per string,
  with pick-position filtering, stereo spread across the neck, a body resonance
  filter and a short room reverb. Strums are spread and humanised rather than
  played as blocks, and the previous chord damps when the fretting hand moves.
- **MIDI out** — where the browser supports Web MIDI, notes can be sent to a
  connected instrument or DAW alongside the built-in guitar.
- **Keeping things** — progressions save to the browser, and the "copy link"
  button encodes the whole progression into the URL to share.

## Running it

It is one self-contained `index.html` with no build step and no dependencies
beyond two Google Fonts. Open the file directly, or serve the folder:

```sh
python3 -m http.server 8000     # then open http://localhost:8000
```

## Publishing to GitHub Pages

In the repository on github.com: **Settings -> Pages -> Source: Deploy from a
branch**, pick the branch and the `/ (root)` folder, then Save. The site appears
at `https://adamwood999-lab.github.io/claudenew/` within a minute or two, and
updates on every push.

## Notes on the music

Relative search is deliberately not pure mood matching. A bright progression
shares no mood tags at all with a dark one, so asking for "the same thing but
darker" in tag space alone collapses to whichever progression is most darkly
tagged — a two-chord drone rather than a relative of the four chords you were
playing. Results are therefore held near the original by shape as well: bar
count, the mix of chord types, and the intervals the roots move by. Asking
I–V–vi–IV to get sadder returns i–VI–III–VII, which is what a musician would
have reached for.

Every one of the 57 mood tags is used by at least one progression and all 1,304
searchable terms resolve to at least one result, so no keyword is a dead end.

Voicings are generated rather than stored, then checked: all 228 root/quality
combinations were verified to contain only chord tones, to include the root and
the defining third (or fourth/fifth for suspended and power chords), and to stay
within a four-fret span. The synth is tuned to within two cents across the
range of the instrument.
