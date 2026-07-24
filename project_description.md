# VoyageAI — Intelligent Travel Itinerary Generator

> **Live Web Application**: [https://voyageai-f4pd.onrender.com](https://voyageai-f4pd.onrender.com)  
> **GitHub Repository**: [https://github.com/SanjeetMurmu126/VoyageAI](https://github.com/SanjeetMurmu126/VoyageAI)

---

## 1. Executive Summary

**VoyageAI** is a full-stack, AI-powered travel planner built with **Node.js, Express, and Google Gemini 2.5 Flash**. It allows users to input any destination, trip duration, budget preference, and personal interests to generate comprehensive, day-by-day travel itineraries delivered via **Server-Sent Events (SSE)** real-time streaming.

---

## 2. Key Highlights & Features

* **⚡ Real-Time Streaming Output**: Streams AI-generated itineraries chunk-by-chunk using Server-Sent Events (SSE), eliminating long loading delays.
* **🎯 Precision Personalization**: Tailors daily itineraries based on budget tier (*Budget-friendly*, *Moderate*, *Luxury*) and custom interest preferences (e.g. food tours, museums, outdoor activities).
* **📅 Interactive Timeline & Checklist**: Renders structured day blocks with morning/afternoon/evening schedules, interactive packing checkboxes, and local travel tips.
* **📄 One-Click Export & Printing**: Integrated print/PDF engine formats custom itineraries into clean, styled documents.
* **🎨 Modern Dashboard Design**: Engineered with a Scandinavian Slate & Emerald minimalist aesthetic—strictly NO gradients and NO glassmorphism for maximum legibility and contrast.

---

## 3. Technical Stack & Deployment

| Layer | Technology | Details |
|---|---|---|
| **Live Hosting** | Render Cloud Platform | Deployed live at `https://voyageai-f4pd.onrender.com` |
| **Backend Engine** | Node.js (v18+) / Express.js | Manages REST endpoints, static file serving, and SSE streaming pipeline |
| **Generative AI** | Google Gemini 2.5 Flash (`@google/generative-ai`) | High-speed LLM configured with structured system prompts and streaming API |
| **Frontend Architecture** | HTML5, Vanilla CSS, Vanilla JavaScript (ES6+) | Modern dashboard UI built with Space Grotesk & IBM Plex fonts, and Lucide Icons |
| **Streaming Protocol** | Server-Sent Events (SSE) | HTTP streaming for progressive chunk rendering in client UI |

---

## 4. System Architecture

```
┌─────────────────────────┐
│   User Browser (UI)     │
└────────────┬────────────┘
             │ 1. POST /api/generate-itinerary (JSON Payload)
             ▼
┌─────────────────────────┐
│ Express Server (Render) │
└────────────┬────────────┘
             │ 2. generateContentStream(prompt)
             ▼
┌─────────────────────────┐
│  Google Gemini API      │ (gemini-2.5-flash)
└────────────┬────────────┘
             │ 3. Chunked SSE Stream Data
             ▼
┌─────────────────────────┐
│   User Browser (UI)     │ ──► Progressive Markdown Rendering & Timeline Node View
└─────────────────────────┘
```

---

## 5. API Endpoint Reference

### `POST /api/generate-itinerary`

#### Request Payload (`application/json`)
```json
{
  "destination": "Kyoto, Japan",
  "days": 3,
  "budget": "Moderate",
  "interests": "historic temples, traditional tea houses, local ramen spots"
}
```

#### Response Stream (`text/event-stream`)
```http
HTTP/1.1 200 OK
Content-Type: text/event-stream
Cache-Control: no-cache
Connection: keep-alive

data: {"text":"### Day 01: Historic Higashiyama\n* 09:00 - Fushimi Inari Taisha: Morning walk through torii gates.\n"}

data: [DONE]
```

---

## 6. Local Development & Deployment

### Environment Setup
Create a `.env` file in the project root:
```env
PORT=3000
GEMINI_API_KEY=YOUR_GEMINI_API_KEY_HERE
```

### Installation Commands
```bash
# 1. Clone repository
git clone https://github.com/SanjeetMurmu126/VoyageAI.git

# 2. Install dependencies
cd VoyageAI
npm install

# 3. Start application
npm start
```
Access the application at `http://localhost:3000` or visit the live cloud deployment at `https://voyageai-f4pd.onrender.com`.

---

## 7. Metadata & Credits

* **Project Name**: VoyageAI
* **Author / Owner**: Sanjeet Murmu (`SanjeetMurmu126`)
* **Live Application**: [https://voyageai-f4pd.onrender.com](https://voyageai-f4pd.onrender.com)
* **Source Repository**: [https://github.com/SanjeetMurmu126/VoyageAI](https://github.com/SanjeetMurmu126/VoyageAI)
* **License**: MIT
