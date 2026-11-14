# kalaasetu-ai
Vernacular Agentic AI &amp; ONDC bridge on WhatsApp empowering rural artisans to discover true urban prices (₹50 vs ₹500), generate studio catalogs with QR Digital Craft Passports, and sell directly to city buyers without middlemen. Built by Team Bharat Builders.

# KalaSetu AI: Vernacular Artisan Commerce Agents

> **Turning ₹50 Village Crafts into ₹500 Urban Brands on ONDC via Voice AI & QR Craft Passports.**  
> Built by **Team Bharat Builders** for the **GAVS Tech4Bharat Hackathon** (Theme 7 — Problem 7.1: *Artisans and weavers depend on middlemen and rarely reach buyers who value their craft*).

---

## 📖 Overview

Rural artisans and weavers in India face severe **information asymmetry** and **digital barriers**. Unaware that a handmade item sold for **₹50** in their village retails for **₹500** in metro cities, makers depend on middlemen who capture up to **90%** of the retail value and strip away the craft's cultural identity.

**KalaSetu AI** solves this by pairing a zero-literacy, voice-first **Multi-Agent AI system on WhatsApp** with **ONDC (Open Network for Digital Commerce)** and **Bhashini APIs**. Instead of learning complex e-commerce dashboards, an artisan simply sends a smartphone photo and a voice note in their native dialect—autonomous agents handle pricing intelligence, catalog generation, logistics estimation, and B2B negotiations while keeping the artisan in control.

---

## ✨ Key Features

- **🎙️ Vernacular Voice-First Onboarding:** Powered by **Bhashini ASR/NMT/TTS** over WhatsApp, enabling artisans to interact in Kannada, Hindi, Tamil, and other regional languages with zero typing or app training.
- **📊 Real-Time Urban Price Discovery:** Queries live **ONDC Beckn `/search` APIs** across Tier-1 cities (Bengaluru, Mumbai, Delhi) to benchmark true urban retail prices and alert artisans against underpriced local offers.
- **📦 SHG Cluster Logistics & Net-Payout Calculator:** Coordinates consolidated pickups through local Self-Help Group (SHG) hubs and Common Service Centres (CSCs), calculating exact net profit (`₹425` payout on a `₹500` sale after `₹58` shipping, `₹15.50` app fees, and ONDC's flat `₹1.50` network fee).
- **🏷️ QR Digital Craft Passport:** Enhances raw phone photos into studio-grade listings and generates a tamper-proof QR tag for every product—allowing urban buyers to scan and hear the artisan's translated voice story.
- **🤝 Human-in-the-Loop (HITL) B2B RFQ Agent:** Autonomously handles bulk Request-for-Quote (RFQ) inquiries from boutiques and corporate buyers, pausing to ask the artisan for voice/button approval before committing to any price or bulk order.

---

## 🏗️ Multi-Agent Architecture & Execution Flow

KalaSetu AI uses an event-driven multi-agent state machine (**LangGraph / CrewAI**) orchestrated by a central **Supervisor Agent**:

```text
[Artisan: Voice Note + Photo via WhatsApp]
                     │
                     ▼
        ┌─────────────────────────┐
        │ 1. Vernacular Gateway   │ ──► Bhashini API (Speech-to-Text + Translation)
        └────────────┬────────────┘
                     │
                     ▼
        ┌─────────────────────────┐
        │ 2. Supervisor Agent     │ ──► Plans tasks & updates Shared State
        └───────┬─────────┬───────┘
                │         │
       ┌────────┘         └────────┐
       ▼                           ▼
┌──────────────┐          ┌────────────────┐
│ 3. Vision &  │          │ 4. Price Intel │
│ Catalog Agent│          │     Agent      │
└──────┬───────┘          └────────┬───────┘
       │ (Craft specs)             │ (Urban price: ₹500)
       └────────────┬──────────────┘
                    ▼
        ┌─────────────────────────┐
        │ 5. Logistics & Margin   │ ──► ONDC Logistics API (Net payout: ₹425)
        └────────────┬────────────┘
                     │
                     ▼
        ┌─────────────────────────┐
        │ 6. HITL Approval Gate   │ ──► WhatsApp Voice Prompt ("Approve ₹500?")
        └────────────┬────────────┘
                     │ (Artisan clicks "Yes")
                     ▼
        ┌─────────────────────────┐
        │ 7. Publishing & B2B     │ ──► ONDC Seller Node + QR Craft Passport
        └─────────────────────────┘
```

### Step-by-Step Execution
1. **Vernacular Ingestion:** WhatsApp webhook receives audio + image; Bhashini transcribes and translates the dialect while preserving the original voice recording.
2. **Supervisor Planning:** Inspects shared state memory and dispatches parallel tasks to the Vision and Price Discovery agents.
3. **Vision & Storytelling Agent:** Classifies the craft, estimates dimensions/weight, generates a clean studio background, and mints a **QR Digital Craft Passport**.
4. **ONDC Price-Benchmarking Agent:** Queries live ONDC retail catalogs in metro pin codes to establish the `₹450–₹550` urban market band and flags the `₹50` local offer as underpriced.
5. **SHG Logistics & Margin Agent:** Fetches consolidated cluster shipping rates via ONDC Logistics Partners and verifies the `₹425` net bank payout.
6. **HITL Approval Gate:** Sends a translated voice summary back to the artisan on WhatsApp for single-tap approval before publishing.
7. **Live ONDC Publishing & B2B Loop:** Publishes the SKU across ONDC buyer apps (Paytm, Mystore, Snapdeal, DigiHaat) and manages ongoing bulk B2B RFQs.

---

## 💰 Unit Economics (8.5x Artisan Income Jump)

| Metric | Traditional Middleman | Closed Marketplaces | KalaSetu AI + ONDC |
| :--- | :--- | :--- | :--- |
| **Urban Selling Price** | ₹500 | ₹500 | **₹500** |
| **Fees & Logistics** | ₹450 (Trader cut) | ~₹180 (25–30% fee + ads) | **₹75 Total** (₹58 shipping + ₹15.50 app + ₹1.50 ONDC) |
| **Artisan Net Payout** | ₹50 (10%) | ~₹320 (64%) | **₹425 (85% — 8.5x local rate)** |

---

## 🛠️ Tech Stack

- **Conversational & Voice Layer:** WhatsApp Business Cloud API, **Bhashini API** (ASR, NMT, TTS)
- **Agentic Orchestration:** Python, FastAPI, **LangGraph / CrewAI**
- **Multimodal Vision & Provenance:** Multimodal Vision LLM (background cleanup & attribute extraction), Cryptographic QR Craft Passport Generator
- **Commerce & Fulfillment Rails:** **ONDC (Beckn Protocol)** Seller Node, ONDC Logistics APIs (India Post / Shiprocket), UPI Direct Settlement

---

## 🚀 Quickstart (Prototype Setup)

```bash
# 1. Clone the repository
git clone https://github.com<your-username>/kalasetu-ai.git
cd kalasetu-ai

# 2. Create and activate virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Configure environment variables
cp .env.example .env
# Add your BHASHINI_API_KEY, WHATSAPP_TOKEN, LLM_API_KEY, and ONDC_SANDBOX_URI

# 5. Run the FastAPI Agent Webhook Server
uvicorn app.main:app --reload --port 8000
```

---

## 🗺️ Roadmap

- **Phase 1 (Prototype & Sandbox):** End-to-end WhatsApp voice-to-ONDC sandbox workflow with Channapatna lacquerware sample catalogs.
- **Phase 2 (Cluster Pilot):** Onboard 50 artisans via local Self-Help Groups (SHGs) in Karnataka using India Post on ONDC for aggregated village pickups.
- **Phase 3 (B2B Scale):** Activate automated bulk RFQ matchmaking for urban interior boutiques and corporate gifting buyers.

---

## 👥 Team Bharat Builders

- **Project:** KalaSetu AI — Vernacular Artisan Commerce Agents
- **Event:** GAVS Tech4Bharat Hackathon (Bengaluru)
- **License:** MIT License
