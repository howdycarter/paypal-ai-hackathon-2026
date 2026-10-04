# Plan to Win — PayPal AI Hackathon

## Concept: PayPilot — the AI collections agent

A voice-first AI agent for freelancers and small agencies that turns "get me paid" into a done task. You tell PayPilot who owes you and how much — by voice or chat — and it drafts the invoice, sends it through PayPal, tracks payment status via webhooks, and autonomously follows up with late payers on a schedule you approve. The demo moment: Chris speaks a request, an invoice goes out live in the PayPal sandbox, a simulated client pays, and the agent confirms collection — all inside three minutes.

One paragraph pitch: late invoices are the quiet tax on independent work — not the invoice itself, but the chasing. PayPilot collapses the whole accounts-receivable loop (create → send → track → follow up → confirm) into a single conversation with an agent that acts through PayPal. It's agentic commerce with a real user and a real job to be done.

## Why it wins — mapped to the actual criteria

| Criterion | How PayPilot scores |
|---|---|
| **Technological Implementation** | Deep, non-trivial PayPal surface: Invoicing API (create/send), Orders API, webhooks for payment-status transitions, sandbox buyer/seller accounts. LLM agent with real tool use (not a chatbot skin) — the agent decides which PayPal call to make and when. |
| **Design** | This is the differentiator. Most entries will be dashboards with a chat widget. PayPilot is a complete conversational product: voice-first input, a live payment timeline, approval gates before money moves. Coherent end-to-end experience, not a proof of concept. |
| **Potential Impact** | Specific audience (independent freelancers, small agencies), specific pain (hours lost chasing invoices; cash-flow gaps from late payment), and the demo *shows* the loop closing — invoice sent, payment tracked, follow-up automated. |
| **Innovation/Idea** | Agentic commerce is the frontier PayPal itself is pushing — and it's a named $5,000 award category ("Best Use of Agentic Commerce"). An agent that negotiates the payment lifecycle is novel next to "pay with AI" demos. |
| **Presentation** | Voice-driven demos are made for video: speak → invoice sent → paid → confirmed. Script the 3-minute video around one continuous live run with zero dead air. Also targets the $5,000 Best Demo Delivery award. |

## Tech approach
- **Stack:** Next.js + TypeScript (single language, fast iteration, easy hosted demo on Vercel)
- **PayPal:** REST APIs via sandbox — Invoicing (create/send/remind), Orders, Webhooks (payment capture events); sandbox buyer + seller test accounts
- **AI:** tool-using LLM agent loop (provider TBD — OpenAI or Anthropic); voice input via browser speech APIs with a typed fallback so the demo never depends on mic reliability
- **Data:** lightweight store for invoice state mirrored from PayPal webhook events (the agent's working memory of "who owes what")
- **Guardrails:** human approval gate before any send/remind action — the agent proposes, Chris (or the demo user) approves. This is both good product and good demo theater.

## Differentiation vs typical entries
Most hackathon entries in this space will be: a chatbot that answers questions *about* payments, or a dashboard with an AI summary bolted on. PayPilot inverts it — the agent *acts* through PayPal's API surface. Judges score "genuine effort and working, non-trivial implementation"; an agent executing a multi-step payment workflow is the strongest possible evidence.

## Milestones (working back from Nov 12, 3:00 PM EST)
- **Oct 5–12 — Foundation:** PayPal developer account + sandbox wired; spike Invoicing/Orders/webhooks; repo architecture; agent loop skeleton with one tool call
- **Oct 13–26 — Agent core:** full tool set (create/send/track/remind invoice, check status); webhook-driven state; approval-gate UX; conversational UI working end-to-end in sandbox
- **Oct 27–Nov 5 — Demo hardening:** voice input + typed fallback; hosted demo URL live; follow-up automation; visual polish pass (this is where Design points are won)
- **Nov 6–10 — Submission package:** script, record, and edit the <3 min YouTube video; Devpost writeup (features, tools, how PayPal + AI are used); run instructions finalized
- **Nov 11–12 — Buffer:** Chris reviews demo + video, approves, submits. Nothing goes out without his explicit sign-off.

## Biggest risks
1. **Sandbox webhook reliability** — PayPal sandbox webhooks can lag or drop. Mitigation: poll-based status reconciliation as backup; never let the demo depend on a single webhook firing live.
2. **Voice demo risk** — live speech recognition failing on camera. Mitigation: typed input is a first-class path; the video can show voice, but every flow works typed.
3. **Scope creep** — agentic systems invite "one more capability." Mitigation: lock the loop (create → send → track → follow up → confirm) by Oct 26; everything after is polish.
4. **Field size** — 4,957 participants. Mitigation: most won't finish; a polished, working, well-presented entry is already top-decile. The Design + Presentation criteria are where a design-led builder separates.
