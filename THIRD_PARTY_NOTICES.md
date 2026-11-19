# Third-Party Notices

EchoLive bundles the following third-party software, models and icons.
License texts are reproduced or shipped beside the files, as their licenses
require.

## MediaPipe Tasks Vision (backgrounds, blur and hand gestures)

The call window's background, blur and hand-gesture effects run on
[MediaPipe Tasks Vision](https://github.com/google-ai-edge/mediapipe)
(© Google LLC), npm package `@mediapipe/tasks-vision` version **1.2.2**,
used unmodified under the **Apache License 2.0**. It ships as
`media/vision/` (`vision_bundle.mjs`, `vision_wasm_internal.js`,
`vision_wasm_internal.wasm`).

License text: `media/LICENSE-mediapipe-apache-2.0.txt`.

## MediaPipe models (backgrounds, blur and hand gestures)

Three of Google's published MediaPipe models ship unmodified, under the
**Apache License 2.0** (the same license text as above):

- `media/selfie_segmenter.tflite`: separates you from your background
  ([Image segmenter](https://developers.google.com/edge/mediapipe/solutions/vision/image_segmenter)).
- `media/selfie_multiclass_256x256.tflite`: the finer version of the same
  separation (hair, face, body, clothes)
  ([Image segmenter](https://developers.google.com/edge/mediapipe/solutions/vision/image_segmenter)).
- `media/gesture_recognizer.task`: recognizes the hand signs that raise your
  hand or send a reaction
  ([Gesture recognizer](https://developers.google.com/edge/mediapipe/solutions/vision/gesture_recognizer)).

All three run on your machine, inside the call window. They read only the
picture from your own camera, and nothing they see leaves your computer.

## Codicons (the call window's icons)

`page/ui/assets/codicon.css`, with its embedded font, is Microsoft's
[Codicons](https://github.com/microsoft/vscode-codicons), the icon set VS Code
itself uses, bundled unmodified under the **Creative Commons Attribution 4.0
International** license (CC BY 4.0).

License text and attribution: `page/ui/assets/CODICONS-NOTICE.txt`.

## Downloaded at runtime, only if your machine needs it

- **FFmpeg** ([ffmpeg.org](https://ffmpeg.org/)). VS Code doesn't let an
  extension's window open a camera or a microphone, so EchoLive reads them,
  and your screen when you share it, through FFmpeg. If Milo's ear
  (EchoAvatar) already fetched FFmpeg, EchoLive uses that same verified copy.
  If not, EchoLive asks you first, then fetches the identical pinned build.
  The archive and the extracted program are both SHA-256-verified against
  digests written into EchoLive's code, and the program is checked again
  before every call.

  FFmpeg is **run as a separate downloaded program**. It isn't linked into or
  shipped with this extension, so its license never reaches this package. A
  copy of the license for the exact build in use is written beside the
  program as `FFMPEG-LICENSE.txt` when it's installed, and that file is the
  authority on its terms.

## Not third-party

The three scene backgrounds (Under the sea, Arcade and Cockpit) are credited
with their sources in [CREDITS.md](CREDITS.md).

Everything else in the package is PiGON EVOLUTIVE AI LLC's own work. That
includes the art of Milo in the room, the hand-sign and reaction pictures,
the seasonal sprites, the call window's sounds, the Xie and Wispie
backgrounds, and the small Windows helper that shares your computer's sound
(`helpers/win-sound`, with its source beside it). See
[CREDITS.md](CREDITS.md).
