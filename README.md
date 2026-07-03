# ipicoin.github.io

> publications preview of github projects

This template should help get you started developing with Vue 3 in Vite.

See [Vite Configuration Reference](https://vite.dev/config/).

## Showcase (Fala 5)

Strona główna prezentuje **Showcase projektów organizacji IPI** — uporządkowany
katalog repozytoriów org (rdzeń, wallet, apki, hardware, infra, fork) z
filtrowaniem po kategorii i statusie.

- Źródło danych: [`src/data/projects.json`](src/data/projects.json) —
  pola: `name`, `description`, `category`, `status`, `url`, `language`, `fork`.
- Komponent: [`src/components/ProjectShowcase.vue`](src/components/ProjectShowcase.vue)
  — renderuje karty i realizuje filtrowanie (reaktywne `computed`).
- Podłączenie: [`src/views/HomeView.vue`](src/views/HomeView.vue).

Aby dodać nowy projekt, wystarczy dopisać wpis do `projects.json` — karty
generują się automatycznie. Realizacja zadania
[[Fala 5] Showcase projektów org](https://github.com/ipicoin/universal-independency-declaration/issues/1).

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```

### Run Unit Tests with [Vitest](https://vitest.dev/)

```sh
npm run test:unit
```

### Run End-to-End Tests with [Playwright](https://playwright.dev)

```sh
# Install browsers for the first run
npx playwright install

# When testing on CI, must build the project first
npm run build

# Runs the end-to-end tests
npm run test:e2e
# Runs the tests only on Chromium
npm run test:e2e -- --project=chromium
# Runs the tests of a specific file
npm run test:e2e -- tests/example.spec.ts
# Runs the tests in debug mode
npm run test:e2e -- --debug
```

### Lint with [ESLint](https://eslint.org/)

```sh
npm run lint
```
