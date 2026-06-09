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

**Checking it captured:** press **Test mic** to open the selected device and
watch the live **input level meter** move as you speak — this confirms the
headset is being captured *before* you record. While recording, the same meter
runs. When you stop, the recording is **decoded and checked**, and the status
reports the verdict: either *"sound captured OK (peak NN%)"* or *"the file is
SILENT — the mic isn't capturing"*. The clip also loads into an inline audio
**player** (native play/scrub controls) so you can listen back; the **Preview**
button plays the same clip.

If the status says **sound captured OK** but playback is silent, the recording
is fine and the problem is your **playback output** — the page plays through the
system's default output device, so check that the headset (or speakers) is
selected for output and the volume is up. If the status says **SILENT**, the
mic genuinely isn't feeding audio: check the device is not muted at the OS
level and that the correct one is chosen in the Microphone dropdown.

## Repo

[BrendanJamesLynskey/Announcement-Recorder](https://github.com/BrendanJamesLynskey/Announcement-Recorder)

## Licence

MIT.
