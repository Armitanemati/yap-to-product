# Legal and security

Practical guidance to build responsibly, not legal advice. Say that once to the user. Rules and thresholds change: **research current official sources every time** (government and regulator sites first) and cite them in the ticket. Never state a legal requirement from memory alone.

---

## 1. Ask about location

Two questions, separately:
1. "Where are you (or your business) based?"
2. "Where are your users or customers?" Example: "You live in the Netherlands but sell to all of Europe, so EU rules apply."

Also note anything that raises the stakes: children as users, health or financial data, payments, user-generated content, AI features, employees.

---

## 2. Create the epics

Create two epics in To Do: **Legal** (label `legal`) and **Security** (label `security`). Fill them with tasks that apply to **this** idea and **these** locations. Each task: what it is in plain words, why it applies here, the official source you checked, and label `needs-professional-review` when a mistake would be costly.

### Legal: topics to check (pick what applies, verify each)

| Region | Topics to research |
|---|---|
| EU / EEA | GDPR (privacy notice, lawful basis, data subject rights, processor agreements with vendors, breach handling); cookie consent rules; consumer protection for online sales (pre-contract information, withdrawal rights, price display); VAT for cross-border sales; accessibility requirements for digital products and e-commerce; platform rules if users post content; AI transparency rules if the product uses AI |
| United Kingdom | UK GDPR and the UK cookie rules; consumer contract rules for online sales |
| United States | State privacy laws where users live; children's privacy if minors may use it; accessibility expectations; sales tax |
| Everywhere | Terms of use; privacy policy; payment provider terms; trademark check on the product name; licenses of any third-party code, fonts, or images |

### Security: baseline tasks (adapt to the stack)

| Task | Plain explanation |
|---|---|
| HTTPS everywhere | The padlock; encrypts traffic |
| Use a trusted login provider | Do not build password storage from scratch; offer two-step login where it matters |
| Secrets out of the code | Passwords and keys live in environment settings, never in the repository |
| Least privilege | Every account and service gets only the access it needs |
| Input validation | Never trust what users type; protects against common attacks (see the OWASP Top 10: https://owasp.org/www-project-top-ten/) |
| Dependency updates | Keep libraries updated; enable automated alerts in GitHub |
| Backups and restore test | Copies of data, and proof that restoring works |
| Logging without personal data | Record errors, not passwords or private details |
| Payments through a provider | Card data never touches your servers |
| Rate limiting | Stop bots from hammering login or forms |

---

## 3. Ask how they want to handle it

Ask with options:
- "A) Do as much as you can: I implement the technical parts (cookie banner, security headers, secret handling) and draft documents (privacy policy, terms), and only ask you for decisions."
- "B) Walk me through it: we go task by task and I explain each."

If the user says "I don't know, just do everything": choose A. Do everything you can. For each decision only they can make, ask a multiple-choice question with consequences, for example:

"Which analytics should the site use?
- A) None: no cookie banner needed for analytics; you know less about visitors.
- B) Privacy-friendly analytics without cookies: often no consent banner needed (I will check the current rules for your countries).
- C) Google Analytics: detailed data; requires a consent banner in the EU."

Drafted legal documents always get `needs-professional-review` and a note that a lawyer or advisor in the user's country should check them before launch.
