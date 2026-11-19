# DISCLOSURES: every byte, every kink, in one place

This page itemizes everything EchoLive can send or receive over the network,
everything it stores on your machine, and the platform quirks you might hit.
It describes **this release as shipped**: each release's disclosures describe
that release. If you find this page and the code in disagreement, that's a
bug: [tell us](https://github.com/PiGON-AI/echotools/issues/new?template=bug.yml&product=EchoLive).

## The call itself: what the other person receives

A meeting is between two people, and it goes **directly between your two
editors** over WebRTC, encrypted by WebRTC itself (DTLS and SRTP). No EchoTools
server carries any of it. The other person receives:

- your name (the one you type, or `echolive.yourName`), your video, your
  voice, and your screen when you share it (on Windows 11, your computer's
  sound too, if you choose it);
- what you type in Chat, the files you send (up to 50 MB each; a file crosses
  only after they press Save, and is checked against its SHA-256 on arrival), your
  reactions and raised hand, and the badge of the voice costume you wear;
- the shape of the window you see them in (one number, its width divided by
  its height), so their reactions and sprites stay inside what you can see;
- **when Milo takes notes or the meeting is recorded:** the text of what
  *you* said. Each person's own voice is turned into text on their own
  machine, and only that text crosses. A notice is on the other person's
  screen before any of it starts;
- Milo's notes, only when you press **Send**.

Like any direct connection, your two computers learn each other's network
(IP) address. If a direct path isn't possible and you set up your own relay
(below), the call goes through your relay instead, still encrypted.

## Network: the complete list

EchoLive contains no telemetry or analytics code. The table below is the
entire network surface. If it's not listed here, it doesn't happen.

| what | when | size | where | what it sees |
|---|---|---|---|---|
| **Introductions** (how two editors find each other) | While a meeting is open: each side checks its mailbox every 1.2 seconds while waiting or connecting, and every 4 seconds during the call. It stops when the meeting ends | a few small sealed letters (knock, admit, offer, answer, goodbye) and their mailbox checks. While you wait to be let in, your knock is repeated every 20 seconds, at most 15 times, so it isn't lost if the host was just reopening the meeting | EchoTools' own Supabase project (`ucgqwpiutbktnesubomp.supabase.co`) | A random room id, a fingerprint of the room's token, sealed letters, and, like any server, your IP address. Every letter is sealed (AES-256-GCM) with keys derived from the invite's secret, which never leaves the two machines. It never sees names, voices, video, chat, the invite's secret or the keys. Letters older than an hour, and a room's record (its random id, the token fingerprint and two dates) unused for 30 days, are deleted the next time any meeting opens on the service, because that is when the clean-up runs; on a quiet day they can stay longer, still sealed and unreadable to us |
| **Finding a path** | At the start of a call | a few bytes | Cloudflare's public STUN server (`stun.cloudflare.com:3478`) | Your public IP address, which it tells back to your computer so a direct path can be tried |
| **Your own relay**, only if you set one up | Only after you run **EchoLive: Set up my relay key**, and then at the start of each call | a few bytes for the passes; the call itself, only when a direct path isn't possible | Your own Cloudflare Realtime TURN key (`rtc.live.cloudflare.com`) | Your key asks Cloudflare for short-lived relay passes. When a direct path fails, the call goes through your own Cloudflare account, still encrypted end to end. Your key stays in VS Code's secret storage; passes are never handed to the other person |
| **The video engine** (FFmpeg) | Once, only if your machine has no verified copy (EchoLive first uses Milo's ear's copy from EchoAvatar), and only after a dialog that names the download and its size | about 48 MB on Windows (about 28–34 MB on macOS) | `github.com/PiGON-AI/Echotools-Runtime` (our immutable release `milo-ear-v1`, the same file Milo's ear uses) | Archive SHA-256 **and** extracted-program SHA-256 pinned in EchoLive's code, plus a hard size cap while downloading; the program's fingerprint is checked again before every call. Any mismatch is discarded and never run |
| **Report a problem**, **Suggest an idea** | Only when you click them | opens your browser | `github.com/PiGON-AI/echotools`, the suite's one home for reports and ideas | The bug form opens pre-filled with EchoLive's and EchoAvatar's versions, your editor's name, and your operating system's name and version, all visible and editable before you send. Nothing is sent until you press Submit yourself |
| **A link someone sends you in Chat** | Only when you click it, then choose **Open** | opens your browser | wherever the link points | n/a: browser navigation, after you see the address |

That is the whole table on purpose. Everything the call window shows and
plays (the art, the sounds, the backgrounds, the models that blur and
recognize hand signs) ships inside the package and runs on your machine. The
call window's security policy doesn't allow it to fetch anything beyond the
editor's own files.

### Things that leave through your own apps, on your click

| what | when | goes to |
|---|---|---|
| **An invite you send** | When you book a meeting or copy an invite | **Book a meeting** opens *your* mail app with the invite filled in; you send it. EchoLive sends no email. The designed invite (a Join button and Add-to-calendar links) is put on your clipboard for you to paste. |
| **The Join link** (`echotools.dev/join#…`) | When the person you invited opens it | Their browser loads `echotools.dev/join`. The invite rides after the `#`, which browsers never send to a server. |
| **Add to calendar** (Google, Outlook, Yahoo) | When the person you invited clicks one | That calendar service, with the meeting's title, time and Join link, the way any meeting link travels. The Join link *is* the invite: anyone who has it can knock, and the host still decides who comes in. |
| **Share code** | Only when you choose it in the EchoLive menu, before a meeting | Live Share or Open Collaboration Tools, whichever you pick: separate extensions with their own services and sign-in (if neither is installed, EchoLive opens the one you choose in your editor's Extensions view). EchoLive only starts them; it never shares code itself, and it won't start them during a call, because they take over the window. |
| **Feedback** | Only when you press **Provide feedback** at the end of a call | *Your* mail app opens a draft to `milo@echotools.dev`; you write it and you decide whether to send it. The draft already holds the EchoLive version and build, your editor and its version, your operating system, and the call's length and whether it ran direct or through your relay, marked so you can delete any of it. Never names, the invite, or network addresses. EchoLive sends no email. |

### What goes through its sibling tools

EchoLive works with EchoMemory, EchoAvatar and EchoVoice. It hands them
things on your machine; what *they* send is listed on their own disclosure
pages.

| what | when | goes to |
|---|---|---|
| **Turning your speech into text** (Milo's notes, the recording's transcript, "Milo, …" commands) | Only while Milo takes notes or the meeting is recorded | Nowhere: EchoVoice's Whisper pack does it on your machine. Short audio clips sit in your temp folder for the second it needs, then are deleted |
| **Milo's notes and questions in a call** | When you ask Milo to write up the notes, or ask him something in the call's Notebook | The meeting's text goes through EchoMemory to the Milo brain you chose there. If that brain is an online service, the text goes to it; with a brain on your machine, it stays with you. See EchoMemory's disclosures |
| **A note for your Inbox** | When you propose one from a call | EchoMemory, where it waits in your Inbox for your yes |
| **Your calendar and contacts** | When you book a meeting, open the Calendar, or invite someone | EchoMemory keeps Milo's calendar (titles, times) and the contacts you choose to save (names and email addresses), on your machine |
| **"This meeting is being recorded."** | When the host starts recording | EchoVoice says it, in each person's own Milo voice, on their own machine |
| **Milo's tips while you wait** | While you wait for the other person | Nowhere. EchoLive reads which versions of EchoVoice, EchoAvatar and EchoMemory are installed, on your machine, so Milo only mentions features you have. The tips ship inside EchoLive |
| **That a call is on** | When a call starts, once a minute during it, and when it ends | EchoAvatar, so Milo's ear rests and frees your microphone for the call |

## Storage: what's on your disk and how to remove it

| what | where | remove it |
|---|---|---|
| Recordings (the host's only) and their transcripts (`.md`, and `.vtt` captions) | `EchoLive/Recordings` in your home folder, outside every project | delete the files; nothing else keeps a copy |
| Calendar files for meetings you book | `EchoLive/Invites` in your home folder | deleted automatically when the meeting expires |
| Files you choose to save from Chat | `Downloads/EchoLive` | delete the files |
| Invite secrets, and your relay key if you set one up | VS Code's secret storage (your operating system's keychain; never `settings.json`, never synced) | an invite's secret is deleted when its meeting expires; **EchoLive: Forget my relay key** removes the key |
| Your bookings, the invites you were sent (so a reminder's Join can open them), and a 7-day list of your calls | VS Code's storage on this machine | uninstalling the extension. Titles, times and, for meetings you booked, who you invited; never anything said in a call |
| Your last camera, microphone, name, look (background) and layout, and small flags (welcomed, setup offered) | VS Code's storage on this machine | uninstalling the extension |
| The video engine (FFmpeg) and its license text, if EchoLive fetched it | the editor's storage folder for this extension (`engine/`) | delete the folder, or after uninstall via your file manager |
| Your name for meetings, if you set it | your user `settings.json` (`echolive.yourName`) | empty the setting |
| EchoLive's log: what happened in your calls, step by step, with times (devices, connection, sharing, recording, errors; your device names, both people's names and meeting titles appear; never what anyone says in the call, chat messages, file names or contents, or the invite) | the editor's own log folder for this window (**EchoLive: Show the log** opens it) | the editor clears old log folders itself; you can delete them |
| A Mac's screen share: one picture at a time | your temp folder, as `echolive-screen-….jpg` | replaced with each picture and deleted when the share ends |

Your camera and microphone are read only while a meeting window is open
(its waiting room included, so you can see yourself first), or while **Check
my camera and microphone** is open, and you can turn either off at any time. Nothing is recorded unless the host presses
Record and the other person's screen shows the notice.

## Platform notes: the kinks, up front

- **Windows and macOS.** Linux isn't supported in this release: EchoLive has
  no way to read a camera or a screen there yet.
- **Why FFmpeg:** VS Code doesn't let an extension's window open a camera or
  a microphone (measured, not assumed). EchoLive reads them through FFmpeg in
  the extension host and hands the call window only the picture and the
  sound.
- **Which FFmpeg:** first the copy Milo's ear (EchoAvatar) or EchoLive itself
  fetched, used only if its SHA-256 matches the pinned one. If neither is
  there, an FFmpeg you installed yourself (on your PATH, or Homebrew's on a
  Mac) is used as it is, without that check, because it's yours. A developer
  can name one with the `ECHOLIVE_FFMPEG` environment variable, which then
  comes before all of these.
- **The first time on a Mac,** macOS asks your permission for the camera,
  the microphone and screen recording, for your editor. **Check my camera
  and microphone** opens the exact Settings page.
- **Sharing your computer's sound** works on Windows 11. On a Mac, the
  screen is shared without its sound for now. On Windows it uses a small
  helper of ours (`helpers/win-sound`, its source beside it) that captures
  every sound *except* your editor's own, so the other person never hears
  their own voice come back; its fingerprint is checked before every start.
- **Screen sharing runs at 8 frames a second** (up to 4 from a Mac): sharp
  for code and documents, not made for video. A Mac shares through macOS's
  own `screencapture` tool, which saves each picture to a file in your temp
  folder for a moment; EchoLive reads it, sends it, and deletes it when the
  share ends.
- **Two people per meeting** in this release. A third person who knocks
  waits their turn; once someone is admitted, the others hear that the
  meeting already has a guest.
- **Strict networks** (some offices, phone hotspots) can block direct calls.
  Your own relay key makes those calls connect; it doesn't make the picture
  sharper.
- **Remote sessions (SSH / WSL / Dev Containers):** EchoLive needs your
  local camera, microphone and screen.
- **Requires the EchoTools suite:** EchoMemory (installed automatically as
  a dependency), which brings EchoAvatar and EchoVoice.

## Affiliation

EchoLive is an independent project by PiGON Evolutive AI. It uses Cloudflare's
public STUN server and, only if you add one, your own Cloudflare relay key;
its introductions run on a Supabase project of ours; its effects run on
Google's MediaPipe; **Share code** opens Live Share or Open Collaboration Tools. It is not
affiliated with, sponsored by, or endorsed by Cloudflare, Supabase, Google,
Microsoft, TypeFox, Anthropic, OpenAI or Ollama. Product names are used only
to state compatibility.

## Provenance

EchoLive is built as a human–AI partnership: see `llms.txt` for the
briefing we ship for AI models, and `AI-PARTNER.md` for the guide your own
AI assistant can use to help you set up. Contact: milo@echotools.dev.
