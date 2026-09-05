# kaoju WorkBuddy - Official Release Channel

Trust anchor for kaoju WorkBuddy releases: change notes and checksums are
published here. **Compiled packages are not downloadable from this repository.**
The product is sold by direct delivery, so no release carries a package asset -
that is deliberate, not an oversight. Source code is proprietary and lives in a
private repository.

## Releases

| version | status | package | public checksums |
|---|---|---|---|
| 0.2.0 | **Current** | not published here - delivered privately by the seller after payment | `releases/kaoju-workbuddy-0.2.0/SHA256SUMS.txt` (every file in the package, 2,769 rows) + master-zip sha256 in the v0.2.0 release notes |
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

## Purchase

Earlybird 39 CNY / Standard 69 CNY (one-time buyout).
**Obtain the package from the seller after payment** - install and run.
No activation step, no activation servers, no feature gates (removed in 0.1.1).

## Integrity

Two checks, in order.

1. Verify the master zip you received against the digest published in that
   version's release notes. For v0.2.0:

   ```
   sha256 : 66da6c21ed10a61dfef0092b9255e52452689054769bb37c0dd1bada38115cd8
   bytes  : 222,448,647
   ```

2. After unpacking, verify every file from the release directory - the layer
   holding `release.json`:

   ```
   sha256sum -c SHA256SUMS.txt
   ```

`releases/kaoju-workbuddy-0.2.0/SHA256SUMS.txt` in this repository is a byte-for-byte copy of the
manifest inside the package (2,769 rows, 348,461 bytes), so the two can
be compared directly. Its own digest:

```
eab925795583788accb627d33ea64e509266fcb612d7a146d8191c6782dfd06e
```

The package contains zero source code, zero key material and zero browser
binaries. Browsers are fetched at install time from official download channels,
and only if the optional acquisition pack is installed.

Third-party licence texts ship inside the package under `LICENSES/`, with
`THIRD_PARTY_NOTICES.md` alongside them.
