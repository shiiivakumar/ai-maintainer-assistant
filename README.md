# AI Maintainer Assistant

AI Maintainer Assistant is a small full-stack TypeScript prototype for maintainers who want quick code review help. Paste a code snippet into the UI, send it to the backend, and receive a structured review with a summary, likely bugs, and practical improvement suggestions.

## Tech stack

- React + Vite + Tailwind CSS
- Node.js + Express
- Vercel serverless API route for deployment
- OpenAI API
- Shared TypeScript package for API contracts

## Project structure

- `client/` React frontend
- `server/` Express API
- `shared/` Shared request and response types

## Getting started

1. Install Node.js 20+ and npm.
2. From the project root, install dependencies:

```bash
npm install
```

3. Copy the example environment file and add your API key:

```bash
Copy-Item server\\.env.example server\\.env
```

4. Start the development servers:

```bash
npm run dev
```

5. Open the frontend URL shown by Vite. The app expects the Express API to run on `http://localhost:3001`.

## Environment

`server/.env`

```env
OPENAI_API_KEY=your_api_key_here
PORT=3001
OPENAI_MODEL=gpt-4.1-mini
MAX_CODE_LENGTH=12000
```

## API

`POST /api/analyze`

Request:

```json
{
  "code": "function hello() { return 'world'; }"
}
```

Response:

```json
{
  "summary": "Simple function that returns a string literal.",
  "bugs": [],
  "suggestions": ["Add a test if this behavior is part of a public module."]
}
```

## Notes

- The backend validates input before calling OpenAI.
- The UI gracefully handles empty states, loading, and API failures.
- The model is asked for strict JSON to keep rendering stable.

## Vercel deployment

This project includes a Vercel-ready setup:

- Static frontend built from `client/`
- Serverless API at `api/analyze.ts`
- Vercel config in `vercel.json`

### Deploy steps

1. Import the repo into Vercel.
2. Set the project root to `ai-maintainer-assistant` if needed.
3. Add these environment variables in Vercel:

```env
OPENAI_API_KEY=your_api_key_here
OPENAI_MODEL=gpt-4.1-mini
MAX_CODE_LENGTH=12000
```

4. Use the default settings from `vercel.json`, or run:

```bash
vercel
```

The frontend will call `/api/analyze` in both local and deployed environments.
