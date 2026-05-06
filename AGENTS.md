# Repository Guidelines

## Project Structure & Module Organization

This is the Dujiao-Next customer-facing web frontend, built with Vue 3, TypeScript, Vite, Tailwind CSS, and Pinia.

- `src/views/`: route-level pages for product, checkout, order, auth, and account flows.
- `src/components/`: reusable UI; feature subfolders cover checkout, payment, security, wallet, product, and captcha UI.
- `src/stores/`: Pinia stores for cart, auth, user profile, Telegram Mini App, and buy-now state.
- `src/api/`: API client, endpoint modules, and shared response/types.
- `src/composables/`, `src/utils/`, `src/router/`, `src/i18n/`: shared hooks, helpers, routing, and localization setup.
- `public/`: static assets served directly. Global styles are in `src/style.css`.

## Build, Test, and Development Commands

- `npm ci`: install dependencies from `package-lock.json`; prefer this for clean installs.
- `npm run dev`: start Vite on `0.0.0.0:5173`; `/api` and `/uploads` proxy to `http://localhost:8080`.
- `npm run build`: run `vue-tsc -b` type checking, then create the production build in `dist/`.
- `npm run preview`: preview the built app locally.

The release workflow uses Node.js `24.11.1`, builds on `v*` tags, zips `dist/`, and runs `git-cliff`.

## Coding Style & Naming Conventions

Use Vue single-file components with `<script setup lang="ts">` where possible. Keep TypeScript strict-clean: unused locals/parameters and fallthrough switch cases fail the build. Follow the existing style: 2-space indentation, single quotes, no semicolons, PascalCase component files such as `ProductCard.vue`, and camelCase utilities such as `useProductList.ts`.

Prefer colocating feature-specific UI in component subfolders and keeping shared business logic in `composables` or `utils`.

## Testing Guidelines

No dedicated test runner is currently configured. Before submitting changes, run `npm run build` and manually smoke-test affected flows in `npm run dev`, especially product browsing, checkout, payment, login/register, wallet, and personal center pages. If adding tests, document the script in `package.json` and use clear `*.spec.ts` or `*.test.ts` names.

## Commit & Pull Request Guidelines

History mostly follows Conventional Commit-style prefixes, sometimes bilingual, for example `fix(product): ...`, `feat: ...`, and `ci: ...`. Use a short imperative subject and optional scope.

Pull requests should include a concise summary, verification steps such as `npm run build`, linked issues when applicable, and screenshots for visible UI changes. Note backend/API assumptions when a change depends on server behavior.

## Security & Configuration Tips

Do not commit secrets, tokens, or local backend credentials. Keep API shape changes reflected in `src/api/types.ts`, and sanitize rendered rich content through the existing content utilities rather than bypassing them in views.
