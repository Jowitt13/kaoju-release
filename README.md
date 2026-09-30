# kaoju · 考据

[中文](#中文) · [English](#english)

## 中文

kaoju 是一套通过 **MCP** 接入 AI 客户端的资料检索、网页/论文采集与本地存证工具。
它让你从“找到线索”走到“留下可追溯的原文、出处和采集记录”：搜索结果、采集文件、
图片来源和作业状态都有对应的证据记录。适用于论文素材整理、舆情监测、竞品调研、
建筑案例研究等场景；发行包还附带四份对应的场景剧本（Skills）。

它不是一个独立聊天机器人，也不会替你判断资料一定真实或图片一定可商用。
联网检索、网页采集和安装浏览器组件需要网络；采集与检索结果保存在你指定的本地数据目录。

### 能做什么：九个 MCP 工具

| 工具 | 用途 |
| --- | --- |
| `doctor` | 检查安装、依赖、数据目录和可用状态。 |
| `register_source` | 登记要采集的网站/来源；登记默认**不等于启用**。 |
| `search_papers` | 从学术及网页检索来源发现资料，可融合多个来源，并保存检索证据。 |
| `acquire_paper` | 通过高量引擎采集已登记且已启用的来源，保存原文与采集记录。 |
| `acquire_page` | 用浏览器采集已登记来源的单页，解析正文，并可提取图片及其出处。 |
| `query_library` | 对本地资料库做只读查询。 |
| `search_images` | 在已采集的本地图片证据中按文字、来源和时间查找。 |
| `deep_search` | 融合文本与图片线索，给出来源、许可归属和预算轨迹；**只检索，不自动下载**。 |
| `get_job_status` | 用 `job_id` 取回后台作业完整结果，或用 `recent` 查看最近作业摘要。 |

典型流程是：先用 `doctor` 体检 → `register_source` 登记来源 →
`search_papers` / `deep_search` 找线索 → `acquire_paper` / `acquire_page` 留下原文证据 →
`query_library` / `search_images` 回查。耗时工具可能先返回 `job_id` 和
`queued` / `truncated`；此时用 `get_job_status` 取最终结果，不能把“尚未等到”当作失败。
失败会标明 `error_class`，空结果与失败也会区分。图片的许可与署名信息随结果保留；
使用前仍需自行核对具体授权。

### 最近几次更新

| 版本 | 主要变化 |
| --- | --- |
| [v0.3.1（当前）](https://github.com/Jowitt13/kaoju-release/releases/tag/v0.3.1) | 修复 v0.3.0 公开包缺少采集引擎运行时包元数据、导致 `acquire_paper` 失败的问题；随包安装器现生成 `kaoju-mcp.json`。发行构建新增本机回环抓取和安装器 dry-run 闸，防止同类坏包再通过。 |
| [v0.3.0](https://github.com/Jowitt13/kaoju-release/releases/tag/v0.3.0) | 工具从 8 个增至 9 个：新增 `get_job_status`；检索与采集支持后台作业、超时后继续查询、宿主取消；失败分类更清楚，`acquire_page` 的 `timeout_seconds` 改为整次操作总预算（默认 18 秒）。**该公开包的 `acquire_paper` 有缺陷，请升级。** |
| [v0.2.2](https://github.com/Jowitt13/kaoju-release/releases/tag/v0.2.2) | 统一数据根，卸载时保留证据库；修复正常 Wiki 页面被误判为挑战页、随包来源模板无法直接提交、空结果被误报成功等问题；失败采集可定位自己的证据。 |
| [v0.2.1](https://github.com/Jowitt13/kaoju-release/releases/tag/v0.2.1) | 首次把 `acquire_paper` 编译引擎和 `acquire_page` 浏览器扩展一起交付，使当时的八个工具可用；补齐扩展依赖的许可文本。 |

更早的 v0.2.0 已被取代；v0.1.x 有 MCP 协议兼容缺陷，不建议继续使用。
历史版本、校验值和资产原样保留，下载时请按**手中版本**对应的校验值验证。

### 下载、安装与校验（Windows）

当前包：[下载 `kaoju-0.3.1.zip`](https://github.com/Jowitt13/kaoju-release/releases/download/v0.3.1/kaoju-0.3.1.zip)。
它可公开下载、无激活或功能门槛；付费购买的是支持与后续更新，并非功能解锁。

1. 先核对 ZIP 的 SHA-256：

   ```text
   41225cc770355d04e9061680d68b4e2dc6a47cfcb9f43daafad4ea6ae8abb50d
   ```

   PowerShell 可运行 `Get-FileHash .\kaoju-0.3.1.zip -Algorithm SHA256`。
2. 解压，进入含 `release.json` 的目录，再运行随包安装器：

   ```powershell
   .\payload\runtime\kaoju-installer\kaoju-installer.exe --mode install --source . --target "$env:LOCALAPPDATA\kaoju"
   ```

   安装器默认还会安装可选浏览器采集扩展，并从官方渠道下载浏览器及所需依赖；
   `--no-acq` 可跳过扩展，但此时 `acquire_page` 不可用。
3. 将安装器生成的 `<安装目录>\kaoju-mcp.json` 导入你的 MCP 客户端。
   编译运行时不要求你另装 Python。安装后可运行：

   ```powershell
   & "$env:LOCALAPPDATA\kaoju\kaoju-doctor\kaoju-doctor.exe" --package-mode --ddi-home "$env:LOCALAPPDATA\kaoju"
   ```

解压后还可在 `release.json` 所在目录执行 `sha256sum -c SHA256SUMS.txt`
逐文件校验。仓库内的 [`releases/kaoju-0.3.1/SHA256SUMS.txt`](releases/kaoju-0.3.1/SHA256SUMS.txt)
与包内清单逐字节一致（3,832 行）。卸载只移除运行时，非空证据数据目录会保留。

**验证边界：**v0.3.1 候选包经过完整安装、两条采集链路实测和发布后重下载哈希核对；
源码全量测试为 1602 通过、7 失败，并非全绿。失败归因与另外三个编译目标复用的说明
已如实记录在 [v0.3.1 发布说明](https://github.com/Jowitt13/kaoju-release/releases/tag/v0.3.1) 中。

---

## English

### kaoju — official release channel

kaoju is an MCP toolset for finding research material, collecting web pages
and papers, and keeping local, traceable evidence. It plugs into an MCP client;
it is not a standalone chatbot. Search and collection use external network
services, while the resulting evidence is stored under your chosen local data
root. Four scenario Skills cover paper research, monitoring, competitive
research, and architecture case studies.

The nine tools are `doctor` (health), `register_source` (source registry),
`search_papers` (discovery), `acquire_paper` (static/high-volume crawl),
`acquire_page` (browser page capture), `query_library` (read-only data query),
`search_images` (local image evidence), `deep_search` (attributed text/image
research, without downloading), and `get_job_status` (completed or recent jobs).
Long-running calls can return a `job_id`; use `get_job_status` for the final
payload. An empty result is distinct from a failure, and image licensing still
needs human review.

### Quick start (Windows)

Download [`kaoju-0.3.1.zip`](https://github.com/Jowitt13/kaoju-release/releases/download/v0.3.1/kaoju-0.3.1.zip),
verify its SHA-256 in the Integrity section below, and unpack it. From the
directory containing `release.json`, run:

```powershell
.\payload\runtime\kaoju-installer\kaoju-installer.exe --mode install --source . --target "$env:LOCALAPPDATA\kaoju"
```

Import the generated `<install root>\kaoju-mcp.json` into your MCP client.
The compiled runtime needs no separate Python installation. The optional
browser acquisition extension is installed by default and downloads its
dependencies and browsers during installation; `--no-acq` skips it and leaves
`acquire_page` unavailable. Uninstall preserves non-empty local evidence data.

Trust anchor for kaoju WorkBuddy releases: change notes and checksums are
published here. **Since v0.2.1 the compiled package is also downloadable from
this repository** - v0.2.1 and later releases each carry their master
archive as an asset, by explicit Owner decision on 2026-09-09, reversing
the earlier delivery-after-payment-only policy. Releases before v0.2.1
carry no asset, and no published asset is ever removed.
Source code remains proprietary and lives in a private repository.

## Releases

| version | status | package | public checksums |
|---|---|---|---|
| 0.3.1 | **Current** - compiled acquisition hotfix: restores `acquire_paper` and rejects stale compiled installers before release | [`kaoju-0.3.1.zip`](https://github.com/Jowitt13/kaoju-release/releases/download/v0.3.1/kaoju-0.3.1.zip) (274,173,679 bytes) | `releases/kaoju-0.3.1/SHA256SUMS.txt` (3,832 rows) + archive SHA-256 in the v0.3.1 release notes |
| ~~0.3.0~~ | **SUPERSEDED by 0.3.1** - the public package's compiled acquisition engine lacked required distribution metadata, so `acquire_paper` failed; its installer also generated the obsolete `workbuddy-mcp.json` name | [`kaoju-0.3.0.zip`](https://github.com/Jowitt13/kaoju-release/releases/download/v0.3.0/kaoju-0.3.0.zip) retained as historical (266,216,412 bytes) | archive SHA-256 remains in the v0.3.0 release notes |
| ~~0.2.2~~ | **SUPERSEDED by 0.3.0** - field-feedback hotfix round; its evidence-preserving uninstall and other fixes are retained | [`kaoju-workbuddy-0.2.2.zip`](https://github.com/Jowitt13/kaoju-release/releases/download/v0.2.2/kaoju-workbuddy-0.2.2.zip) retained as historical (336,110,525 bytes) | `releases/kaoju-workbuddy-0.2.2/SHA256SUMS.txt` (4,347 rows) + archive SHA-256 in the v0.2.2 release notes |
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

### What v0.3.1 fixes over v0.3.0

- The compiled acquisition engine now ships the runtime distribution metadata
  queried during a crawl, including `lxml`; `acquire_paper` has been verified
  against a loopback source after a full installation.
- Release assembly now performs an offline compiled-engine crawl and a compiled
  installer dry run. A zero exit code without a successful fetch, or an installer
  that writes the obsolete MCP configuration name, blocks the build.
- The release exposes nine MCP tools. The MCP protocol's `serverInfo.version`
  remains `0.13.0`; it is not the distribution version.

### What v0.3.0 added over v0.2.2

- `get_job_status` became the ninth tool: look up a job by `job_id` or inspect
  bounded recent summaries. Heavy search and acquisition calls can continue in
  the background after the server deadline; poll for the completed payload.
- Host cancellation can stop acquisition work or discard late search results.
  Failures include a structured `error_class` rather than being mistaken for
  empty results. `acquire_page` treats `timeout_seconds` as a total operation
  budget, defaulting to 18 seconds.
- The public v0.3.0 archive had a broken `acquire_paper` engine; use v0.3.1.

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

Earlybird 39 CNY / Standard 69 CNY (one-time buyout). The v0.3.1 package is
nonetheless **freely downloadable from the v0.3.1 release**: there is no
activation step, no activation server and no feature gate (removed in 0.1.1),
so a downloaded copy is a fully working copy. Paying buys support and future
updates - not functionality.

## Integrity

Two checks, in order.

1. Verify the master zip you downloaded (or received) against the digest published in that
   version's release notes. For v0.3.1:

   ```
   sha256 : 41225cc770355d04e9061680d68b4e2dc6a47cfcb9f43daafad4ea6ae8abb50d
   bytes  : 274,173,679
   ```

   The superseded v0.3.0 archive remains downloadable. Its digest is preserved
   in the v0.3.0 release notes. The older v0.2.2 archive digest is:

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

`releases/kaoju-0.3.1/SHA256SUMS.txt` in this repository is a byte-for-byte
copy of the manifest inside the v0.3.1 package (3,832 rows, 484,580 bytes),
so the two can be compared directly. Its own digest:

```
27a0ea827616689e68f014f960ecd50d9a1649ca62a77307de7aa665f7a069b5
```

The older `releases/kaoju-workbuddy-0.2.2/SHA256SUMS.txt` is retained
unchanged (4,347 rows, 547,850 bytes); its digest is:

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
