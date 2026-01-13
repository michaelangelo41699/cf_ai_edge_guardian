# Edge Guardian (cf_ai_edge_guardian)

**A Real-Time AI Computer Vision System for Digital Safety.**

Edge Guardian is a full-stack mobile application that utilizes Cloudflare's Edge network to analyze images for psychological manipulation, dark patterns, and fear-mongering tactics. It demonstrates a complete "Region: Earth" architecture, handling multimodal AI inference, stateful memory, and mobile user input without a single centralized server.

##  Live Demo & Architecture

* **Backend:** Deployed on Cloudflare Workers (Global).
* **Frontend:** React Native (Expo) Mobile App.
* **AI Model:** Llama 3.2 11B Vision Instruct (running on Workers AI).

### System Architecture
1.  **User Input:** User captures/selects an image via the React Native mobile app.
2.  **Edge Optimization:** Image is resized and compressed on-device to <50KB to minimize latency and token usage.
3.  **Gateway:** Cloudflare Worker receives the request and sanitizes the Base64 payload.
4.  **Coordination:** The Worker routes the request to a **Durable Object** (acting as a per-user session).
5.  **Inference:** The Durable Object invokes **Workers AI (Llama 3.2 Vision)** with a "One-Shot" JSON prompt.
6.  **State & Memory:** The analysis result is stored persistently inside the Durable Object (SQLite) to provide a history of past scans.

## Assignment Components Checklist

This project satisfies all requirements for the Cloudflare AI Assignment:

* **LLM:** Uses `@cf/meta/llama-3.2-11b-vision-instruct` for multimodal analysis.
* **Workflow / Coordination:** Orchestrated via **Cloudflare Workers** binding to **Durable Objects**.
* **User Input:** Native Mobile Interface (React Native) supporting camera and gallery uploads.
* **Memory / State:** **Durable Objects** provide persistent storage for user scan history and "Traffic Light" logic.

##  Tech Stack

* **Backend:** TypeScript, Cloudflare Workers, Durable Objects, Workers AI.
* **Frontend:** React Native, Expo, TypeScript.
* **Tools:** Wrangler, npm, VS Code.

##  How to Run Locally

### Prerequisites
* Node.js (v18+)
* Cloudflare Account (for Wrangler)
* Expo Go app on your phone (for testing frontend)

### 1. Backend Setup
The backend runs on Cloudflare Workers.

```bash
cd backend
npm install

# Deploy to your Cloudflare account
npx wrangler deploy
