# Chatter Backend

A TypeScript/NestJS backend for the Chatter application. This service provides the server-side APIs and app server configuration for the Chatter ecosystem.

- Repository: [HarshXAI/chatter-backend](https://github.com/HarshXAI/chatter-backend)
- Language: TypeScript
- Framework: NestJS
- Default branch: main

## Features

- Modular, scalable architecture using NestJS
- Environment-based configuration
- Production build output in `dist/`
- Ready for CI/CD (AWS CodeBuild via `buildspec.yml`)
- Procfile included for platform runtimes that use process types (e.g., Heroku)

Note: This README outlines the common workflows and conventions for a NestJS service. Adjust sections (DB, auth, docs) to match your actual implementation.

## Quick Start

### Prerequisites
- Node.js 18+ (recommended Node 20 LTS)
- PNPM, NPM, or Yarn
- A `.env` file with your configuration (see below)

### Install

Using pnpm (preferred, pnpm-lock.yaml present):
```bash
pnpm install
```

Using npm:
```bash
npm ci
```

Using yarn:
```bash
yarn install
```

### Development

```bash
# Start in watch mode
pnpm start:dev
# or
npm run start:dev
# or
yarn start:dev
```

The service typically listens on `http://localhost:3000` unless overridden by `PORT` in `.env`.

### Production build and run

```bash
# Build the project to dist/
pnpm build
# or
npm run build
# or
yarn build

# Start compiled app
pnpm start:prod
# or
npm run start:prod
# or
yarn start:prod
```

### Testing

```bash
# Unit tests
pnpm test

# Watch mode
pnpm test:watch

# e2e tests (if configured)
pnpm test:e2e

# Coverage
pnpm test:cov
```

(Replace `pnpm` with your package manager as needed.)

## Environment Variables

Create a `.env` file at the project root. Common variables for a NestJS service include:

```
# Core
NODE_ENV=development
PORT=3000

# CORS
CORS_ORIGIN=http://localhost:3000

# Auth (if applicable)
JWT_SECRET=change_me
JWT_EXPIRES_IN=1d

# Database (if applicable)
DATABASE_URL=postgres://user:password@localhost:5432/chatter

# Cache/Queue (optional)
REDIS_URL=redis://localhost:6379

# Logging
LOG_LEVEL=info
```

Only keep variables relevant to your implementation; remove the rest.

## Project Structure

```
.
├─ .vscode/                 # Editor settings (optional)
├─ dist/                    # Compiled output (generated)
├─ public/                  # Static assets (if served)
├─ src/                     # Application source
│  ├─ main.ts               # Entrypoint (bootstrap)
│  ├─ app.module.ts         # Root module
│  └─ ...                   # Feature modules, services, controllers
├─ test/                    # Tests
├─ nest-cli.json            # Nest CLI config
├─ tsconfig.json            # TypeScript config
├─ tsconfig.build.json      # TS build config for Nest
├─ buildspec.yml            # AWS CodeBuild spec
├─ Procfile                 # Process definition (e.g., Heroku)
├─ package.json
└─ README.md
```

## API Documentation

If Swagger/OpenAPI is enabled in `main.ts`, the docs are typically available at:
- Local: `http://localhost:<PORT>/docs` or `/api`

Update this section with the exact path if configured.

## Scripts

Common NestJS scripts (check your `package.json` for exact script names):

- `start` — Start the app
- `start:dev` — Start with hot reload (watch mode)
- `start:prod` — Start compiled app from `dist/`
- `build` — Compile TypeScript to `dist/`
- `test`, `test:watch`, `test:e2e`, `test:cov` — Testing scripts
- `lint` — Lint source code
- `format` — Format code

## Deployment

### Heroku / Platforms using Procfile
A `Procfile` is present. Typical content:
```
web: node dist/main.js
```
Ensure you build before starting (e.g., with a prestart hook or build step in the platform).

### AWS CodeBuild
A `buildspec.yml` is present for CI/CD. Confirm the phases (install/build/post_build) match your build pipeline, and that environment variables and credentials are configured in your CI/CD environment.

### General Notes
- Always build (`npm run build`) before starting in production.
- Ensure `.env` or platform environment variables are set for production (secrets, DB URLs, etc.).
- Use a process manager (PM2) or platform supervisor for reliability if running on a VM.

## Contributing

1. Fork the repo and create your branch from `main`.
2. Install dependencies and set up `.env`.
3. Run `start:dev` and ensure tests pass.
4. Commit with conventional messages if possible.
5. Open a pull request describing your changes.

## Troubleshooting

- Port already in use: update `PORT` in `.env` or free the port.
- Build errors: clear cache, reinstall deps, ensure Node/TS versions match.
- TypeScript path issues: verify `tsconfig.json` and `tsconfig.build.json`.
- Swagger not visible: confirm Swagger is set up in `main.ts` and the environment allows it.

## License

No license specified. Consider adding a LICENSE file (e.g., MIT, Apache-2.0) to clarify usage.

## Contact

- Maintainer: [@HarshXAI](https://github.com/HarshXAI)
- Issues: Use the repository’s Issues tab to report bugs or request features.

---
Generated for a NestJS TypeScript backend. Tailor database/auth/docs sections to your exact setup.
