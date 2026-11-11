# Next.js Collaborative Document Editor

A full-stack collaborative document editor built with **Next.js 16**, **Tiptap**, **Liveblocks**, **Better Auth**, **tRPC**, and **PostgreSQL**.

The project explores what a production-minded editor needs beyond a rich-text surface: authentication, document ownership, real-time multiplayer editing, threaded discussions, version history, and a type-safe API.

## Features

- **Authentication** — email/password sign-in with Better Auth and Prisma-backed sessions
- **Document workspace** — create, list, and manage documents
- **Real-time collaboration** — multiplayer editing through the Liveblocks Tiptap extension
- **Presence and cursors** — see collaborators and their current selections
- **Threaded comments** — review and resolve discussions directly in the editor
- **Version history** — inspect and restore previous document states
- **Rich-text editing** — tables, images, highlights, text alignment, mathematics, sub/superscript, and more
- **Type-safe API** — tRPC procedures backed by Zod validation
- **Permission model** — owner, admin, write, and read access levels in the Prisma schema
- **Modern UI** — Next.js App Router, React 19, Tailwind CSS 4, and shadcn/ui

## Tech stack

| Layer | Technology |
| :--- | :--- |
| Framework | Next.js 16 App Router |
| Language | TypeScript |
| Editor | Tiptap 3 |
| Real-time collaboration | Liveblocks |
| Authentication | Better Auth |
| API | tRPC 11 |
| Database | PostgreSQL + Prisma 7 |
| UI | React 19, Tailwind CSS 4, shadcn/ui |
| Validation | Zod |

## Architecture

```text
Next.js App Router
├── Better Auth ──────────────► Prisma ─► PostgreSQL
├── tRPC API ─────────────────► Prisma
├── Document workspace ───────► Liveblocks
└── Tiptap editor ────────────► Liveblocks real-time room
```

Key paths:

```text
app/(auth)/                  Authentication routes
app/documents/               Document list and editor routes
app/api/liveblocks-auth/     Authenticated Liveblocks session endpoint
components/editor/           Tiptap editor, comments, toolbar, and history UI
trpc/                        Type-safe API routers and middleware
prisma/schema.prisma         Document, collaborator, and auth models
```

## Getting started

### Prerequisites

- Node.js 18+ and Bun, or npm/pnpm/yarn
- PostgreSQL 14+
- A Liveblocks project with a secret key

### Environment variables

Create `.env.local` and configure:

```env
DATABASE_URL=postgresql://user:password@localhost:5432/editor
BETTER_AUTH_SECRET=replace-with-a-random-secret
BETTER_AUTH_URL=http://localhost:3000
LIVEBLOCKS_SECRET_KEY=replace-with-your-liveblocks-secret
```

### Install and run

```bash
bun install
bunx prisma generate
bunx prisma migrate dev
bun dev
```

Open `http://localhost:3000/documents` to enter the document workspace.

### Verification

```bash
bun run lint
bunx tsc --noEmit
bun run build
```

There is no automated test suite yet. The current verification path is linting, type checking, production build, and manual testing of authentication and collaboration flows.

## Current limitations

- Automated tests and CI are not configured yet.
- Permission enforcement should be covered by end-to-end tests before production use.
- Deployment and Liveblocks production configuration are not documented yet.
- The root `/` page is still a placeholder; the document workspace lives under `/documents`.

## Roadmap

- Add integration tests for authorization and document lifecycle
- Add a production deployment guide
- Add screenshots and a short collaboration demo
- Tighten permission checks across every document mutation
- Add observability for failed collaboration and API requests

## License

No license has been added yet. Add one before distributing or accepting external contributions.