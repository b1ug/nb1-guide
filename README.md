# nb1 Guide

<img src="assets/nb1-mascot.webp" alt="The nb1 light companion" width="96" height="96">

Documentation and examples for [nb1](https://github.com/b1ug/nb1), the local blink(1) control toolkit.

The interactive 3D view ships [blink(1) Models](https://github.com/b1ug/blink1-models). The dependency lock pins the exact MK2 source archive. The build verifies the model manifest and copies its assets into the site for same-origin, offline use.

Bilingual documentation for [nb1 v0.1.4](https://github.com/b1ug/nb1/releases/tag/v0.1.4), fixed to core `0a2199cab89621888782baa154522c37ad83b641`. Built with VitePress 1.6.4 and the approved Nightlab presentation. English is the default, with complete Chinese counterparts, local search, the approved nb1 artwork and an optional local 3D model. The static site requests no hardware permission.

Production target: **https://b1ug.github.io/nb1-guide/**. Builds and deployment are distinct: the workflow publishes only a verified main-branch build through GitHub Pages. Deployment status is recorded by the Actions environment.

[Device selection](docs/getting-started.md#choose-among-several-lights) · [Trigger routing](docs/trigger-routing.md) · [Remote MCP and HTTP](docs/remote-access.md)

[简体中文](README.zh-CN.md)

## Read the documentation

| Document | Purpose |
| --- | --- |
| [Overview](docs/overview.md) | Choose a local control path and find the guides. |
| [Get started](docs/getting-started.md) | Install v0.1.4, select a device and explicitly play; preview is optional. |
| [API v1](docs/api-v1.md) | Fields, defaults, constraints, errors and recovery. |
| [Agents](docs/agents.md) | Matching MCP tools and the Skill. |
| [Agent notifications](docs/agent-notifications.md) | Optional Codex turn-ended notifications and their tested scope. |
| [Install](docs/install.md) | Released downloads, Homebrew, foreground server, optional services and upgrades. |
| [Support](docs/support.md) | Diagnostics, ownership, platform and hardware evidence. |
| [Changelog](docs/changelog.md) | Published releases and separately dated historical candidates. |
| [Terminology](docs/api-v1-terminology.md) | Action, Sequence, Step, Job, Pattern and DeviceSequence. |
| [Browser tools](docs/browser.md) | Direct WebHID, the Chrome companion, ownership, privacy and review packages. |
| [Architecture](docs/architecture.md) | The documentation site, separate browser tools and the embedded workbench. |

## Develop and preview locally

Use **Node.js 22.12 or newer** and npm. From a standalone checkout of this repository:

```sh
npm ci --ignore-scripts
npm run build
npm run preview
```

Open `http://127.0.0.1:4175`. The preview serves the generated static build on loopback. For the production project path, run `VITEPRESS_BASE=/nb1-guide/ npm run build` and open `http://127.0.0.1:4175/nb1-guide/` after starting `VITEPRESS_BASE=/nb1-guide/ npm run preview`. For live editing, stop the preview and run:

```sh
npm run dev
```

The development server uses the same loopback address and port. These commands are for documentation development and review; running the hardware toolkit or its daemon is a separate workflow described in the guides.

VitePress is fixed at stable `1.6.4`. Its Vite dependency is explicitly overridden to patched `6.4.6`, within the Vue plugin's supported Vite range. The lockfile pins the complete dependency graph. Dependency updates require rebuilding and checking search and navigation again.

## Sources, generated pages and build receipts

Edit the maintained Markdown in `docs/` and the home pages in `pages/`, together with assets and site configuration. The preparation step creates the ignored `site/` tree, pairs English and Chinese heading anchors, and includes the local fonts and nb1 images. VitePress produces the ignored static `dist/` tree. Generated `site/` and `dist/` files are build outputs rather than content sources.

The build includes raw Markdown as `/source/<source-path>.txt`, the bundled `/api-v1.openapi.json`, `/llms.txt`, and `/content-provenance.json`. `/site-info.json` records source pages and their hashes; `/site-build.json` records generated file hashes, dependency-lock identity and static-link checks. These receipts identify a build, not browser acceptance or hardware qualification. Search and runtime assets are served locally, with no mandatory CDN or tracking requests.

## Sources and scope

The API, OpenAPI, installation and matching MCP/Skill guidance are tied to released core `0a2199cab89621888782baa154522c37ad83b641`. Content provenance records exact upstream and local source hashes. Chinese explanations preserve code identifiers, JSON fields, CLI commands and limits. Historical physical-device and notification records retain their original source and date; the release does not silently renew them.

The [approved nb1 mascot](assets/nb1-mascot.webp) and [favicon](assets/nb1-icon.png) match the embedded workbench. They are the site's only production brand image variants. Language switching is explicit; English remains the default.

## Choose the right project

| Deliverable | What it provides | Who owns the device? |
| --- | --- | --- |
| This documentation site | Static guides, API reference, downloads and examples. | Nobody; the site requests no USB or HID permission. |
| [nb1 Embedded Workbench](https://github.com/b1ug/nb1-debugger) | The local `/demo/` UI served by the nb1 HTTP server. | The running nb1 daemon owns native USB; the page uses its same-origin API. |
| [nb1 WebHID](https://github.com/b1ug/nb1-webhid) | A separate development preview using direct WebHID and a shared Go/WASM compiler. | The browser page or experimental extension, after explicit permission and ownership handoff. |

The Workbench frontend is maintained separately and imported into nb1 as a verified static bundle. It is a UI, not another daemon. The [hosted browser preview](https://b1ug.github.io/nb1-webhid/) has its own release and compatibility policy. Its experimental **nb1 Light Reminders** extension has no Chrome Web Store listing. The [one-minute reminder test](docs/browser.md#load-the-chrome-companion) covers one MK2 on macOS with the popup closed. See [architecture](docs/architecture.md) and [browser tools](docs/browser.md).

The documentation and browser preview are GitHub Pages projects on the same `https://b1ug.github.io` origin. WebHID grants are scoped to the origin, not its project paths. This documentation code makes no HID calls; its path does not isolate browser permissions.

Node.js is required to develop this documentation site or rebuild a frontend. It is not a dependency of an ordinary nb1 Go build. Go modules, optional Git source checkouts and manifest-verified `dist/` assets are different dependency mechanisms; [the build boundary](docs/architecture.md#build-dependencies) explains them. Normal nb1 builds do not need a recursive Git clone or invoke a frontend package manager.

## License

[MIT](LICENSE), copied from nb1 with its existing copyright notice, covers the documentation and theme code. The optional mk2 model uses CC BY-SA 4.0 for enclosure geometry and CC BY-SA 3.0 for the PCB layout and its derived geometry. The site ships both notices and the Three.js MIT license. API documentation retains its source attribution above.

## Nightlab presentation

The docs chrome uses the exact semantic colors and four type roles from the selected `design-nightlab` handoff. Both home pages render the assembled mk2 using the catalog’s studio lighting. The top LED is blue and the bottom LED red. Without WebGL, the two-face illustration displays the same demo colors. It does not compile or play effects and makes no device connection. The optional model assets load on the home route only. Model and Three.js licenses, source hashes and integration changes are recorded in [`public/nightlab/source-receipt.json`](public/nightlab/source-receipt.json). Documentation and API attribution follow the released core; original model geometry, fonts and approved image bytes are preserved.
