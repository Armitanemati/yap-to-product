# Workspace: Claude Code, project folder, memory, GitHub, phone

Use with the guided setup protocol in `SKILL.md` section 7: at most five numbered steps per message, then a checkpoint. Commands here were current when written; if one fails, check the official docs at https://code.claude.com/docs and adapt. Never ask for or type passwords or tokens.

---

## 1. Moving from a chat app to Claude Code

Say why in one sentence: "Claude Code can create your project folder, save it to GitHub, use a cheaper model for small fixes automatically, and let you continue from your phone."

### Handoff summary (write this first)
Write a short summary the user will paste as their first message in Claude Code, so the same topic continues without repeating anything:

```
Continue my project "[PROJECT NAME]" with the yap-to-product skill.
Idea: [one to three sentences]
Decisions so far: [users, accounts, data, look and feel, payments, MVP scope]
Tracker: [Jira site and project key, or "not set up yet"]
Domain and staging: [now or later; domain if known]
Open questions: [list]
```

Offer to save it as a file the user can download, too.

### Steps for the user
Requirements: a paid Claude plan (Pro, Max, Team, or Enterprise) or a Claude Console account. Quickstart: https://code.claude.com/docs/en/quickstart

1. **Install Claude Code.** Open a terminal (Mac: Terminal app; Windows: PowerShell) and paste the install command:
   - Mac or Linux: `curl -fsSL https://claude.ai/install.sh | bash`
   - Windows PowerShell: `irm https://claude.ai/install.ps1 | iex`
   Then close the terminal, open a new one, and run `claude --version`. You should see a version number.
2. **Create the project folder and start Claude Code there**, using a short lowercase name without spaces:
   - Mac or Linux: `mkdir -p ~/projects/plant-tracker && cd ~/projects/plant-tracker && claude -n plant-tracker`
   - Windows PowerShell: `mkdir $HOME\projects\plant-tracker; cd $HOME\projects\plant-tracker; claude -n plant-tracker`
   The first time, it asks you to log in through your browser.
3. **Install this plugin** inside Claude Code (once per computer):
   `/plugin marketplace add Armitanemati/yap-to-product`
   `/plugin install yap-to-product@yap-to-product`
4. **Paste the handoff summary** as your first message.
5. Reply in the new session; it continues from there.

Next time, return to the same conversation from the project folder with `claude -c` (most recent) or `claude --resume plant-tracker` (by name).

(Replace `plant-tracker` with the project's name and `OWNER` with the repository owner of this plugin.)

---

## 2. Creating a project folder and GitHub repository (inside Claude Code)

Ask first: "Shall I create a project folder and a private GitHub repository for this? You can make it public later."

Then, with the user's approval:
1. Create the folder (for example `~/projects/<name>`) and move the session there (`/cd`, or ask the user to restart Claude Code inside it).
2. Initialize git, and write `docs/brief.md` with the handoff summary and `README.md` with the project name and one-line purpose. Add a `.gitignore` suitable for the stack, which always ignores `.env` and secret files.
3. If the GitHub CLI is installed and logged in (`gh auth status`), create the repository as **private** and push: `gh repo create <name> --private --source=. --push`. Confirm the name with the user before running it.
4. If `gh` is missing or not logged in, guide the user instead:
   - Install the GitHub CLI: https://cli.github.com, then the user runs `gh auth login` themselves.
   - Or create the repository in the browser: https://github.com/new (private, no README), then add the remote and push with the commands GitHub shows.
5. Confirm by opening the repository page, and tell the user its link.

Never make a repository public without an explicit request. Never commit secrets.

---

## 3. Project memory

Context must survive between sessions, devices, and model switches. Memory lives in files the user owns, not in your head.

### In Claude Code (a project folder)
Create these with the user's approval, and keep them current:

| File | Holds | Update when |
|---|---|---|
| `CLAUDE.md` (project root) | Ten lines at most: what the product is, tracker site and project key, where the memory files are, current focus. Claude Code loads this file automatically at the start of every session. | Focus or key facts change |
| `docs/brief.md` | The handoff summary: idea, users, location, scope, decisions | A product decision is made |
| `docs/vibe.md` | Inspiration list, confirmed patterns, design direction (`references/vibe.md`) | New inspiration or a design decision |
| `docs/decisions.md` | Dated log: decision, reason, who decided | Every decision, one line each |
| `docs/inspiration/` | The inspiration images | The user shares images |

Rules: record what the **user** decided, not your suggestions. Keep entries short. Never store passwords, keys, or personal data about the user's customers in these files. Commit the files to the project's repository so they travel with it (including to cloud sessions).

### In a Claude chat app
- If the user has no project: remind them to create one in the app and add their materials (brief, inspiration images) to it, so future chats in that project start with the same context.
- If they work in a project: read its knowledge before asking anything.
- Offer the brief and design direction as files they can add to the project after each major decision.

### On every return
Read the memory first. Summarize in two lines where things stand (by ticket key and stage), then continue. Do not re-ask anything recorded.

---

## 4. Phone access

Two ways. Explain the difference in one line each, then guide the one the user picks.

| Option | How it works | Use when |
|---|---|---|
| **Remote Control** (recommended) | The session keeps running on the user's computer; the phone becomes a remote screen. All local files, plugins, and the tracker connection keep working. | The computer can stay on, with Claude Code running. |
| **Cloud session** | The work runs in the cloud on the GitHub repository. Continues with the laptop closed. | The computer will be off. Plugins installed on the computer do not load there; copy the skill into the repository's `.claude/skills/` folder if it should travel. |

Docs: https://code.claude.com/docs/en/remote-control and https://code.claude.com/docs/en/mobile

### Remote Control steps
1. Install the Claude app on your phone (iOS or Android) and sign in with the same account. In Claude Code, `/mobile` shows a QR code that opens the right app store.
2. In this Claude Code session, run `/remote-control`. Or start a fresh one in the project folder with `claude remote-control`.
3. Scan the QR code shown in the terminal, or open the Claude app, tap **Code**, and pick this session.
4. Keep the computer on and Claude Code running. If it sleeps, the session reconnects when it wakes.
5. Send a test message from the phone. Reply "done" when it appears here.

Tip: ask Claude to notify you when a long task finishes; Remote Control can send push notifications to the phone.

### Cloud session steps
1. Make sure the project is pushed to GitHub (section 2).
2. Follow the cloud quickstart to connect GitHub: https://code.claude.com/docs/en/web-quickstart
3. In the Claude app, tap **Code**, choose the repository and branch, and describe the task.
4. Pull the results to the computer later with `git pull`.
