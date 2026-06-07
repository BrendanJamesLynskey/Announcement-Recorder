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
tool; a correct entry is remembered for the browser-tab session so a reload
doesn't re-prompt.

> **Note:** the gate is **client-side only**. Because this is a static page,
> the passphrase is present in the page source, so the gate keeps casual
> visitors out rather than providing real access control. Don't rely on it to
> protect anything sensitive.

## Messages

Twelve templates are built in — next station, arriving, final stop, welcome,
doors closing / released, apology for delay, three security announcements, and
a free-text **Custom** option. Templates that mention a station name pull the
station list from [`welsham-circle.json`](welsham-circle.json) so the dropdown
always matches the bundled Welsham Circle route (it falls back to a hard-coded
list if the file can't be fetched).

## Recording

Recording uses the browser's `MediaRecorder`, which requires a secure context
— open the page over **HTTPS** (GitHub Pages) or **localhost**. The first
Record click asks for microphone permission. Saved files are named
descriptively (e.g. `next-station-bankside.webm`); convert to WAV externally
with `ffmpeg` if your target needs PCM.

## Repo

[BrendanJamesLynskey/Announcement-Recorder](https://github.com/BrendanJamesLynskey/Announcement-Recorder)

## Licence

MIT.
