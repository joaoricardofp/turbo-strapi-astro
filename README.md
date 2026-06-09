# Turborepo starter

This Turborepo starter is maintained by the Turborepo core team.

## Using this example

Run the following command:

```sh
pnpx create-turbo@latest
```

## What's inside?# astro-strapi-starter

A monorepo starter for building static websites with a headless CMS. Uses Astro for the frontend and Strapi as the content management system, orchestrated with Turborepo.

---

## Stack

| Layer | Technology |
|---|---|
| Frontend | Astro 6 + React 19 |
| CMS | Strapi 5 |
| Monorepo | Turborepo + pnpm workspaces |
| Styling | Tailwind CSS v4 |
| Components | shadcn/ui |
| Database | PostgreSQL |

---

## Project structure

```
.
├── apps/
│   ├── web/          # Astro frontend
│   └── cms/          # Strapi CMS
├── packages/
│   ├── biome-config/
├── turbo.json
├── pnpm-workspace.yaml
└── package.json
```

---

## Requirements

- Node.js >= 18
- pnpm >= 9
- PostgreSQL instance (local or remote)

---

## Getting started

**1. Clone the repository**

```bash
git clone https://github.com/joaoricardofp/turbo-strapi-astro.git
cd turbo-strapi-astro
```

**2. Install dependencies**

```bash
pnpm install
```

**3. Set up environment variables**

```bash
cp apps/cms/.env.example apps/cms/.env
```

Fill in the values in `apps/cms/.env`. See the environment variables section below.

**4. Start the development environment**

```bash
pnpm dev
```

This starts both apps in parallel via Turborepo:

- Astro at `http://localhost:4321`
- Strapi at `http://localhost:1337`

---

## Environment variables

All required variables are documented in `apps/cms/.env.example`.

```env
# Server
HOST=0.0.0.0
PORT=1337

# Security (generate random values for production)
APP_KEYS=
API_TOKEN_SALT=
ADMIN_JWT_SECRET=
TRANSFER_TOKEN_SALT=
JWT_SECRET=

# Database
DATABASE_CLIENT=postgres
DATABASE_HOST=
DATABASE_PORT=5432
DATABASE_NAME=
DATABASE_USERNAME=
DATABASE_PASSWORD=
DATABASE_SSL=false
```

The Astro app requires a `.env` file at `apps/web/.env`:

```env
STRAPI_URL=http://localhost:1337
```

> Never commit real `.env` files. They are already listed in `.gitignore`.

---

## Strapi setup

After starting the CMS for the first time:

1. Create your admin account at `http://localhost:1337/admin`
2. Define your content types under **Content-Type Builder**
3. Go to **Settings → Users & Permissions → Roles → Public** and enable `find` for each content type the frontend needs to access

---

## Fetching content in Astro

A typed fetch helper is available at `apps/web/src/lib/strapi.ts`:

```typescript
import fetchApi from '@/lib/strapi'

const data = await fetchApi<YourType>({
  endpoint: 'your-content-type',
  wrappedByKey: 'data',
})
```

---

## Available scripts

| Command | Description |
|---|---|
| `pnpm dev` | Start all apps in development mode |
| `pnpm build` | Build all apps |
| `pnpm lint` | Lint all apps |
| `pnpm check-types` | TypeScript type checking |
| `pnpm format` | Format with Prettier |

---



## License

MIT
