# AnyWebSupport AI

AnyWebSupport AI is an AI-powered customer support chatbot that can answer questions about any webpage. You give it a URL, it scrapes the page content, and then uses OpenAI to respond to user questions based on what it finds. No manual knowledge base setup required.

Built with Next.js, React, and OpenAI's GPT-4o-mini model.

---

## What it does

1. The user pastes a URL into the chat interface.
2. The backend scrapes the page content using Cheerio.
3. That content is passed to GPT-4o-mini as context.
4. The AI answers user questions based only on what's on that page, streamed back in real time.
5. Users can switch languages and submit feedback, which gets saved to Firebase Firestore.

---

## Features

- Works with any public webpage, no configuration needed per site
- Real-time streaming responses from OpenAI
- Multi-language support: English, Spanish, French, Chinese (Simplified), and Hindi
- Feedback form with star ratings, stored in Firebase Firestore
- Clean dark-themed UI built with Material UI
- Serverless-friendly web scraping using Cheerio (no headless browser required)

---

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | Next.js 14 (App Router) |
| UI | React 18, Material UI v5 |
| AI | OpenAI API (GPT-4o-mini) |
| Web Scraping | Cheerio |
| Database | Firebase Firestore |
| Internationalization | i18next, react-i18next |
| Styling | Tailwind CSS, Emotion |

---

## Getting Started

### Prerequisites

- Node.js 18 or later
- An OpenAI API key
- A Firebase project with Firestore enabled

### Installation

```bash
git clone https://github.com/your-username/AnyWebSupport-AI-Site-Support-Bot.git
cd AnyWebSupport-AI-Site-Support-Bot
npm install
```

### Environment Variables

Create a `.env.local` file in the root of the project and add your OpenAI API key:

```
OPENAI_API_KEY=your_openai_api_key_here
```

The Firebase config is currently stored in `firebase.js`. For production use, move those values into environment variables as well.

### Running Locally

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

---

## Project Structure

```
app/
  page.js              # Landing page
  layout.js            # Root layout
  globals.css          # Global styles
  i18n.js              # i18next configuration
  dashboard/
    page.js            # Chat interface
  api/
    chat/
      route.js         # API route: scrapes URL + calls OpenAI
  en/ es/ fr/ ch/ hi/  # Translation files for each language
firebase.js            # Firebase initialization
```

---

## How the API Works

The `/api/chat` route receives the chat history plus the URL (sent as a system message). It:

1. Fetches the raw HTML of the URL using `fetch`
2. Parses it with Cheerio and extracts the body text
3. Passes that text as context to GPT-4o-mini
4. Streams the response back to the client

The AI is instructed to only answer based on the scraped content, and to politely decline questions about anything not covered on the page.

---

## Supported Languages

The chat interface can be switched between:

- English
- Spanish (Español)
- French (Français)
- Chinese Simplified (中文)
- Hindi (हिन्दी)

---

## Feedback

After a chat session, users can click "Give Feedback" to submit a star rating and comment. Feedback is stored in the `feedback` collection in Firebase Firestore.
