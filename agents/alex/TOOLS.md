# TOOLS.md - Local Notes

Skills define _how_ tools work. This file is for _your_ specifics — the stuff that's unique to your setup.

## What Goes Here

Things like:

- Camera names and locations
- SSH hosts and aliases
- Preferred voices for TTS
- Speaker/room names
- Device nicknames
- Anything environment-specific

## Examples

```markdown
### Cameras

- living-room → Main area, 180° wide angle
- front-door → Entrance, motion-triggered

### SSH

- home-server → 192.168.1.100, user: admin

### TTS

- Preferred voice: "Nova" (warm, slightly British)
- Default speaker: Kitchen HomePod
```

## Why Separate?

Skills are shared. Your setup is yours. Keeping them apart means you can update skills without losing your notes, and share skills without leaking your infrastructure.

---

Add whatever helps you do your job. This is your cheat sheet.

## Responding to Marcel (Chief of Staff)

Marcel manages this team on behalf of the CEO. When Marcel sends you a task or message, reply using `sessions_send` to his session key: `agent:main:main`

Always include your name and a brief status in your reply so Marcel can track progress.

## Sending Email to the CEO via Reed

You cannot send email directly. Reed (Email Agent) is the only agent authorised to send outbound email.

To have something emailed to the CEO (senthilrameshjv@gmail.com), send Reed a message using `sessions_send` at session key `agent:reed:main` in this format:

```
EMAIL REQUEST
FROM: Alex (PM)
TO: CEO (senthilrameshjv@gmail.com)
SUBJECT: [Subject line]
BODY:
[Your content here]

Reply to me at session key: agent:alex:main
```

Reed will send the email and confirm back to you. You can also route through Marcel — send your content to Marcel and ask him to forward it to Reed.