# IPI GitHub Pages Preview

Legacy Vue/Vite scaffold retained to preserve the history of an earlier IPI
GitHub Pages experiment. The maintained website and documentation source is
[`www.ipi.io`](https://github.com/ipicoin/www.ipi.io).

## What the source contains

The current default branch is essentially the generated Vue starter:

- Home and About routes;
- the placeholder counter store and starter styles;
- one generated Playwright check for the starter heading; and
- Vite, linting, formatting, and GitHub Pages workflow configuration.

It does not implement a wallet, explorer, protocol client, or current IPI
product experience. There are no unit test files even though a `test:unit`
script remains in `package.json`.

## Development

```sh
npm install
npm run dev
npm run build
```

The Vite production build succeeds. The generated end-to-end check can be run
with Playwright after installing its browser dependencies:

```sh
npx playwright install
npm run build
npm run test:e2e
```

## Development status

**Legacy scaffold.** This repository is non-canonical and should not be used as
evidence of current IPI functionality, protocol status, or a production release.
New website and documentation work belongs in
[`www.ipi.io`](https://github.com/ipicoin/www.ipi.io).

## License

Licensed under [Apache License 2.0](LICENSE).
