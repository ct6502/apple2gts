# apple2gts

The Apple IIGS edition of the [Apple2TS](https://apple2ts.com) emulator, served at
**[apple2gts.com](https://apple2gts.com)**.

## What this repository is

This repository contains **no source code**. It exists only to serve the built static site
for `apple2gts.com`, which is a second deployment of the same build published at
`apple2ts.com`.

## Where to contribute

All development happens in **[ct6502/apple2ts](https://github.com/ct6502/apple2ts)** —
bug reports, feature requests, pull requests, and translation updates all belong there.
Nothing in this repository is compiled or hand-edited, so issues and pull requests opened
here cannot be actioned.

## How it is deployed

Deployment is automatic; do not commit to `gh-pages` by hand, because the next deployment
overwrites it.

1. The [`main-build-deploy.yml`](https://github.com/ct6502/apple2ts/blob/main/.github/workflows/main-build-deploy.yml)
   workflow in `ct6502/apple2ts` installs, lints, builds, and tests the app once on every
   push to `main`.
2. That one build is deployed to `apple2ts.com`, then pushed into this repository's
   `gh-pages` branch as a single commit by
   [`JamesIves/github-pages-deploy-action`](https://github.com/JamesIves/github-pages-deploy-action),
   authenticated with a fine-grained token held in the `APPLE2GTS_TOKEN` secret of the
   apple2ts repository.
3. The push to `gh-pages` is followed by a `repository_dispatch` event sent from
   apple2ts, which triggers
   [`deploy-pages.yml`](.github/workflows/deploy-pages.yml) here. That workflow uploads the
   branch contents as a Pages artifact and publishes it with `actions/deploy-pages`.

   The dispatch is required because a `push` trigger would never fire: GitHub runs the
   workflow file found in the pushed ref, and `gh-pages` contains only site files. Use
   *Run workflow* on this repository's Actions tab to redeploy the current `gh-pages`
   contents without a new apple2ts build.

## Credits

- Apple2TS and the Apple II emulator: [Chris Torrence (@ct6502)](https://github.com/ct6502)
- Apple IIGS emulator development: [@anomixer](https://github.com/anomixer)

## License

MIT — see [LICENSE](LICENSE).
