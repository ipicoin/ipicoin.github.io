# IPI GitHub Pages Preview

Legacy Vue application used to preview IPI web concepts on GitHub Pages.

> **Status: incubating and non-canonical.** The maintained public website source
> is [`www.ipi.io`](https://github.com/ipicoin/www.ipi.io). Content here must not
> be treated as a protocol specification, current network status, or official
> production release unless the canonical project documentation links to it.

## Development

Requires Node.js `20.19` or newer, or `22.12` or newer.

```sh
npm install
npm run dev
npm run build
npm run test:unit
npm run lint
```

End-to-end tests use Playwright:

```sh
npx playwright install
npm run build
npm run test:e2e
```

## License

Licensed under [Apache License 2.0](LICENSE).
