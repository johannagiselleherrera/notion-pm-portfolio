# notion-pm-portfolio

A reusable Claude skill that builds a complete, professional Notion portfolio for Project Managers — from scratch, in one session.

## What it does

Runs a structured conversational interview with the PM, then automatically creates:

- **1 portfolio page** — hero section, about me, services, metrics, case studies, skills, testimonials, and contact
- **3 Notion databases** — Portfolio (case studies), Skills, Recommendations (testimonials)

No forms. No copy-pasting. One confirmation, then Claude builds everything directly in Notion.

## Requirements

- [Claude](https://claude.ai) with the Skills plugin enabled
- Notion connected to Claude via MCP (Model Context Protocol)

> **How to connect Notion:** Claude Settings → Connectors → Notion → Connect → Authorize your workspace.

## Installation

1. Download `notion-pm-portfolio.skill` from [Releases](../../releases)
2. In Claude, open the Skills panel and install the `.skill` file
3. Start a new conversation and say: *"Build my PM portfolio in Notion"*

Alternatively, clone this repo and load `SKILL.md` directly if your setup supports it.

## How it works

### Phase 1 — Interview

Claude collects everything needed through natural conversation, grouped into 7 sections:

| Section | What's collected |
|---|---|
| Personal info | Name, location, contact details, headline, availability |
| About me + services | Bio (2–3 paragraphs), 3 core services with descriptions |
| Key metrics | 3 quantified impact numbers |
| Case studies | 1–3 projects: challenge, actions, outcomes, reflection |
| Skills | Expertise (methodologies, soft skills) + Tools (software) |
| Testimonials | 1–5 reviews with reviewer name, role, and full quote |
| AI workflows *(optional)* | Tools used, what was built, current status |

Claude presents a full summary and asks for confirmation before touching Notion.

### Phase 2 — Creation

Once confirmed, Claude:

1. Checks that Notion MCP tools are available (and guides connection if not)
2. Creates 3 databases at workspace root (Portfolio, Skills, Recommendations)
3. Populates each database with the PM's content
4. Creates the main portfolio page with the full layout
5. Delivers direct links to all 4 items + 3 manual steps to finish

### Manual steps after creation

Three things Claude can't do via API — done in under 5 minutes:

1. **Add your profile photo** — delete the placeholder, type `/image`, upload
2. **Link the databases** — type `/linked` → "Create linked database view" → select the matching DB for each section
3. **Publish** — Share → Publish → Share to web → copy the public link

## Language support

Claude auto-detects the PM's language and conducts the interview in it.
All Notion content (headings, labels, callout text) is always written in **English** — the portfolio is public-facing and professional.

## Customization

The skill is designed to be generic and portable. To adapt it:

- Edit `SKILL.md` directly — it's plain Markdown with a YAML frontmatter
- Modify the page template in Phase 2 → Step 4 to change layout or sections
- Add or remove interview sections in Phase 1 as needed

## File structure

```
notion-pm-portfolio/
├── SKILL.md          # The skill — instructions for Claude
├── evals/
│   └── evals.json    # Test cases used during development
└── README.md
```

## Contributing

Pull requests welcome. If you adapt this for a different role (designer, engineer, consultant), open a PR or fork it — just update the `name` and `description` fields in the SKILL.md frontmatter.

## License

MIT
