# Guided setup guides

Use these with the guided setup protocol in `SKILL.md` section 7: open the page, give at most five numbered steps, checkpoint, verify, update the tracker.

Provider pages change. Treat every link and step here as a starting point: if the screen looks different, read it and adapt. If a link fails, search the provider's official documentation. Never ask for or type passwords, card details, or API tokens.

---

## A. Claude in Chrome (optional, makes everything else easier)

Lets Claude open pages and read what the user sees, so the user does not have to hunt for settings.

- Page: https://claude.com/chrome
- Mention it once, only if no browser tools are available. It is a beta extension for paid Claude plans; check the page for current availability.
- Steps for the user: open the page, select "Add to Chrome", follow the prompts, grant access only to sites they trust.

## B. Jira account (free plan)

- Page: https://www.atlassian.com/software/jira/free (free for small teams; check the page for current limits)

Steps:
1. Open the page and choose the free plan.
2. Sign up with your email (you type it; I never do).
3. Pick a site name. This becomes your web address, like yourname.atlassian.net. Short and lowercase is easiest.
4. When Jira asks about a template, choose **Kanban** (simplest for one person or a small team).
5. Reply "done" when you see your empty board.

## C. Jira project statuses

Goal: columns **For Future**, **To Do**, **In Progress**, **Testing** (only if staging is on), **Done**.

Menu names differ between project types and change over time, so read the screen and guide from what is there. Typical path in a team-managed project:
1. Open the board.
2. Open the board or workflow settings (often a "..." menu near the board title, or "Project settings").
3. Add a status or column named **For Future** and place it before To Do.
4. If staging is on, add **Testing** between In Progress and Done.
5. Reply "done" when the board shows all columns in order.

## D. Connect Jira to Claude

The connection method depends on where the user runs Claude, and it changes over time. Look up the current official instructions instead of relying on memory:
- Claude apps: search the Claude Help Center (https://support.claude.com) for "Atlassian" or "connectors".
- Claude Code: search Atlassian's documentation for its remote MCP server, or the Claude Code docs (https://code.claude.com/docs) for "MCP".

Then guide in numbered steps. The user approves the sign-in screen themselves. Verify by listing their visible projects.

## E. Buy a domain (example: Cloudflare Registrar)

Cloudflare is one option; any reputable registrar works. If the user already has a domain, skip to F.

- Sign up: https://dash.cloudflare.com/sign-up
- Register page: https://dash.cloudflare.com/?to=/:account/registrar/register
- Docs: https://developers.cloudflare.com/registrar/get-started/register-domain/

Steps:
1. Create a Cloudflare account and **verify your email** (registration needs a verified email).
2. On the Register page, type the name you want and select Search.
3. Pick an available domain and select Purchase. Choose how many years.
4. Enter your contact details and payment yourself, review the terms, and complete the purchase.
5. Reply "done" when you get the confirmation email.

Before step 4, remind the user: check the renewal price, not only the first-year price.

## F. Connect the domain to hosting, with HTTPS

First ask where the product is hosted. Open that host's "custom domain" documentation; the host tells you which DNS records to add.

- Cloudflare DNS records page: https://dash.cloudflare.com/?to=/:account/:zone/dns/records
- Docs: https://developers.cloudflare.com/dns/manage-dns-records/how-to/create-dns-records/

Steps:
1. In your hosting dashboard, add your domain as a custom domain. Note the record it asks for (type, name, value).
2. In Cloudflare, open DNS > Records and select **Add record**.
3. Choose the type the host asked for (usually CNAME or A) and paste the name and value exactly.
4. Select Save (you click it).
5. Wait a few minutes, then open your domain. Reply "done" when it loads with a padlock icon.

If the padlock is missing after an hour, check the host's HTTPS setting.

## G. Staging site at test.yourdomain

Steps:
1. In your hosting dashboard, create a second environment or deployment for staging (often called "preview" or "staging").
2. Add the custom domain `test.yourdomain.com` to that environment and note the record it asks for.
3. In Cloudflare DNS, add that record with the name `test`.
4. Protect staging so strangers and search engines do not find it (password protection if the host offers it, or a "noindex" setting).
5. Reply "done" when test.yourdomain.com opens and shows the staging version.

## H. Go live

Only after the staging review passes:
1. Confirm the staging version is the one you want live.
2. Promote or redeploy it to the production environment (the host's "promote" or "deploy to production" action).
3. Open the main domain and check the key pages.
4. Reply "done" and move the Go live task to Testing or Done yourself.

## I. Privacy policy and terms

Needed when the product collects personal data or takes payments. Do not write legal guarantees. Offer to draft a plain-language first version from what the product actually collects, and tell the user to have it reviewed for the countries they serve.
