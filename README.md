# TokenRouter plugin template

Create native and Vue extensions for TokenRouter plugin API v1. The template includes
a daily check-in implementation, user and administrator pages, an SDK test host, and
a workflow that publishes validated packages for five platforms.

## Create a plugin

1. Use this repository as a template. Replace `github.com/TokenFlux/tokenrouter-plugin-template`
   in `go.mod` and `cmd/plugin/main.go` with your new repository's module path.
2. Replace `example.checkin` in `plugin.json` and `web/vite.config.ts` with your publisher-qualified
   ID. Update the publisher, homepage, descriptions, and license to match your project.
3. Review the declared capabilities. The included reward example requests `wallet.credit`;
   remove permissions your implementation does not need.
4. Run `make test pack` with the versions in `go.mod`, `.node-version`, and `web/package.json`.
   Run `make bootstrap` when changing dependencies, and commit the resulting lockfiles.
5. Update the manifest version and CHANGELOG before creating a matching `v<version>` tag.
   The workflow publishes `plugin.json`, `checksums.txt`, and all five platform archives.

The Go SDK and `@tokenflux/tokenrouter-plugin-sdk` are independently versioned and MIT
licensed. The example requires a compatible host with plugin support and a minimum
host version of 0.6.0. SDK contracts and publication rules are in the
[plugin development guide](https://github.com/TokenFlux/TokenRouter/tree/main/docs/guides/plugins).

## Develop against a host

Run `make dev`, enable `plugins.dev_mode`, and add the absolute `dev/` directory to
`plugins.dev_dirs` in an isolated TokenRouter instance. Restart the plugin after
rebuilding. `pnpm --dir web dev` runs a browser-only mock for interface development;
its balances and records do not establish host persistence.

Plugin code runs with the administrator's trust and is not an operating-system or
browser sandbox. Store business records in host KV and disposable caches in StateDir.
Frontend files are public and must not contain credentials or secret configuration.
The example keeps the first claimed reward amount for idempotent retries and retains
completed records when administrators uninstall without purging plugin data.

The calendar artwork comes from [Lucide](https://github.com/lucide-icons/lucide/blob/66d8f9fc394b8530377e5f6112f0b8908ba01280/icons/calendar.svg).
Its license and attribution are retained below and in `assets/LICENSE.lucide`.

```text
ISC License

Copyright (c) 2026 Lucide Icons and Contributors

Permission to use, copy, modify, and/or distribute this software for any
purpose with or without fee is hereby granted, provided that the above
copyright notice and this permission notice appear in all copies.

THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES
WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF
MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR
ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES
WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN
ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF
OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.

---

The following Lucide icons are derived from the Feather project:

airplay, alert-circle, alert-octagon, alert-triangle, aperture, arrow-down-circle, arrow-down-left, arrow-down-right, arrow-down, arrow-left-circle, arrow-left, arrow-right-circle, arrow-right, arrow-up-circle, arrow-up-left, arrow-up-right, arrow-up, at-sign, calendar, cast, check, chevron-down, chevron-left, chevron-right, chevron-up, chevrons-down, chevrons-left, chevrons-right, chevrons-up, circle, clipboard, clock, code, columns, command, compass, corner-down-left, corner-down-right, corner-left-down, corner-left-up, corner-right-down, corner-right-up, corner-up-left, corner-up-right, crosshair, database, divide-circle, divide-square, dollar-sign, download, external-link, feather, frown, hash, headphones, help-circle, info, italic, key, layout, life-buoy, link-2, link, loader, lock, log-in, log-out, maximize, meh, minimize, minimize-2, minus-circle, minus-square, minus, monitor, moon, more-horizontal, more-vertical, move, music, navigation-2, navigation, octagon, pause-circle, percent, plus-circle, plus-square, plus, power, radio, rss, search, server, share, shopping-bag, sidebar, smartphone, smile, square, table-2, tablet, target, terminal, trash-2, trash, triangle, tv, type, upload, x-circle, x-octagon, x-square, x, zoom-in, zoom-out

The MIT License (MIT) (for the icons listed above)

Copyright (c) 2013-present Cole Bemis

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

```
