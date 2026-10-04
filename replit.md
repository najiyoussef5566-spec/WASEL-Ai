# ChatGPT Clone

A browser-based chat demo with a React interface and a Node.js API that streams scripted local replies.

## Run & Operate

- `pnpm --filter @workspace/api-server run dev` — run the API server (port 5000)
- `pnpm --filter @workspace/chatgpt-clone run dev` — run the chat app
- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from the OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- Required env: `DATABASE_URL` — Postgres connection string used by the shared API server

## Stack

- pnpm workspaces, Node.js 24, TypeScript 5.9
- API: Express 5
- DB: PostgreSQL + Drizzle ORM
- Validation: Zod (`zod/v4`), `drizzle-zod`
- API codegen: Orval (from OpenAPI spec)
- Build: esbuild (CJS bundle)

## Where things live

- `artifacts/chatgpt-clone` — React chat interface; conversation history stays in browser localStorage
- `artifacts/api-server` — Express API, including the local mock streaming route
- `lib/api-spec/openapi.yaml` — source of truth for the server API contract

## Architecture decisions

- Conversation history stays in the browser rather than a shared database, so users' chats are not exposed across visitors without authentication.
- Chat replies are deterministic local mock responses; they do not call an external AI provider or require an API key.

## Product

- Start chats, receive streamed demo replies, and revisit or delete browser-local conversations.

## User preferences

- No additional preferences recorded.

## Gotchas

- Chat streaming is consumed with `fetch` and a `ReadableStream`; the generated React Query mutation is not a streaming client.

## Pointers

- See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details
