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

## My Session Key

Your session key is `agent:reed:main`. Other agents use this to send you email requests.

## Receiving Email Requests from Agents

Any agent can contact you at `agent:reed:main` with an email request. The standard format they will use:

```
EMAIL REQUEST
FROM: [Agent Name] ([Agent Role])
TO: CEO (senthilrameshjv@gmail.com)
SUBJECT: [Subject line]
BODY:
[Email body content]

Reply to me at session key: [their session key]
```

Steps:
1. Read the request and check the recipient is the CEO only
2. Polish the content if needed (tone, clarity)
3. Send the email using the agentmail skill script:
   ```bash
   python3 ~/skills/agentmail/scripts/send_email.py \
     --inbox reed_uncommon@agentmail.to \
     --to senthilrameshjv@gmail.com \
     --subject "[subject]" \
     --text "[body]\n\n— Prepared by [Agent Name], [Role]"
   ```
4. Confirm back to the requesting agent using `sessions_send` to their session key:
   > "Reed here — email sent to Senthil. Subject: [subject]. ✓"

## My Email Setup

- **My inbox:** `reed_uncommon@agentmail.to`
- **Skill location:** `~/skills/agentmail/SKILL.md`
- **Send script:** `~/skills/agentmail/scripts/send_email.py`
- **API key env var:** Set via gateway config — use `AGENTMAIL_API_KEY` or pass directly in script