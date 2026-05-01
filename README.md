<div align="center">

# Rayan Terki

### AI Developer — Building production AI systems where standard models fall short

📍 Gatineau, QC, Canada &nbsp;·&nbsp; [LinkedIn](https://linkedin.com/in/rayan-terki) &nbsp;·&nbsp; [Email](mailto:rayantrk06@gmail.com)

</div>

---

## How I work

I start from a real problem, not from a solution looking for one.

When I hit something I don't know how to solve, I research — papers, methodologies, what others have actually shipped in similar contexts — until I find an approach that fits the constraints of the specific problem. Then I adapt it. I don't apply methods blindly; I keep what works for the case at hand and discard what doesn't.

When I build, I build for the person who'll actually use the system — an annotator who needs to label hundreds of audio files, a marketing team that needs to act on consumer signals, a Béjaïa resident recording emergency scenarios on their phone. Generic features don't ship value. Features designed around the real workflow do.

I use AI coding assistants (Claude Code, Cursor, Antigravity, Codex, Gemini) the way an accountant uses a calculator — as acceleration on operations I understand, not as a substitute for understanding. I review what they produce, recognize when something's off, and know how to fix it. I orchestrate multiple tools in parallel because each is good at different things, and I've spent the last 18 months learning which one for which job.

This is how I've built two real-world AI systems and one open-source project over the past 18 months.

---

## Projects

### 📊 [RamyPulse](https://github.com/rayantr06/ramypulse) — Marketing intelligence for Algerian brands

**The problem.** Algerian consumers leave thousands of comments daily on social media in Darija, Arabizi, and French — often code-switched in the same sentence. No standard NLP tool processes this reliably. Brands operating in this market have no way to know what's working and what's not.

**What I built.** End-to-end SaaS platform: ingestion from 5 social platforms, hybrid NLP pipeline, multi-tenant FastAPI backend with 28-table SQLite schema and in-code migrations, React 18 + Vite 7 frontend with 9 pages designed around marketing workflows (NSS dashboard, campaign impact analysis with pre/active/post windows, RAG-powered conversational explorer, alert engine, AI recommendations, What-If simulator).

**Why it's interesting.** I designed for system uncertainty from day one. The 4-tier inference fallback (DziriBERT → Gemini → Ollama → lexicon with safe neutral logits) exists because LLMs fail in unpredictable ways and the system can't crash. The ABSA adapter distinguishes cross-phrase sarcasm from legitimate mixed opinions through inter-aspect scanning, with `reason` fields on every annotation for traceability. The 20 hand-crafted adversarial test cases target exactly the failure modes the base model has — sarcasm, ironic emojis, dense code-switching, French litotes. 890+ tests across the platform because behavior in production matters more than a benchmark number.

Presented at AI Expo 2026 — Industry Track, attracting direct partnership interest from a major Algerian FMCG company. Built in collaboration with Leticia Bouchenna (M2 Data Science, Université de Béjaïa) who led data collection, partnerships, and academic presentation.

`Python` `FastAPI` `React 18` `TypeScript` `Vite 7` `SQLite` `FAISS` `BM25` `DziriBERT` `Gemini` `Ollama` `PyTorch` `HuggingFace` `Docker`

---

### 🎙️ DGPC — Emergency-call AI pipeline for low-resource Kabyle

**The problem.** The Direction Générale de la Protection Civile of Béjaïa receives emergency calls in Kabyle EOR — a Berber dialect with virtually zero NLP resources. No ASR model handles it well. No annotation methodology applies directly. The downstream stakes are high: a misclassified emergency call has real consequences.

**How the project unfolded — each component answers a problem I hit in the previous one.**

I started by designing the annotation schema with 15 DGPC-specific fields including the operator's rationale (`notes_cot`), then annotated 506 real calls. *Leticia couldn't annotate everything manually* → I built a Streamlit annotation app with Gemini 3 Flash assistance: Gemini does the heavy lift, the human corrects. *Data still insufficient* → I researched, found Pleias SYNTH methodology, read their publication, adapted it to Kabyle EOR: Memory Core with 47K verified entries from academic sources (FarZ1, Belkacem, KabyleNLP), 2-layer hybrid RAG with adaptive fusion based on scenario complexity, Kabyle Guard quality filter (7 blocking rules + 11 calibrated quality penalties), 384 validated synthetic scenarios produced. *We also need audio, not just text* → tried TTS, quality wasn't good enough for low-resource Kabyle, pivoted to participatory voice collection: I built a deployed web app where Béjaïa residents record scenarios on their phone, designed for non-technical users — 958 recordings collected. *Long calls need chunking for ASR training* → tried pyannote diarization, results weren't usable, switched to MMS forced alignment with a reframed approach: "the data is verified, there's nothing to throw away — I just need to find the chunk boundaries." *Some participants gamed the recording* → designed an empirical calibration: selected 15 trusted speakers, computed thresholds on their data (ROC AUC 0.9572), used those thresholds to validate everyone else's recordings.

Then I reframed evaluation itself. WER on Whisper-small came out at 0.88 — basically useless by classic ASR metrics. Instead of pivoting to a different model, I redefined the metric: `LocationScore`, `VictimCountScore`, `SeverityScore`, `IncidentTypeScore`, `CriticalCueF1`. What matters in production isn't transcription beauty — it's whether the downstream extractor can recover the intervention information.

**Why it's interesting.** Every component exists because a specific real-world problem made it necessary. The project is an end-to-end data engine: real annotations → synthetic generation grounded in verified linguistic resources → human voice collection → forced alignment with empirical calibration → ASR fine-tuning experiments (Whisper, Qwen3-ASR, NeMo) → task-oriented evaluation framework.

Built in collaboration with Leticia Bouchenna (M2 Data Science, Université de Béjaïa) who led the partnership with Direction Générale de la Protection Civile de Béjaïa.

`Python` `FastAPI` `Flask` `Streamlit` `Gemini` `PyTorch` `torchaudio` `MMS` `Whisper` `Qwen3-ASR` `NeMo` `QLoRA` `Google Apps Script`

---

### 🚨 [Emergency Lang Kit (ELK)](https://github.com/rayantr06/emergency-lang-kit) — Personal open-source

Modular AI architecture (Kernel + Plugins pattern), hybrid RAG (ChromaDB dense + FAISS sparse), Whisper fine-tuning via QLoRA for low-resource languages, FastAPI services with strict Pydantic validation, HITL review mechanisms, pytest functional tests, full Docker stack with documented HLD + LLD architecture.

`Python` `FastAPI` `OpenAI` `LLaMA 3` `ChromaDB` `FAISS` `Whisper` `QLoRA` `pytest` `Docker`

---

## Tech I work with

**Backend** &nbsp; Python · FastAPI · Flask · Pydantic · SQLite · multi-tenant architecture · in-code schema migrations

**Frontend** &nbsp; React 18 · TypeScript · Vite 7 · Playwright E2E · type-safe API contracts

**LLM integration** &nbsp; OpenAI · Gemini (Flash & Pro) · LLaMA 3 / Ollama · structured JSON output · graceful degradation · multi-tier fallback patterns

**ML & fine-tuning** &nbsp; PyTorch · HuggingFace Transformers · DziriBERT · Whisper · Qwen3-ASR · NeMo · QLoRA · knowledge distillation · Focal Loss

**RAG & retrieval** &nbsp; FAISS · BM25 · ChromaDB · Reciprocal Rank Fusion · adaptive retrieval budgets

**Data engineering** &nbsp; synthetic data generation · MMS forced alignment · audio preprocessing · empirical threshold calibration · adversarial test design

**AI-accelerated development** &nbsp; Claude Code · Cursor · Antigravity / Codex · GitHub Copilot · multi-agent orchestration with frozen interface contracts and TDD-first discipline

**Infrastructure** &nbsp; Docker · GitHub Actions · Streamlit · Google Apps Script

---

## Background

- **DEC in Computer Programming** — Collège La Cité, Ottawa (2023–2026)
- **Preparatory Classes in CS & Mathematics** — ESTIN, Béjaïa, Algeria (2021–2023)
- 18 months of independent AI engineering on real-world projects
- Languages: French (native) · English (professional) · Arabic (native) · Kabyle (native)

---

## Currently

Looking for an AI / ML developer role in Canada — Gatineau, Ottawa, Montreal, or remote. I'm looking for a team where I can keep doing what I've been doing: starting from real problems, building maintainable systems, and using AI as an engineering tool rather than a magic wand.

📧 **rayantrk06@gmail.com** &nbsp;·&nbsp; 💼 [LinkedIn](https://linkedin.com/in/rayan-terki) &nbsp;·&nbsp; 📍 Gatineau, QC, Canada 🇨🇦
