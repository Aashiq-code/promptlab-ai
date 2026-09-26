# PromptLab AI

A React, Vite, and Express prompt workspace. Prompts, favorites, settings, and run history persist in browser localStorage. The Express API keeps provider credentials on the server and returns labeled sample responses when credentials are not configured.

## Install

Requires Node.js 20 or newer and npm.

```sh
npm install
```

## Configure AI providers

Copy `.env.example` to `.env` in the project root. Add one or both provider keys; keys are read by Express only and are never included in frontend bundles or API responses.

```env
GEMINI_API_KEY=your_gemini_key
OPENAI_API_KEY=your_openai_key
PORT=5000
```

Gemini: create a key in Google AI Studio and set `GEMINI_API_KEY`.

OpenAI: create an API key in the OpenAI platform and set `OPENAI_API_KEY`.

Restart the API server after changing `.env`. Requests without a configured provider key return a clearly labeled DEMO MODE sample response.

## Run

Start the API and frontend in separate terminals:

```sh
npm run server
npm run dev
```

Or start both using `npm run dev:full`. Open the Vite URL printed in the terminal, usually `http://localhost:5173`.

The frontend proxies `/api` requests to `http://localhost:5000`. The API health check is `GET /api/health`; generation is `POST /api/ai/generate`.

## Notes

- Prompt and history data are per-browser localStorage data; no database or account sync is configured.
- The Express API currently exposes provider health and generation endpoints. Prompt and history CRUD are handled client-side until a database is introduced.
- Tailwind CSS is configured through the Vite plugin; the interface also uses a small authored CSS layer for its design system.