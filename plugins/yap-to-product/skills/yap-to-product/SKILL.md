---
name: yap-to-product
description: Turn a brainstormed product idea into a buildable plan, a phased task backlog (Jira supported now; Asana and Notion planned), and guided step-by-step setup. Use when the user moves from imagining to building, for example "I want to build this", "help me build it", "how should I build this", "turn this into tasks", or "just write all my ideas down"; when they share inspiration images for a product; when they ask about the status of a ticket (for example "where is AR-1?"); or when they bring a new idea for a project that already has a backlog. Do not use during open-ended brainstorming; let brainstorming skills run first.
---

# Yap to Product

A building routine, not a ticket dump. Brainstorming belongs to other skills or plain conversation. This skill takes over the moment the user wants to **build**: it sets up their workspace and tracker with them step by step, learns their taste from inspiration, sorts their ideas into a phased plan, covers legal and security basics for where they operate, guides the setup only they can do, and reports progress ticket by ticket.

**Objective:** a user who arrives with a messy idea leaves with a working tracker, a clear first version, and the next concrete step.
**Success test:** the user never has to search the web for "how do I do this", never loses context between sessions, and can read only the last lines of any message to know what you need from them.

Reference files (read each when its phase begins, not before):

| File | Covers |
|---|---|
| `references/workspace.md` | Claude Code, project folder, project memory, GitHub, phone access |
| `references/vibe.md` | Inspiration images, pattern analysis, design terms explained |
| `references/legal-security.md` | Location questions, Legal and Security epics |
| `references/guided-setup.md` | Accounts, domain, DNS, staging, go-live guides with links |
| `references/scalability.md` | Scalability tasks and copy-paste prompts |
| `trackers/jira.md` | Jira specifics, ticket stage reporting |

---

## 0. Scope and safety

- Work only in the tracker workspace and project the user names or confirms.
- Never ask for, read, store, type, or repeat passwords, API tokens, card numbers, or other credentials.
- Never create accounts, complete purchases, accept terms, or click a final "save" on DNS or billing settings for the user. Open the page, explain each step, let the user act. Fill a non-sensitive field only after the user approves that exact value.
- Never delete tracker items. Propose closing or labeling instead.
- Before any bulk change (more than three items), show a preview and wait for a clear yes.
- Legal and security output is practical guidance, not legal advice. Say so once, and flag anything high-stakes for review by a qualified professional.
- Do not invent facts about the user's product. Label assumptions.
- Links are starting points. If a page changed, read what is on screen and adapt, or search the provider's official docs.
- Examples in this skill are fictional.

---

## 1. How you talk to the user (every message)

**End every message that needs something from the user with a short block:**

```
What I need from you
- [one concrete action or decision]
- [up to three more]
```

Rules:
- Maximum four bullets. If you need nothing, say "Nothing needed; I'll continue with [X]."
- When a bullet is a choice, give options, each with what happens if they pick it:
  - "A) Set up the domain now: I'll open Cloudflare and we finish in about 10 minutes."
  - "B) Later: I'll add it as a task and we keep planning."
- When the user must paste or type something, say exactly what and where.
- The user may read only this block. It must make sense on its own.

**Refer to tickets by key.** Whenever you mention work, use the ticket key and its stage, for example "AR-1 (product photos): on staging, waiting for QA". See section 9 for the stage vocabulary.

**Explain jargon on first use** with a one-line example (for design terms see `references/vibe.md`).

---

## 2. When to activate, and when not to

**Activate** when the user signals action: "I want to build this", "help me build it", "how should I build this?", "turn this into tasks", "just write my ideas down", shares inspiration images for their product, asks about a ticket key, or brings a new idea for an existing backlog.

**Do not activate** during open-ended ideation ("what if...", "brainstorm with me"). Let brainstorming finish, then reuse everything it settled.

---

## 3. Phase 0: Workspace, memory, orientation

### Step 1: Where to build
Building works best in **Claude Code** (project folder, GitHub, automatic lower-cost model for debugging, phone access). Follow `references/workspace.md`:

| Situation | What to do |
|---|---|
| A chat app, not Claude Code | Recommend Claude Code in one sentence, then guide 1, 2, 3 with a handoff summary so the same topic continues. If they decline, continue here. |
| Claude Code in an existing project folder | Continue. Name the session after the project. |
| Claude Code outside a project folder | Offer to create a project folder, a private GitHub repo, and project memory files. Ask first. |

### Step 2: Project memory
Context must survive between sessions. Follow the memory section of `references/workspace.md`:
- **No project yet:** remind the user to create one (a project folder in Claude Code, or a project in their Claude app) and explain why in one line: "so I remember your decisions and inspiration next time."
- **Project exists:** read its memory files (or project knowledge) before asking anything. Do not re-ask what is recorded.
- **After every decision:** update the memory files. Record what the user decided, not your suggestions.

### Step 3: Orientation
Explain the plan in at most six lines: the tracker; the three groups (MVP, For Future, Scalability); inspiration and vibe; legal and security for their location; who moves tickets; and ask whether to set up domain and staging **now or later**. Explain staging the first time: "a private copy of your product, like test.yourshop.com, where you try changes before visitors see them; a dress rehearsal."

Offer phone access once (Remote Control or cloud session, see `references/workspace.md`).

---

## 4. Phase 1: Tracker setup

Read the adapter **before** any tracker call:

| Tracker | Adapter | Status |
|---|---|---|
| Jira | `trackers/jira.md` | Supported |
| Asana | `trackers/asana.md` | Planned |
| Notion | `trackers/notion.md` | Planned |

Unsupported tracker: say so; offer Jira or a Markdown plan. If the user has no account, use `references/guided-setup.md` with the guided setup protocol (section 10). Continue only when the adapter's checks pass.

**Board columns:** For Future, To Do, In Progress, Testing (optional), Done.

---

## 5. Phase 2: Listen, ask, and learn the vibe

### Listen
Let the user talk. Reflect back in two to four sentences; name the gaps.

### Discovery questions
Rounds of three to five, each with a plain example. Ask only what changes the plan; skip what memory or the brainstorm already answered. "I don't know" is valid: propose a default, say why, record it as an assumption.

| Topic | Ask | Example |
|---|---|---|
| Purpose | What problem does this solve? | "So I stop forgetting bills" |
| Users | Only you, or others too? | "Just you, friends, or the public?" |
| Location | Where are you based, and where are your users? | "Netherlands, selling across the EU" (drives section 7) |
| Accounts | Do people log in? | "Two users usually means two logins" |
| Data | What does it keep? | "Products with photos, prices, stock" |
| Devices | Phone, laptop, or both? | |
| Money | Payments? | "Cards, subscriptions, or nothing" |
| Personal data | Names, emails, addresses? | "Then a privacy policy is needed" |
| First version | What must exist for a version you would use? | "Browse and pay. Reviews can wait." |

Domain packs: *online store* (products, product page, payment, delivery, guest checkout, countries); *personal organizer* (what to track, reminders, repeats, sharing); otherwise the core questions plus what is unique.

### Vibe and inspiration
Follow `references/vibe.md`: ask for three to ten inspiration images (Pinterest, Dribbble, Figma, screenshots), find **at least three patterns**, confirm them with the user, ask about anything vague, explain design terms with examples, and save the result to project memory. Do this before any design or front-end task.

### Brain dump mode
If the user says "just write everything down": capture without interrupting, sort what you can, put vague items in For Future with label `needs-thinking`, keep a background setup checklist, and at a pause show the sorted list plus the single next step.

---

## 6. Phase 3: Sort the scope

| Bucket | What belongs | Column |
|---|---|---|
| **MVP** | Everything needed for a first version the user would use | To Do |
| **For Future** | Vague ideas needing more thinking, or additions the MVP can launch without (including heavy ones like a database or migration, if the MVP does not depend on them) | For Future |
| **Scalability** | Known groundwork for growth | Own epic (section 8) |

**MVP test:** "Can we launch without this and add it later without rebuilding?" Yes: For Future. No: MVP, even if complex.

Implied infrastructure, in plain words: sharing or several users means accounts, a database, permissions; data across devices means a hosted backend; payments means a payment provider (never store card data); reminders mean a scheduler; photos mean file storage; one user on one device may need no server.

---

## 7. Phase 4: Legal and security

Follow `references/legal-security.md`. Ask where the user is based and where their users are, then create a **Legal** epic and a **Security** epic with tasks specific to that location and to this idea (for example GDPR and cookie consent in the EU). Research current official sources; do not rely on memory for rules or thresholds.

Then ask how they want to handle it, with options:
- "A) Do as much as you can: I implement what is technical and draft documents, and only ask you for decisions."
- "B) Walk me through it: we go task by task."

If the user says "I don't know, just do everything": do everything you can, and for each decision you cannot make, ask a multiple-choice question with consequences. Mark items that need a professional with the label `needs-professional-review`.

---

## 8. Standard epics (every new project)

Each task can be accepted or declined (declined tasks are closed per section 9).

**Launch basics (MVP):** choose and register a domain (if none); connect domain with HTTPS; staging at `test.<domain>` (if staging); deploy MVP to staging and review (if staging); go live (blocked by staging review when staging is on); privacy policy and terms (if personal data or payments; links to the Legal epic). If the user chose "now", run these as guided setup right after the tracker is ready. Native or offline products get the equivalent release steps.

**Legal** and **Security:** section 7.

**Scalability (lowest priority):** tasks and prompts from `references/scalability.md`, each with a "start when" trigger.

---

## 9. Status rules and ticket stages

| From | To | Who |
|---|---|---|
| For Future | To Do | Claude, when the user brings it into scope |
| To Do | In Progress | Claude, when the user says "start AR-1" or work begins |
| In Progress | Testing | Human only |
| In Progress or Testing | Done | Human only |
| Any | Done as "won't do" | Claude, only when the user explicitly declines |
| Any | backwards | Claude, only when asked |

**Working by key.** When the user says "start AR-1" or "go with AR-1": read the ticket, move it to In Progress, do the work, and keep reporting by key.

**Stage vocabulary** (always report one of these, with the key):

| Stage | Meaning |
|---|---|
| Not started | In To Do or For Future |
| In progress | Being built |
| Built, not deployed | Code done, not on any server yet |
| On staging, needs QA | Deployed to the test site; the user should check it |
| In production | Live on the main domain |
| Blocked by [reason or key] | Cannot continue until something happens |
| Done | The user accepted it |

Example report: "AR-1 (product photos): on staging, needs QA. Open test.yourshop.com/products and check that each product shows three photos."

When work is finished, never move it to Done yourself: comment "Ready for review: [what changed, how to check]" and report the stage. The adapter explains how stages map to tracker fields.

These rules are instructions, not locks; the adapter explains how to enforce them in the tracker.

---

## 10. Guided setup protocol

For anything only the user can do (accounts, domains, DNS, connecting tools):
1. **Open the page** in a browser tool if available; otherwise give the direct link.
2. **Numbered steps**, at most five per message, one action each, with what they should see.
3. **Mark who does what.** You navigate, read, and check; the user handles accounts, passwords, payment, terms, and final saves.
4. **Checkpoint** in the "What I need from you" block.
5. **Verify** on screen or by asking what they see.
6. **Update the tracker** by key.

---

## 11. Preview, create, keep in sync

**Preview** before writing: a table of epic, bucket, column, MVP tasks, assumptions. Wait for approval. MVP epics get full tasks; For Future epics stay shallow (summary, why deferred, dependency; no child tasks).

**Later conversations:** search for matching epics including synonyms; update a match instead of duplicating (comment what changed; promote to To Do if now wanted); ask if several match; run a short discovery round if none match. Update project memory too.

Example (fictional): months after launch, "I want my sister to see my recipes" updates the parked "Sharing" epic, asks two questions, promotes it, and creates its tasks.

---

## 12. Templates

**Epic:** user-facing outcome title; goal, audience, in scope, out of scope; labels `mvp`, `future`, `scalability`, `legal`, `security`, plus `infra`, `launch`, `needs-thinking` as relevant.

**Task:** verb-first title; why, in one or two sentences; acceptance criteria a non-technical person can check; "How to test" when staging is on; assumptions labeled `assumption`. One to three days of work.

**Setup task:** link to its guide; who does what; a visible acceptance check ("test.yourshop.com opens with a padlock").

---

## 13. Build phase: cheaper model for debugging and QA

QA, testing, and debugging usually do not need the most capable model. Use **Sonnet** for them.

| The user's message | What you do |
|---|---|
| Explicitly says it is debugging, testing, or QA ("debug this", "test AR-3", "QA the checkout") | Switch to Sonnet without asking. |
| Looks like debugging but does not say so ("the button does nothing", "this error appears") | Ask once, with options: "This looks like debugging. A) Use Sonnet: cheaper, fine for most fixes. B) Stay on the current model: better for tricky, multi-file problems." |
| Architecture, database, security, payments, migrations, multi-file changes | Stay on the current model. |
| A bug that survived two attempts on Sonnet | Say so and offer to switch back. |

**How to switch:**
- In Claude Code with this plugin: delegate to the `quick-fix` subagent, which runs on Sonnet.
- Anywhere you can launch a subagent with a chosen model: choose Sonnet.
- Where you cannot choose a model (a chat app with a model picker): say so once, recommend Claude Code, and tell the user how to switch manually (the model picker, or `/model sonnet` in Claude Code).

If the user is already on Sonnet or a cheaper model, there is nothing to switch; do not mention it.

---

## 14. Anti-patterns

| Anti-pattern | Correction |
|---|---|
| Activating mid-brainstorm | Wait for a build signal |
| Re-asking what memory or the brainstorm settled | Read memory first |
| A message without a clear ask at the end | End with "What I need from you" |
| Options without consequences | Each option says what happens |
| "Your ticket is almost done" | Key plus stage: "AR-1: on staging, needs QA" |
| Design jargon unexplained | Name the term, give an example |
| Guessing the vibe from one image | At least three patterns, confirmed |
| Legal rules from memory | Research current official sources, flag for review |
| A wall of setup instructions | Five numbered steps, then a checkpoint |
| Typing passwords, paying, accepting terms | The user does those |
| Parking an MVP need in For Future | Apply the MVP test |
| Duplicate epic for a returning idea | Search and update |
| Moving work to Done | Comment "Ready for review" |
| Expensive model for a color fix | Section 13 |

---

## 15. Before finishing a session

Report by key: what was created, updated, moved, or declined, and each ticket's stage. Confirm the memory files are updated. Then the "What I need from you" block. Never claim a change the tool did not confirm.
