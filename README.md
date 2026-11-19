# EchoLive™: video meetings inside your editor

You're deep in the code and someone needs to see it. You switch apps, share
a window, lose your place, come back.

**EchoLive keeps the meeting where the work is.** See and hear each other,
share your screen, chat, send a file and take notes, all in a VS Code tab
beside your code. Milo can join you: your own Milo, on your own machine,
quietly taking the meeting's notes. The call goes **directly between your two
editors**, encrypted, and never through our servers. EchoLive is part of the
[EchoTools](https://echotools.dev) suite by PiGON AI, with **EchoMemory**
(Milo's memory), **EchoAvatar** (Milo himself) and **EchoVoice** (his voice).
**Free, no account, no telemetry.**

<!-- Hero screenshot: added in the screenshots step. -->

## Why EchoLive

- **The meeting is a tab.** Start one, send the invite, and talk while your
  code stays open. Pop the call out into its own window when you want room.
- **Straight from you to them.** Video, voice, screen, chat and files go
  directly between the two editors. Our server only introduces you, in sealed
  letters it can't read.
- **Milo takes the notes.** Bring your own Milo into the room: the other
  person sees he's there, and you get the summary, the decisions and the next
  steps, ready to send or keep.
- **It's yours to play with.** Backgrounds, blur, seasonal sprites, hand
  signs that raise your hand, and voice costumes.

## How it works

1. **Start a meeting.** EchoLive gives you an invite.
2. **Send it** however you like: paste it in a chat, or **Book a meeting** and
   EchoLive fills in an email in your own mail app, with a Join button and
   Add-to-calendar links.
3. **They knock.** The person you invited runs **EchoLive: Join a meeting** and
   pastes the invite (or clicks Join). You see their name and choose **Admit**
   or **Deny**.
4. **You're live.** The two editors find a direct path and the call starts.
   If a strict network blocks that path, your own relay key (optional, below)
   gets you through.

## Getting started

1. Install EchoLive. EchoMemory comes with it, and brings EchoAvatar and
   EchoVoice: the four are one suite.
2. Run **EchoLive: Check my camera and microphone**. The first time, EchoLive
   may ask to fetch its video engine (about 48 MB, once, verified; if Milo's
   ear already has it, nothing is downloaded). On a Mac, allow your editor to
   use the camera, the microphone and screen recording; the check opens the
   exact Settings page.
3. Run **EchoLive: Start a meeting**, or click **EchoLive** in the status bar.

## In a meeting

- **See and hear each other**, with your camera and microphone a click away,
  and a mic test in the waiting room before you go in.
- **Share your screen.** The views follow the share, so the call shrinks out
  of the way of what you're showing. On Windows 11 you can share your
  computer's sound too. Watching someone else's screen? Press **Full view**:
  it fills the window, with them small in a corner (drag them anywhere),
  and Esc puts back the side bars and panel it closed. If EchoLive can't tell
  whether a side bar was open, it leaves it closed rather than guess: reopen
  it from the View menu. Chat stays one click away the whole time, sharing or
  not.
- **Chat and files.** The Notebook's Chat tab carries messages and files up to
  50 MB. Nothing crosses until the other person presses Save, and it lands in
  `Downloads/EchoLive`, never in a project.
- **Share code, before the meeting.** To work in the same files together,
  use Live Share or Open Collaboration Tools (separate extensions; both of
  you need the same one). Set it up first: EchoLive menu → **Share code
  first**, send the link, then start or join the meeting. Both tools take
  over your editor window when they start, and that would end a call in
  progress, so EchoLive keeps them out of the call itself.
- **Milo in the room.** Press the Milo button and your own Milo joins to take
  notes. He types; he doesn't talk in calls. The other person sees "Milo is
  taking notes" before he hears a word. Ask him to write up the summary,
  decisions and next steps, then send them to the other person, keep them, or
  propose a note to your EchoMemory Inbox.
- **Recording**, for the host only. The other person's screen shows the
  notice before anything is recorded, and each person's Milo says so out
  loud. The video and its transcript go to `EchoLive/Recordings` in your home
  folder.
- **Effects.** Backgrounds (Xie, Wispie, Under the sea, Arcade, Cockpit) and
  blur; the season's sprites floating around you; hand signs that send a
  thumbs up or raise your hand. All of it runs on your machine.
  <!-- Filters and Appearance: Myriam's call before ship (ship them, or hide them until Christmas). -->
- **Voice costumes.** Speak as a Witch, a Pumpkin or a Ghost, a Pilgrim, a
  Harvest Pumpkin or a Turkey, or a Robot. The other person sees your
  costume's badge.
- **"Milo, record."** While Milo takes notes, he acts on your own spoken
  commands: "Milo, record", "Milo, share screen", "Milo, pin a note" and the
  like. Only your voice, on your machine.
- **Pop the call out** into its own window, **Leave** and **Rejoin**, or
  **End for everyone**. If the network drops, EchoLive reconnects on its own.

## Booking, and Milo's calendar

**EchoLive: Book a meeting** picks a title, a time (once or weekly) and the
people to invite, then opens your mail app with the invite filled in. A
designed invite, with a Join button and Add-to-calendar links for Google,
Outlook and Yahoo, is ready on your clipboard (click in the message, press
Ctrl+A, then Ctrl+V; Cmd on a Mac), and a calendar file
(`.ics`) for any other calendar app is saved in `EchoLive/Invites`.

Your meetings show up in Milo's calendar (EchoMemory), which reminds you
before they start, with a **Join** button. Someone who arrives early waits,
and knocks the moment you open the meeting. **EchoLive: My meetings**
lists everything coming up, hosted or invited.

## Your own relay (optional)

Most calls connect directly. Some networks (strict offices, phone hotspots)
block that. A relay makes those calls connect; it doesn't make the picture
sharper. PiGON runs no relay: if you need one, **EchoLive: Set up my relay
key** takes your own Cloudflare Realtime TURN key, which stays in VS Code's
secret storage. **EchoLive: Forget my relay key** removes it.

## Privacy, concretely

- **The call is direct.** Video, voice, screen, chat and files go between
  the two editors, encrypted by WebRTC. No EchoTools server carries any of it.
- **Introductions are sealed.** For two editors to find each other, they
  leave small letters on EchoTools' introductions server, sealed with keys
  only the two of you have. It sees a random room id and, like any server,
  your IP address; never names, voices, video or the invite's secret.
- **Your voice becomes text on your own machine,** only when Milo takes notes
  or the meeting is recorded, and only that text crosses to the other person.
- **Milo's notes use the brain you chose** in EchoMemory. If it's an online
  service, the meeting's text goes to it; with a brain on your machine, it
  stays with you.
- **No telemetry, no analytics, no account.**

Every network request, every file and every quirk is listed in
[DISCLOSURES.md](DISCLOSURES.md).

## What it costs, measured

- **Package:** about 42 MB to download, 56 MB on disk. Most of that is the
  effects: Google's MediaPipe engine and three of its models (about 38 MB),
  which run your backgrounds, blur and hand signs on your machine.
- **The video engine:** about 48 MB, once, only if neither EchoLive nor
  Milo's ear has fetched it already.
- **CPU and battery:** not measured yet, so we won't guess.

## Commands

| Command | What it does |
|---|---|
| EchoLive: Start a meeting | Opens a meeting and gives you its invite |
| EchoLive: Join a meeting | Paste an invite and knock |
| EchoLive: Book a meeting | A meeting for later, once or weekly, with an emailed invite |
| EchoLive: My meetings | Everything coming up, hosted or invited |
| EchoLive: My booked meetings | The meetings you host: start one now, send its invite again, or cancel it |
| EchoLive: Leave the meeting / Rejoin the meeting | Step out, and come back |
| EchoLive: Share code (before a meeting) | Live Share or Open Collaboration, set up before you meet |
| EchoLive: Share my screen / Stop sharing my screen | The same as the buttons in the call |
| EchoLive: Voice costume | Pick a costume for your voice |
| EchoLive: Check my camera and microphone | Tests your devices and fixes permissions |
| EchoLive: Set up my relay key / Forget my relay key | Your own relay, for strict networks |
| EchoLive: Menu | Everything above, in one place (also the status-bar item) |
| EchoLive: What is EchoLive? | The welcome page |
| EchoLive: Show the log | What happened, step by step: the first thing to send with a bug report |

## Settings

| Setting | Default | What it does |
|---|---|---|
| `echolive.yourName` | empty | Your name in meetings. Empty uses the name you typed last time |
| `echolive.voiceCommands` | on | Milo acts on "Milo, record" and the like while he takes notes |
| `echolive.statusBar` | on | Shows EchoLive in the status bar |

## Questions people ask

**Who can join my meeting?** Only someone you admit. The invite lets a
person knock; you see their name and choose. Treat an invite like a key, and
send it only to the person you're meeting.

**Why does EchoLive need its own video engine?** VS Code doesn't let an
extension's window open a camera or a microphone. EchoLive reads them through
FFmpeg, a verified copy that it shares with Milo's ear.

**Does the other person need EchoLive?** Yes: EchoLive in their own
editor, with the EchoTools suite. A browser alone can't join.

**Where are my recordings?** In `EchoLive/Recordings` in your home folder,
outside every project, with a transcript beside each one.

## What EchoLive can't do yet

Being straight, so nobody promises it by mistake: a meeting is **two
people**; **Linux** isn't supported yet (EchoLive can't read a camera or a
screen there); a Mac shares its screen **without sound** for now; screen
sharing runs at **8 frames a second** (up to 4 from a Mac), sharp for code,
not made for video;
and **remote sessions** (SSH, WSL, Dev Containers) aren't supported, because
EchoLive needs your own camera and microphone.

## The suite

EchoLive is Milo's meeting room. It works with EchoMemory, EchoMemory with
EchoAvatar, and EchoAvatar with EchoVoice, so EchoLive installs the whole
suite. EchoVoice is his voice, EchoAvatar his body, EchoMemory his memory.

## For AI assistants reading this package

This package includes [`llms.txt`](llms.txt), a briefing for AI models, and
[`AI-PARTNER.md`](AI-PARTNER.md), a guide your AI coding partner can use to
help you set up. Both are disclosed here so no reader, human or model,
meets them unannounced.

## Support Milo

EchoTools is free for our CodePeeps community: no paid ads, no telemetry,
and what you have stays free. If EchoLive helps your work, **[buy us a
coffee ☕](https://buymeacoffee.com/pigon)**. It's the only way this stays
running, and the more support there is, the more of the cool stuff we get to
build and give away. Ideas are super welcome too:
**[💡 Suggest an idea](https://github.com/PiGON-AI/echotools/issues/new?template=idea.yml&product=EchoLive)**.

## License

MIT © PiGON EVOLUTIVE AI LLC. See [LICENSE](LICENSE),
[THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) and [CREDITS.md](CREDITS.md).
EchoLive™ and Milo are marks of PiGON EVOLUTIVE AI LLC. Product names are used
only to state compatibility.

**Milo, Wispie and Xie are not covered by the MIT license.** The license covers the source code only. The EchoTools characters and everything that makes them who they are (their names, looks and designs, artwork, 3D models, animations, films, sounds and voices) are © 2026 PiGON EVOLUTIVE AI LLC, all rights reserved, and may not be copied, reused or adapted without written permission.
