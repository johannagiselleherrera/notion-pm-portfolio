---
name: notion-pm-portfolio
description: |
  Builds a complete, professional Notion portfolio for Project Managers from scratch in one session. Runs a structured interview to collect all necessary information (personal info, bio, services, metrics, case studies, skills, testimonials, and optionally an AI workflows section), then creates a full portfolio page + 3 populated databases (Projects, Skills, Testimonials) directly in Notion via MCP. Use this skill whenever a PM wants to create, build, or set up a portfolio in Notion. Trigger on phrases like "build my PM portfolio", "create a portfolio page in Notion", "I want a Notion portfolio", "set up my portfolio as a project manager", "help me create a PM portfolio page", or any request to showcase PM work, case studies, or testimonials in Notion. Also trigger when someone mentions wanting a public PM page, a professional showcase, or a portfolio to share with recruiters or clients — especially if they mention Notion.
---

# Notion PM Portfolio Builder

You are helping a Project Manager build a complete, professional Notion portfolio. This is a two-phase process:
1. **Interview** — gather everything needed through a structured conversation
2. **Create** — build 1 portfolio page + 3 populated databases in Notion, all in one go

The result is a clean, minimal portfolio the PM can publish and share as a public link.

---

## Language

Detect the language the PM uses in their very first message and conduct the entire session in that language.

Keep ALL Notion page content — headings, labels, section titles, callout text, placeholder instructions — in **English**. The portfolio is public-facing and professional, so English content is always correct regardless of what language the PM is using.

---

## Phase 1 — Interview

Collect all the information below before doing anything in Notion. The goal is to feel like a smart colleague asking the right questions — not a form. Group related questions together naturally. Ask multiple things in one message. Match the PM's tone (casual or formal). If they're unsure about something, help them — suggest headline phrasing, give metric examples, propose service titles.

**Do NOT search Notion, do NOT create anything in Notion until Phase 2.** This phase is conversation only.

### Section 1 — Personal Info (ask first, all together)

Lead with these — they're quick and anchor everything else:
- Full name
- City and country
- Email address
- Phone / WhatsApp (with country code)
- LinkedIn profile URL
- Professional headline / tagline — the one-liner under their name. Help them craft one if needed. Examples: "Bilingual Project Manager | Agile Delivery · Project Recovery · AI-Augmented Workflows", "Senior PM | SaaS Delivery · Team Scaling · Stakeholder Alignment"
- Availability: full-time / part-time / contract, remote preferences, time zones

### Section 2 — About Me + Core Services

- Bio: 2–3 paragraphs. Should cover background/origin story, current specialization, and what makes them interesting as a PM
- 3 core services ("What I do best") — each needs a short title + 1–2 sentence description. Suggestions if they're stuck: Project Recovery, Agile Delivery Leadership, Process Optimization, Stakeholder Management, Distributed Team Leadership, AI-augmented PM workflows

### Section 3 — Key Metrics (exactly 3)

Three numbers that make their impact concrete:
- A value (e.g., "30%", "4 months", "10 team members", "$1.2M")
- A short description (e.g., "reduction in rework through sprint governance")

Prompt if they're stuck: "Think about your biggest wins — delivery speed, team size, cost savings, error reduction, client retention."

### Section 4 — Projects / Case Studies (1 to 3)

For each project:
- Title
- Client (or "Confidential" if preferred)
- Role
- Team composition
- Timeline
- Stack & Tools
- **The Challenge**: What was the situation when they got involved? (1 paragraph)
- **What They Did**: Bullet points, grouped by theme if applicable (e.g., *Technical realignment*, *Stakeholder management*, *Team recovery*)
- **Outcome**: Bullet points with ✅, quantified where possible
- **Reflection**: One sentence — "What this project says about how I work." Should feel authentic.

### Section 5 — Skills

Two lists:
- **Expertise**: Methodologies, domain knowledge, soft skills (e.g., Agile, Scrum, Risk Management, Roadmap Planning, Stakeholder Management, Project Recovery)
- **Tools**: Software and platforms (e.g., Jira, Confluence, Notion, Figma, Trello, Miro, Slack, Google Workspace)

### Section 6 — Testimonials (1 to 5)

For each:
- Reviewer full name
- Reviewer role + relationship context (e.g., "Full Stack Developer — worked under my direct supervision at Zafirus")
- Full quote text (verbatim)

### Section 7 — AI & PM Automation (optional)

Ask: "Do you use or build AI-powered tools or workflows in your PM work?"
- **Yes** → Ask: tools used, what they built or are building, current status. This becomes a dedicated section.
- **No** → Skip entirely. Never mention it again.

---

### Confirmation Step

Once all sections are collected, present a clean structured summary and ask:

> "Does everything look right? Any changes before I start building?"

**Do not proceed to Phase 2 until the PM confirms.**

---

## Phase 2 — Notion Creation

### Prerequisite: Verify Notion MCP Connection

Before doing anything, check whether Notion MCP tools are available in this session. Look for tools with `notion` in their name (e.g., `notion-create-database`, `notion-create-pages`, `notion-update-page`).

- **If Notion tools are available** → proceed immediately.
- **If Notion tools are NOT available** → stop and tell the PM:

> "To build your portfolio, I need access to your Notion workspace. Here's how to connect it:
> 1. Open **Claude Settings** (gear icon, top right)
> 2. Go to **Connectors** (or **Integrations**)
> 3. Find **Notion** and click **Connect**
> 4. Authorize access to your workspace
> 5. Come back here and say "ready" — I'll pick up right where we left off."

Do not proceed until Notion tools are confirmed available.

**Critical rules:**
- Use whichever Notion MCP tools are available in the session — do not hardcode specific tool IDs
- Always create **brand new** pages and databases — never search for existing ones, never modify or update existing Notion content
- Execute all steps in order
- If any individual step fails: log the error, inform the PM, and continue — never abort the whole process

---

### Step 1: Get Current Date

Check if a date/time MCP tool is available in the session (look for tools with `date`, `time`, or `datetime` in their name). If found, call it to get the current date. If no such tool is available, use the current date from context. Extract month and year for the footer (format: "Month YYYY", e.g., "April 2026").

---

### Step 2: Create Three Databases at Workspace Root

This step comes BEFORE creating the portfolio page. Use `notion-create-database` for each. Do NOT use a parent — these go at workspace root.

**Database 1 — Portfolio** (for case studies)
```
Name: "Portfolio"
Properties:
  - Name (title)
```

**Database 2 — Recommendations** (for testimonials)
```
Name: "Recommendations"
Properties:
  - Name (title)
  - Reviewer (rich_text)
```

**Database 3 — Skills**
```
Name: "Skills"
Properties:
  - Name (title)
  - Category (select, options: "Expertise", "Tools")
```

Save the URL returned for each database — you'll reference it in the manual steps summary.

---

### Step 3: Populate the Three Databases

Use `notion-create-pages` with the correct `data_source_id` parent for each database.

**Portfolio DB** — one page per case study:

```markdown
**Client:** [value]
**Role:** [value]
**Team:** [value]
**Timeline:** [value]
**Stack & Tools:** [value]

---

## The Challenge
[paragraph]

## What I Did
[bullet points, grouped by theme if applicable]

## Outcome
[✅ bullet points]

> **What this project says about how I work:** [reflection sentence]
```

**Recommendations DB** — one page per testimonial:
- `Name` = reviewer's full name
- `Reviewer` = reviewer's role + relationship context
- Page content: `> "[full quote text]"`

**Skills DB** — one page per individual skill:
- `Name` = the skill name (one per page — do not group)
- `Category` = `"Expertise"` or `"Tools"` (exact string match required)

---

### Step 4: Create the Main Portfolio Page

Use `notion-create-pages` at workspace root (no parent).

**Settings:**
- Title: `[Full Name] — Project Manager Portfolio`
- Icon: `🎯`

**Full page content** (copy this structure exactly, substituting the PM's information):

```markdown
<columns>
<column>
### [Full Name]

**[Headline]**

🌎 [Availability — e.g. "Remote-first · Full-time, part-time, and contract engagements across US, LATAM, and European time zones"]
</column>
<column>

*👤 Add your profile photo here — delete this placeholder text, type /image, and upload your photo. Right-click the image block to adjust the style so it sits cleanly next to your name.*

</column>
</columns>

<columns>
<column>
<callout icon="/icons/pin_gray.svg">
📍 [City, Country]
</callout>
</column>
<column>
<callout icon="/icons/mail_gray.svg">
[[email]](mailto:[email])
</callout>
</column>
<column>
<callout icon="/icons/phone-call_gray.svg">
[[phone]](tel:[phone-digits-only])
</callout>
</column>
<column>
<callout icon="/icons/link_gray.svg">
[[linkedin short display]](https://[full linkedin URL])
</callout>
</column>
</columns>

---

<columns>
<column>
## About Me

[bio paragraph 1]

[bio paragraph 2]

[bio paragraph 3 if provided]

## What I do best
</column>
<column>
</column>
</columns>

<columns>
<column>
**[Service 1 title]**
[Service 1 description]
</column>
<column>
**[Service 2 title]**
[Service 2 description]
</column>
<column>
**[Service 3 title]**
[Service 3 description]
</column>
</columns>

## Metrics

<columns>
<column>
**[Metric 1 value]**
[Metric 1 description]
</column>
<column>
**[Metric 2 value]**
[Metric 2 description]
</column>
<column>
**[Metric 3 value]**
[Metric 3 description]
</column>
</columns>

---

[INCLUDE THIS BLOCK ONLY IF PM SAID YES TO AI SECTION — otherwise skip it entirely]
## 🤖 AI & PM Automation

[AI content — what they use or build, tools, status]

---
[END AI BLOCK]

# Projects

*Click on any project card to open the full case study.*

*⚙️ **To display your projects here:** type `/linked` → "Create linked database view" → select "Portfolio".*

---

# Skills

*⚙️ **To display your skills here:** type `/linked` → "Create linked database view" → select "Skills".*

---

# Testimonials

[IF testimonials were originally in another language: *Originally written in [language] — translated for accessibility. Verifiable on LinkedIn.*]

*⚙️ **To display your testimonials here:** type `/linked` → "Create linked database view" → select "Recommendations".*

---

## Contact me!

Always open to new opportunities — full-time roles, contract engagements, or interesting one-off projects.

<columns>
<column>
<callout icon="/icons/mail_gray.svg">
**Email**
[[email]](mailto:[email])
</callout>
</column>
<column>
<callout icon="/icons/link_gray.svg">
**LinkedIn**
[[linkedin short display]](https://[full linkedin URL])
</callout>
</column>
<column>
<callout icon="/icons/phone-call_gray.svg">
**WhatsApp**
[[phone]](tel:[phone-digits-only])
</callout>
</column>
</columns>

*The fastest way to reach me is email or LinkedIn DM. I respond within 24 hours on weekdays.*

---

*Last updated: [Month YYYY]*
```

---

### Step 5: Deliver the Final Summary

After all steps complete, give the PM:

**What was created — direct links to all 4:**
- 🎯 Portfolio page: [URL]
- 📁 Projects database (Portfolio): [URL]
- 🛠️ Skills database: [URL]
- 💬 Testimonials database (Recommendations): [URL]

**3 manual steps to finish:**

> **1. Add your profile photo**
> Open the portfolio page. In the right column of the hero section, delete the italic placeholder text. Type `/image` and upload your photo. Right-click the image → adjust style so it's clean and aligned with your name block.

> **2. Link the 3 databases to the page**
> For each section (Projects, Skills, Testimonials):
> - Find the ⚙️ placeholder line
> - Delete it
> - Type `/linked` → "Create linked database view" → select the matching database (Portfolio / Skills / Recommendations)
> This embeds the live database view directly on your portfolio page.

> **3. Publish your portfolio**
> Click **Share** (top right of the page) → **Publish** → toggle **"Share to web"** on. Copy the public link — this is what goes on your CV and LinkedIn profile.

If any creation step failed, list those separately with clear notes on what to do manually.
