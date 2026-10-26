# mediscanx
# MediScanX

An AI-assisted pharmacy management Android app that helps small pharmacies manage stock, sales and orders, find medicines quickly, and ask an AI assistant questions about their inventory.

## Demo

A demo video of MediScanX is posted on my LinkedIn profile: [Bhoomi Pal on LinkedIn](https://www.linkedin.com/in/bhoomi-pal-90ab282a2/)

## The problem

Many small pharmacies still track stock by hand, copy details from supplier invoices manually, and search for medicines by exact name. This costs time and causes mistakes. MediScanX puts these tasks in one mobile app.

## Features

- **Inventory, sales and orders:** track medicines in stock, record sales and manage orders
- **Fuzzy medicine search:** finds medicines even when the name is misspelled or partly typed (Fuse.js)
- **OCR invoice parsing:** reads supplier invoices to reduce manual data entry
- **AI assistant:** a chat assistant that answers questions about the pharmacy's inventory

## Tech stack

| Layer | Technology |
|---|---|
| Frontend | Vite, JavaScript |
| Android app | Capacitor (web app wrapped as an Android app) |
| Search | Fuse.js |
| AI backend | n8n cloud workflow, LangChain AI Agent, Google Gemini Flash |
| Chat memory | n8n Buffer Window Memory |
| Data store (MVP) | Excel workbook with Inventory, Sales and Orders sheets |

## How the AI assistant works

```
Android app -> n8n webhook -> IF node -> AI Agent (Gemini Flash + memory) -> formatted reply -> app
```

The assistant uses **in-context grounding**: current inventory data is added to the prompt so the model answers from the pharmacy's own stock. This is not full RAG with a vector database.

## Getting started

Prerequisites: Node.js, Android Studio, an n8n cloud workflow and a Google Gemini API key.

1. Download or clone this repository and open the project folder in a terminal.
2. Install dependencies:

```bash
npm install
```

3. Create a `.env` file in the project folder and add your own API keys. Never upload your `.env` file to GitHub.

4. Run in the browser:

```bash
npm run dev
```

5. Build for Android:

```bash
npm run build
npx cap sync android
npx cap open android
```

## Project status

MediScanX is a work in progress.

- [x] Inventory, sales and orders
- [x] Fuzzy medicine search
- [x] OCR invoice parsing
- [x] n8n AI assistant workflow
- [ ] AI chat connection from the Android app (fixing API key and endpoint access in the APK build)
- [ ] Replace the Excel data store with a real database
- [ ] Move API keys to a secure backend

## Known limitations

- Excel is used as the database to keep the first version simple. It does not scale to many users.
- The development proxy used by Vite does not work inside the Android build, so the app needs a deployed backend endpoint.
- API keys must not be stored in the app. They should live on a server.

## Author

**Bhoomi Pal**
B.Tech Computer Science Engineering, UPES Dehradun
[LinkedIn](https://www.linkedin.com/in/bhoomi-pal-90ab282a2/) | [GitHub](https://github.com/Shubhi-gif-7565)
