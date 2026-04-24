# Yoshi Labs — Claude Code Workspace

> Shared workspace for Bleuspace (hospitality), Yoshi Labs (AI consulting), and Agent Yoshi (AI agent SaaS).

## Project Overview

**Owner:** Prince Yoshiko Intes (CEO)
**AI Co-founder:** FINN (runs on Hermes, handles ops/monitoring/deployment via Telegram)
**You:** Claude Code — the builder. You write code, FINN reviews and deploys.

## Stack

- **Framework:** Next.js 16 (App Router), TypeScript
- **Styling:** Tailwind CSS 4
- **Deploy:** Vercel (connected to GitHub)
- **CRM:** GoHighLevel (GHL) — lead capture, booking
- **Payments:** PayMongo (PH market)
- **Database:** Supabase (Agent Yoshi)
- **AI Models:** GLM-4.7 (runtime), Claude Haiku (guest bot), Claude Sonnet/Opus (coding)

## Repos

| Repo | Path | Description |
|------|------|-------------|
| bleuspace-website | /root/bleuspace-website | Bleuspace.co hospitality site |
| agent-yoshi | /root/agent-yoshi | AI agent SaaS product |
| yoshilabs | /root/yoshilabs | Yoshi Labs parent site |
| bleuspace-calendar | /root/bleuspace-calendar-deploy | Content calendar v3 |

## Critical Rules

### Brand
- Bleuspace = premium + tech-forward. NOT generic templates.
- "AI Assistant" not "chatbot" — always.
- Mobile-first. Every page must look good on iPhone.
- Prince cares about visual quality. Make it look designed, not generated.

### Code Style
- Server Components by default. Client Components only for interactivity.
- No `console.log` in production code.
- Immutable patterns — spread operator, never mutate state.
- Use Zod schemas for all input validation.
- Type everything. No `any` unless absolutely necessary.

### Security
- Never hardcode API keys, tokens, or secrets.
- All env vars through `.env` or Vercel encrypted env.
- GHL_PRIVATE_TOKEN and VERCEL_TOKEN are in `~/.hermes/.env`.
- Never expose internal APIs to client-side code.

### Git Workflow
- Commit messages: conventional commits (`feat:`, `fix:`, `chore:`).
- Always `git pull` before starting work.
- Push to GitHub → FINN handles Vercel deploy.
- Never force push to main.

### Design Rules
- No purple hues as primary color.
- No emojis in production code or comments.
- Typography matters — use Inter or Space Grotesk.
- Proper spacing: 4px grid system.
- Animations: subtle and purposeful, never flashy.

## Architecture Decisions

1. **Bleuspace site:** Static Next.js + GHL API for leads. No CMS — content lives in `src/content/*.ts`.
2. **Agent Yoshi:** Next.js + Supabase + PayMongo. Chat UI primary, Telegram secondary.
3. **Build pipeline:** Claude Code → Onlook (visual customization) → Vercel deploy.
4. **Guest AI Assistant:** Connected to Guesty API. GLM-4.7 for responses. Escalates to Prince via Telegram.

## Key API Endpoints

- GHL Contacts: `https://services.leadconnectorhq.com/contacts/`
- GHL Booking: `https://api.leadconnectorhq.com/widget/booking/xssBfjIuAsjNwA3QBk79`
- Bleuspace lead form: `/api/submit-lead`
- Vercel API: `https://api.vercel.com/v9/projects/`

## Working with FINN

FINN is the co-founder running on Hermes. He monitors the system via cron jobs.
- Code reviews: FINN reads diffs and flags issues via Telegram
- Deploys: FINN runs `vercel --prod` after Prince pushes to GitHub
- Issues: FINN creates GitHub issues for bugs found in monitoring
- Communication: All FINN messages go to Prince via Telegram (DM: 7686310733)

## File Structure (Bleuspace)

```
src/
  app/
    page.tsx              # Homepage
    list-your-property/   # Hot lead form
    property-management/  # Hot lead form
    resources/            # Warm lead form + pricing guide
    contact/              # General lead form
    pricing/              # Tier comparison
    api/
      submit-lead/        # GHL integration endpoint
  components/
    ui/                   # Shared UI components
    sections/             # Page sections
    forms/                # Lead capture forms
  content/
    *.ts                  # Static content data
  lib/
    ghl.ts               # GHL API helpers
    utils.ts             # Shared utilities
```

## gstack

gstack is installed at `~/.claude/skills/gstack/`. Use it for all builds.

Available skills: /office-hours, /plan-ceo-review, /plan-eng-review, /plan-design-review, /design-consultation, /design-shotgun, /design-html, /review, /ship, /land-and-deploy, /canary, /benchmark, /browse, /connect-chrome, /qa, /qa-only, /design-review, /setup-browser-cookies, /setup-deploy, /retro, /investigate, /document-release, /codex, /cso, /autoplan, /plan-devex-review, /devex-review, /careful, /freeze, /guard, /unfreeze, /gstack-upgrade, /learn.

**Build pipeline:** /office-hours → /autoplan → build → /review → /qa → /ship

Use /browse for all web browsing. Never use mcp__claude-in-chrome__* tools.

## PH Market Context

- Currency: Philippine Peso (₱)
- Target: Service businesses ₱100K-₱500K/mo revenue
- Price sensitivity: ₱5K/mo is the sweet spot for retainer
- Language: English for business, Tagalog optional for warmth
- Payment: PayMongo (GCash, Maya, credit card)
