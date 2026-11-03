# Paytm Saathi 🤝

**Your Kirana AI Teammate** — An autonomous multi-agent AI system that doesn't just answer merchant questions, it finishes the job.

Built for the **Paytm Build for India AI Hackathon** — Track 3: Autonomous AI Teammates.

---

## 🧩 The Problem

Lakhs of small merchants on Paytm — kirana stores, auto parts shops, grocery sellers — face the same repeat issues every day:

- Payments that look stuck or confusing
- Soundbox devices going offline
- Settlement amounts that don't match expectations
- Merchants quietly going dormant, unnoticed
- Incomplete KYC blocking onboarding
- Field sales reps visiting the wrong merchants
- Pending customer udhaar with no easy way to follow up

Every one of these currently requires a human support agent — and at this scale, support teams simply can't keep up.

## 💡 The Solution

**Paytm Saathi** is one AI teammate made up of **seven specialist agents**, coordinated by a central orchestrator called **Saathi Brain**. Instead of a single generic chatbot, each agent is an expert in one problem domain — and agents can automatically hand off work to each other, just like a real support team.

Every action an agent takes passes through a **Policy Engine** that checks its risk level — low-risk actions run automatically, high-risk actions always wait for human approval — with a full audit trail for every decision.

---

## 🧠 How It Works

```
Merchant/Event Signal → Saathi Brain (Orchestrator)
                              │
                 ┌────────────┼────────────┐
                 ▼            ▼            ▼
            Resolve   Fix   Reconcile   Revive   Onboard   FieldMate   Vasooli
                              │
                   Policy Engine (risk check)
                              │
                 Allowed? ──No──▶ Human Approval Queue
                      │Yes
                      ▼
                 Action Executed
                      │
                 Verification Step
                      │
                 Audit Log (immutable)
```

### The Seven Agents

| Agent | Handles | Example |
|---|---|---|
| **Resolve** | Failed / confusing payments | Confirms an auto-reversed payment instead of raising a ticket |
| **Fix** | Soundbox / device issues | Voice-guided troubleshooting; auto-books a technician if remote fix fails |
| **Reconcile** | Settlement mismatches | Explains the exact fee breakdown behind a settlement gap |
| **Revive** | Dormant merchant recovery | Proactively detects a sales drop and investigates the cause |
| **Onboard** | KYC completion | Flags a blurry PAN photo or missing document and guides the merchant |
| **FieldMate** | Field sales support | Prioritized visit routes; converts voice notes into CRM entries |
| **Vasooli** | Udhaar (credit) recovery | Sends consent-based reminders to customers on the merchant's behalf |

### Multi-Agent Handoff (live demo)

Our strongest proof point: a single merchant case (**Singh Automobiles**) flows through **4 agents across 6 steps** with zero human intervention —
`Revive` detects an 86% sales drop → investigates and hands off to `Fix` → `Fix` attempts a remote reboot, verifies it failed, books a technician → `FieldMate` prioritizes the visit and bundles a loan offer → `Revive` re-checks and confirms recovery to ₹17,500/day.

---

## 🏗️ Tech Stack

**Backend**
- Python, FastAPI, Pydantic v2
- LangGraph + LangChain — multi-agent orchestration
- SQLAlchemy + Alembic, PostgreSQL
- APScheduler — background scans (dormancy detection, device health checks)

**Frontend**
- Merchant App: React Native (Expo) + TypeScript
- Employee Control Tower: React (Vite) + TypeScript + Tailwind CSS

**AI/ML**
- LLM-based reasoning for intent classification and orchestration
- OCR for KYC document validation
- Speech-to-Text / Text-to-Speech for multilingual voice support

**Safety & Governance**
- Policy Engine with risk-tiered action control (R0–R4)
- Verification-separate-from-execution for every agent action
- Idempotency keys, bounded agent loops, full audit logging

---

## 📱 Applications

| App | Description | Live Link | 
|---|---|---|
| **Merchant App** | Mobile-first app for merchants — OTP login, Soundbox status, Saathi Chat, udhaar tracker | [paytm-saathi-merchant-mobile-xbtm.vercel.app](https://paytm-saathi-merchant-mobile-xbtm.vercel.app/) |
| **Employee Control Tower** | Dashboard for Paytm staff — live KPIs, case management, agent activity log, handoff demo | [Paytm-saathi-employee dashboard](https://paytm-saathi-employee-web.vercel.app/) | 

---

## 🚀 Getting Started

```bash
# Clone the repository
git clone <repo-url>
cd paytm-saathi

# Backend setup
cd backend
pip install -r requirements.txt
alembic upgrade head
uvicorn app.main:app --reload --port 8000

# Merchant app
cd merchant-app
npm install
npm run start   # Expo dev server, localhost:8081

# Employee Control Tower
cd employee-dashboard
npm install
npm run dev      # Vite dev server, localhost:5173
```

> Demo accounts and seeded data are available on first run — see `backend/seed/demo_data.py`.

---

## ✨ What Makes This Different

- **One teammate, not seven bots** — shared context, real agent-to-agent handoff
- **Real actions, not just conversation** — books technicians, reverses confusion, recovers money
- **Safety by design** — every action risk-checked before execution, human approval on sensitive actions
- **Self-verifying** — agents confirm real outcomes before marking a case resolved
- **Built for Bharat** — voice-first, multilingual, no learning curve for merchants

---

## 📈 Impact & Business Case

- Lower support cost — fewer tickets need a human
- Recovered GMV — dormant merchants proactively won back
- Faster onboarding-to-active conversion
- Higher field-sales conversions via targeted visits
- Higher merchant retention through recovered udhaar

---

## 🗺️ Roadmap

- Transparent AI confidence scores on every decision
- Gradually increasing agent autonomy per merchant ("trust ladder")
- Area-level pattern detection across merchants
- Festival-calendar-aware proactive support

---

## 👥 Team

Built for the Paytm Build for India AI Hackathon — Track 3: Autonomous AI Teammates.

## 📄 License

This project was built for hackathon demonstration purposes.
