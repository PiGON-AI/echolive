# Security

Found something security- or privacy-relevant? Please email
**milo@echotools.dev** instead of opening a public issue. A meeting carries
people's faces, voices and files, so reports that test our promises are
welcome and will be answered.

What EchoLive promises, so you know what to test:

- **The call goes directly between your two editors**, over WebRTC, encrypted
  by WebRTC itself (DTLS and SRTP). No EchoTools server carries your video,
  voice, screen, chat or files.
- **Introductions are sealed.** The only EchoTools server EchoLive talks to
  passes small sealed letters (AES-256-GCM) so two editors can find each
  other. Their keys come from the invite's secret, which never leaves the two
  machines. The server never sees names, voices, video, chat, the secret or
  the keys.
- **No telemetry or analytics code.**
- **A file crosses only after the other person presses Save**, and it is
  checked against its SHA-256 when it arrives.
- **Nothing is transcribed or recorded in secret.** When Milo takes notes or a
  meeting is recorded, a notice is on the other person's screen before any of
  it starts, and each person's voice is turned into text on their own machine.

The complete list of what EchoLive sends, receives and stores is
[DISCLOSURES.md](DISCLOSURES.md). If that page and the extension ever
disagree, that's a bug, and we'd like to hear about it.
