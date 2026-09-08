# kaoju WorkBuddy - Official Release Channel

Trust anchor for kaoju WorkBuddy releases: change notes and checksums are
published here. **Since v0.2.1 the compiled package is also downloadable from
this repository** - the v0.2.1 release carries the master archive as an asset,
by explicit Owner decision on 2026-09-09, reversing the earlier
delivery-after-payment-only policy. Releases before v0.2.1 carry no asset.
Source code remains proprietary and lives in a private repository.

## Releases

| version | status | package | public checksums |
|---|---|---|---|
| 0.2.1 | **Current** - all eight tools fully usable (acquire_paper + acquire_page fixed) | [`kaoju-workbuddy-0.2.1.zip`](https://github.com/Jowitt13/kaoju-release/releases/download/v0.2.1/kaoju-workbuddy-0.2.1.zip) attached to the v0.2.1 release (336,077,009 bytes) | `releases/kaoju-workbuddy-0.2.1/SHA256SUMS.txt` (every file in the package, 4,343 rows) + master-zip sha256 in the v0.2.1 release notes |
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

Earlybird 39 CNY / Standard 69 CNY (one-time buyout). The v0.2.1 package is
nonetheless **freely downloadable from the v0.2.1 release**: there is no
activation step, no activation server and no feature gate (removed in 0.1.1),
so a downloaded copy is a fully working copy. Paying buys support and future
updates - not functionality.

## Integrity

Two checks, in order.

1. Verify the master zip you downloaded (or received) against the digest published in that
   version's release notes. For v0.2.1:

   ```
   sha256 : a5c05fb7efd4f5b6720911c39278ab5135a83952bae3f890f0451fce78dee735
   bytes  : 336,077,009
   ```

2. After unpacking, verify every file from the release directory - the layer
   holding `release.json`:

   ```
   sha256sum -c SHA256SUMS.txt
   ```

`releases/kaoju-workbuddy-0.2.1/SHA256SUMS.txt` in this repository is a byte-for-byte copy of the
manifest inside the package (4,343 rows, 547,289 bytes), so the two can
be compared directly. Its own digest:

```
bbea1ec69633e2966d08f5044f927ecc4b480a4d797b16c66f120b3ee0f1c65f
```

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
