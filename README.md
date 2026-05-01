# Lead Intelligence Pipeline

Multi-node agentic intake system for home service operators. Classifies inbound requests through four sequential AI nodes — intent, urgency, enrichment, routing — and outputs a structured lead card with CRM assignment and action decision.

**Live:** [deploy URL here]

---

## Architecture

Four discrete Claude API calls, each with scoped context and typed output. Each node receives prior state, building signal progressively — mirroring a LangGraph `StateGraph` pipeline.

```
Intake Request
     │
     ▼
[Intent Classifier] → serviceCategory, issueType, confidence
     │
     ▼
[Urgency Engine]    → urgency, safetyRisk, timeline, flags
     │
     ▼
[Lead Enrichment]   → estimatedValue, intentStrength, jobSize
     │
     ▼
[Routing Agent]     → action, crmTarget, SLA, escalation
     │
     ▼
Operator Lead Card
```

---

## Stack

- Vanilla HTML/JS frontend
- Anthropic Claude API (`claude-sonnet-4-20250514`)
- Vercel serverless function proxy (`/api/classify`)
- Deployed on Vercel

---

## Deploy

1. Push repo to GitHub
2. Import to Vercel
3. Add environment variable: `ANTHROPIC_KEY` = your Anthropic API key
4. Deploy — works for any visitor, no key required

---

## Local Setup

Add your key directly to `api/classify.js` for local testing, or use a `.env` file with `ANTHROPIC_KEY=your_key_here`.

---

## Related

- [Operator Revenue Dashboard](link) — lead source conversion and AI agent activity by operator
