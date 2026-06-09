# Announcement Recorder

A browser-based recorder for **Welsham Railway** station announcements and
security messages. Pick a message type (and a station, where the template
needs one), read the on-screen script aloud, and save the result as a WebM
(Opus) audio file ready to drop into the sim. Extracted into its own repo
from the [Welsham Railway](https://github.com/BrendanJamesLynskey/Welsham-Railway)
sim, where it previously lived as `recorder.html`.

[Open it here](https://brendanjameslynskey.github.io/Announcement-Recorder/)

## Access

The recorder is behind a password gate. Enter the passphrase to reach the
tool. The password is required on every visit and every reload — nothing is
remembered between page loads.

> **Note:** the gate is **client-side only**. Because this is a static page,
> the passphrase is present in the page source, so the gate keeps casual
> visitors out rather than providing real access control. Don't rely on it to
> protect anything sensitive.

## Messages

Built-in templates come in three groups, plus a free-text **Custom** option:

- **On train** — next station, arriving, final stop, welcome, doors
  closing / released, apology for delay.
- **Security** — belongings, suspicious items, emergency alarm.
- **Platform** — station/concourse PA announcements: next train to arrive,
  now standing, approaching, delayed, cancelled, platform alteration, and a
  non-stopping-train warning. These read out a **platform number** (selected
  from the Platform dropdown) alongside the destination, e.g. *"The next train
  to arrive at platform 2 is the Welsham Railway service to Bankside."*

Templates that mention a station pull the station list from
[`welsham-circle.json`](welsham-circle.json) so the dropdown always matches the
bundled Welsham Circle route (it falls back to a hard-coded list if the file
can't be fetched). The Station and Platform dropdowns are only used by the
templates that reference them.

## Recording

Recording uses the browser's `MediaRecorder`, which requires a secure context
— open the page over **HTTPS** (GitHub Pages) or **localhost**. The first
Record click asks for microphone permission. Saved files are named
descriptively (e.g. `next-station-bankside.webm`); convert to WAV externally
with `ffmpeg` if your target needs PCM.

**Choosing the microphone:** use the **Microphone** dropdown in the Capture
section to pick the input device. If a USB headset is connected, select it here
— otherwise the browser records from the operating system's default input,
which is often the computer's built-in mic rather than the headset. Device
names only appear once microphone permission has been granted, so record once
(or press **Refresh**) to populate the list, then pick your headset.

**Checking it captured:** while recording, a live **input level meter** fills
as the mic picks up sound — watch it move as you speak to confirm the right
device is being captured. When you stop, the clip loads into an inline audio
**player** (with native play/scrub controls and a duration readout) so you can
listen back before saving; the **Preview** button plays the same clip. If a
recording comes back silent, the status flags it so you can re-check the mic
selection.

## Repo

[BrendanJamesLynskey/Announcement-Recorder](https://github.com/BrendanJamesLynskey/Announcement-Recorder)

## Licence

MIT.
