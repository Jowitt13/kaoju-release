# kaoju WorkBuddy - Official Release Channel

Trust anchor for kaoju WorkBuddy releases: change notes and checksums are
published here. **Since v0.2.1 the compiled package is also downloadable from
this repository** - the v0.2.1 and v0.2.2 releases each carry their master
archive as an asset, by explicit Owner decision on 2026-09-09, reversing
the earlier delivery-after-payment-only policy. Releases before v0.2.1
carry no asset, and no published asset is ever removed.
Source code remains proprietary and lives in a private repository.

## Releases

| version | status | package | public checksums |
|---|---|---|---|
| 0.2.2 | **Current** - field-feedback hotfix round. The data root is now unified, so **uninstalling no longer deletes your evidence library**; wiki pages are no longer misjudged as bot-challenge pages and dropped; the source templates that ship with the playbooks validate as-is instead of being rejected; an empty result set is no longer reported as a success; and a failed acquisition now points at its own evidence files | [`kaoju-workbuddy-0.2.2.zip`](https://github.com/Jowitt13/kaoju-release/releases/download/v0.2.2/kaoju-workbuddy-0.2.2.zip) attached to the v0.2.2 release (336,110,525 bytes) | `releases/kaoju-workbuddy-0.2.2/SHA256SUMS.txt` (every file in the package, 4,347 rows) + master-zip sha256 in the v0.2.2 release notes |
| ~~0.2.1~~ | **SUPERSEDED by 0.2.2** (its uninstaller could delete the evidence library: the installer and the compiled runtime disagreed about where the data root was, so the uninstall preserved one path and removed the other. All eight tools were usable; fixed in 0.2.2) | asset RETAINED - still downloadable from the v0.2.1 release (336,077,009 bytes); historical release entries and assets are never rewritten or removed | `releases/kaoju-workbuddy-0.2.1/SHA256SUMS.txt` (kept, historical; 4,343 rows) + master-zip sha256 in the v0.2.1 release notes |
| ~~0.2.0~~ | **SUPERSEDED by 0.2.1** (pre-launch build: acquire_paper structurally dead and acquire_page extension never shipped in the compiled package; never distributed to a customer) | no asset; kept as honest history | `releases/kaoju-workbuddy-0.2.0/SHA256SUMS.txt` (kept, historical) |
| ~~0.1.1~~ | **DEPRECATED** - unusable with a spec-compliant MCP client (protocol defect, fixed in 0.2.0) | no asset; a zip asset was published once and has been removed | `releases/kaoju-workbuddy-0.1.1/SHA256SUMS.txt` (archive level only) |
| ~~0.1.0~~ | **DEPRECATED** - same protocol defect; also carried the since-removed activation flow | no asset; removed | `releases/kaoju-workbuddy-0.1.0/SHA256SUMS.txt` (archive level only) |

### Why 0.1.x is deprecated

MCP 2024-11-05 requires `CallToolResult.content` to be an **array of content
blocks**. 0.1.0 and 0.1.1 returned the payload object itself in that position,
so a spec-compliant client rejected the return value of **all eight tools**: the
server started and listed its tools, then every call failed on the client side.
Those versions also answered `ping` with JSON-RPC `-32601 method not found`,
where the specification requires an empty result, so a client keepalive could
drop the session.

Both are fixed in 0.2.0 and guarded by a permanent conformance suite anchored to
the specification text rather than to the implementation's output shape.

### What v0.2.2 adds over 0.2.1

A hotfix round driven by the first real-world field report. Nothing here changes
the tool face: v0.2.2 still exposes the same eight tools, and `serverInfo.version`
stays at `0.10.0` (a separate namespace from the release version).

- **The data root is unified, so uninstalling preserves your evidence.** In 0.2.1
  the installer resolved the data root one way and the compiled runtime another,
  and the generated MCP configuration carried no `DDI_DATA_HOME`, so the two could
  never agree. Uninstall preserved the path the marker recorded and deleted the
  path the runtime actually wrote - which is where the evidence library lives.
  The MCP configuration now injects `DDI_DATA_HOME` (agreement by construction),
  the runtime falls back to the install marker, an inherited environment that
  would resolve outside the install target is refused loudly instead of silently
  adopted, pre-existing data is migrated idempotently, and uninstall now preserves
  **every** non-empty candidate root and reports which ones it kept, leaving a
  `KAOJU_UNINSTALL_NOTE.txt` inside the preserved root.
- **Wiki pages are no longer thrown away as bot-challenge pages.** The block
  detector matched challenge markers against the first 4000 characters of raw
  HTML, where MediaWiki's own `mw.config` key names (`...CaptchaNeededForGenericEdit`,
  `...ForceShowCaptcha`, `...HCaptchaSiteKey`) live in `<head>` scripts. Markers now
  match **visible text only**, and a challenge verdict additionally requires the
  visible text to be short (a challenge page is a door, not an article), so a real
  article that merely mentions a captcha is no longer rejected by both engines.
- **The shipped source templates validate as-is.** The playbooks said "templates
  are in `source_templates/`" while the real schema is flat with unknown keys
  forbidden, and the shipped templates were nested - so following the official
  template was guaranteed to fail. Templates are now the source payload verbatim;
  the reconnaissance records moved to sibling files under `source_templates/recon/`
  and are not submitted to the API.
- **An empty result set is no longer reported as a success.** The response carries
  a three-state `outcome` (`ok` / `empty` / `failed`) projected from the five-state
  provider status, and a provider failure is never laundered into `empty` or `ok`.
  Vendor envelope telemetry (`total_results`, `search_time_ms`) now survives a
  zero-result response instead of vanishing with the result list.
- **A failed acquisition points at its own evidence.** Failure responses carry
  `failure_evidence` naming the run's `acq-result.json` and `acq-spec.json`, so the
  per-engine reasons are reachable instead of having to be guessed.
- **The playbooks carry field-feedback discipline**: one entity per `sub_query`,
  a timeout is not a failure and where the failure evidence actually lands, how to
  tell a truncated result set from the whole corpus, and that `outcome: "empty"` is
  not `outcome: "ok"`.

### What v0.2.1 adds over the superseded 0.2.0 pre-launch build

- `acquire_paper` (high-volume engine) is compiled into the package and works
  (the pre-launch 0.2.0 build could never run it);
- `acquire_page` (browser single-page acquisition) works: the optional
  `kaoju-acq` extension now SHIPS with the release source and installs at
  install time (dependencies via the frozen lock, browsers via official
  download channels);
- the worker domain is decoupled from the compiled core (raw markdown across
  the boundary, ParseResult rebuilt and contract-checked on the MCP side);
- licensing extended to the extension domain (`LICENSES/acq/` plus the
  vendored LGPL-2.1 text for the install-time ffmpeg binary).

## Purchase

Earlybird 39 CNY / Standard 69 CNY (one-time buyout). The v0.2.2 package is
nonetheless **freely downloadable from the v0.2.2 release**: there is no
activation step, no activation server and no feature gate (removed in 0.1.1),
so a downloaded copy is a fully working copy. Paying buys support and future
updates - not functionality.

## Integrity

Two checks, in order.

1. Verify the master zip you downloaded (or received) against the digest published in that
   version's release notes. For v0.2.2:

   ```
   sha256 : 6e602233a4628e923248a1deeb1d8e23db9d5a82d09e75a1ea6da126d8df2695
   bytes  : 336,110,525
   ```

   The superseded v0.2.1 archive is still downloadable and its digest is
   still published in the v0.2.1 release notes:

   ```
   sha256 : a5c05fb7efd4f5b6720911c39278ab5135a83952bae3f890f0451fce78dee735
   bytes  : 336,077,009
   ```

2. After unpacking, verify every file from the release directory - the layer
   holding `release.json`:

   ```
   sha256sum -c SHA256SUMS.txt
   ```

`releases/kaoju-workbuddy-0.2.2/SHA256SUMS.txt` in this repository is a byte-for-byte copy of the
manifest inside the package (4,347 rows, 547,850 bytes), so the two can
be compared directly. Its own digest:

```
d73bdd4595471442602a6007e7972ef42687f903ce9a35ff7ac600b8caacf2b2
```

`releases/kaoju-workbuddy-0.2.1/SHA256SUMS.txt` is kept alongside it, unchanged
(4,343 rows, 547,289 bytes, digest
`bbea1ec69633e2966d08f5044f927ecc4b480a4d797b16c66f120b3ee0f1c65f`).

The package's compiled runtime contains zero source code, zero key material and
zero browser binaries. The optional acquisition extension ships as five small
readable worker modules (an explicit Owner decision) with its dependency
install and browser downloads happening at INSTALL TIME from official channels.
Browsers are fetched only if the extension is installed (it is part of the
default install; `--no-acq` skips it).

Third-party licence texts ship inside the package under `LICENSES/`, with
`THIRD_PARTY_NOTICES.md` alongside them - now covering BOTH dependency domains
(the compiled runtime corpus and the acquisition-extension corpus), including
the LGPL-2.1 text for the install-time ffmpeg binary.
