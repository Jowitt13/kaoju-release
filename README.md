# 考据 kaoju · v0.4.0

## 最新安装入口 · 2026-10-12 · v0.4.0 / 安装器修订 v023

- [联网单 EXE](https://github.com/Jowitt13/kaoju-release/releases/download/v0.4.0/kaoju-setup-0.4.0-online-v023.exe)：小体积入口，联网下载发行包及安装依赖
- [离线单 EXE](https://github.com/Jowitt13/kaoju-release/releases/download/v0.4.0/kaoju-setup-0.4.0-offline-v023.exe)：Windows x64，约 910 MiB，自带 Python / uv / 冻结依赖 / 采集浏览器，安装无需下载依赖
- [新版联网 ZIP](https://github.com/Jowitt13/kaoju-release/releases/download/v0.4.0/kaoju-0.4.0-online-v023.zip) · [修订说明与校验附件](https://github.com/Jowitt13/kaoju-release/releases/tag/v0.4.0)

两种 EXE 都含 DeepSeek Harness 的 insert / cwd / serverName 修正，不自动改客户端配置
**未做数字签名**；联网冷下载在本机 30 分钟预算内未完成，暖环境安装通过，网络较慢可选离线版
公开 ZIP 的逐文件下载校验在本机既有代理路径通过，默认直连两次超时，未改系统网络设置
离线版安装后访问网络资料仍需网络；干净 Windows 和全部客户端接入不作验证承诺
产品仍为 v0.4.0，旧附件及 tag 保留；下文旧安装入口和历史校验资料不作为本次新版推荐入口

---


[中文](#中文) · [English](#english)

## 中文

给 Agent 使用的本地研究工具：通过 MCP 检索资料、登记来源、采集网页与论文，
把原文、解析结果、图片出处和校验清单保存在你自己的数据目录

kaoju 不是独立聊天机器人，也不替代原文核对或图片授权核查
检索与采集需要访问外部服务，证据文件保存在本地

**当前版本：[v0.4.0](https://github.com/Jowitt13/kaoju-release/releases/tag/v0.4.0)**
· [下载安装器 EXE（推荐）](https://github.com/Jowitt13/kaoju-release/releases/download/v0.4.0/kaoju-setup-0.4.0.exe)
· [手动安装 ZIP](https://github.com/Jowitt13/kaoju-release/releases/download/v0.4.0/kaoju-0.4.0.zip)
· [发布说明](releases/kaoju-0.4.0/RELEASE_NOTES.md)

### 能做什么

| 工具 | 作用 |
| --- | --- |
| `doctor` | 安装与资料目录体检 |
| `register_source` | 登记采集来源，拒绝覆盖重复来源；登记不等于启用 |
| `search_papers` | 多提供方文献检索，失败也留证据 |
| `acquire_paper` | 采集已登记、已启用来源的 URL |
| `acquire_page` | 浏览器采集单页，保存原文、解析结果与引擎尝试记录，可提取图片出处 |
| `query_library` | 对本地资料表执行只读 SQL |
| `search_images` | 按文字、来源和时间回查本地图片证据 |
| `deep_search` | 多轮文本与图片候选检索，保留来源和预算轨迹；只搜，不自动下载 |
| `get_job_status` | 查询作业与近期摘要，取回后台任务结果 |

随包保留论文、竞品、建筑案例、舆情四个研究剧本（Skills）
舆情剧本不是内建定时监测服务，本版不新增管理面板、证据工作台或自动引文核验
遇到 `queued` / `truncated`，保留 `job_id` 并用 `get_job_status` 查询，不重复提交

### v0.4.0 更新了什么

- 中文图形安装向导：固定尺寸、红白雕塑视觉、思源宋体中文、系统等线英文、可折叠位置设置
- 三动作鸟形阶段动画：每帧约 0.25 秒、整轮约 0.75 秒，不伪造下载百分比
- 浏览器由官方 patchright/playwright CLI 安装，匹配的缓存可复用，不强制重下载
- 安装失败、超时与取消保留诊断；支持重试与明确标注的浏览器降级安装
- 运行中取消按进程树清场，任务和清场均收束后再关闭窗口
- 11 个 Agent 接入入口，导出配置、命令或版本感知提示词，不自动修改客户端配置

### 下载、校验与安装（Windows）

#### 推荐：一个 EXE，双击开始

1. 下载 [kaoju-setup-0.4.0.exe](https://github.com/Jowitt13/kaoju-release/releases/download/v0.4.0/kaoju-setup-0.4.0.exe)
2. 双击运行，联网下载并校验 v0.4.0 发行包后，自动打开原来的中文安装向导，无需手动解压
3. 按向导安装，完成后选择 Agent 接入入口，按说明合并配置并调用 `doctor` 验证

安装器采用透明雕塑图标，大小 180,736 字节；它是**联网安装入口，不是离线包**
需要可访问 GitHub 和官方依赖/浏览器下载服务，且准备阶段至少有 2.5 GiB 临时盘空间
下载包的长度、SHA-256 和内部逐文件清单均校验通过才启动向导
正常退出后自动清理自己的下载临时目录；强杀或断电可能留下临时目录

**本 EXE 未做数字签名**，首次运行可能出现 Windows 安全提示；请核对下载来源和哈希，不要关闭系统防护
EXE SHA-256（[校验文件](https://github.com/Jowitt13/kaoju-release/releases/download/v0.4.0/kaoju-setup-0.4.0.exe.sha256)）：

```text
68926a2f4229199d87225acbcbf98b98de41d2ba4073c00ca319b91318e7b5d4
```

可执行 `Get-FileHash .\kaoju-setup-0.4.0.exe -Algorithm SHA256` 逐字核对
新入口复用以下原始 v0.4.0 ZIP 和向导，原 ZIP、版本 tag、历史校验值不变

#### 手动安装 / 命令行：保留原 ZIP

ZIP：`kaoju-0.4.0.zip`，292,927,113 字节
SHA-256（也提供 [.sha256 校验文件](https://github.com/Jowitt13/kaoju-release/releases/download/v0.4.0/kaoju-0.4.0.zip.sha256)）：

```text
9a5746b50a3c70f4ae004a42adad1bca45ea9967ae2380dc057a6d38525edb1a
```

1. 下载后执行 `Get-FileHash .\kaoju-0.4.0.zip -Algorithm SHA256`，与上面逐字核对
2. 完整解压，进入包含 `release.json` 的发行目录，不要只复制单个 exe
3. 启动图形向导，使用默认位置或展开位置设置：

   ```powershell
   .\payload\runtime\kaoju-installer\kaoju-installer.exe --mode wizard --source .
   ```

默认浏览器采集扩展的安装需要 Python 3.11、`uv`，以及访问官方下载和依赖服务的网络
编译后的 MCP 服务运行不要求另装 Python；浏览器二进制不在 ZIP 内
产品可公开下载，无激活步骤或功能门槛，付费支持不用于解锁功能

如需命令行安装：

```powershell
.\payload\runtime\kaoju-installer\kaoju-installer.exe --mode install --source . --target "$env:LOCALAPPDATA\kaoju" --data-root "$env:LOCALAPPDATA\kaoju\data"
```

`--no-acq` 跳过浏览器扩展，`acquire_page` 将不可用
下载失败时向导可以明确选择「跳过浏览器继续」，CLI 可用 `--skip-browsers` 重试
降级安装不代表浏览器可用；之后从发行目录再次执行正常安装命令补装

解压后的全文件清单有 4,757 行，与仓库内
[`releases/kaoju-0.4.0/SHA256SUMS.txt`](releases/kaoju-0.4.0/SHA256SUMS.txt) 逐字节一致
可在发行目录用 `sha256sum -c SHA256SUMS.txt` 核对
完整包有 4,758 个文件，清单本身不计入自身哈希

### 连接 Agent

完成页选择「连接客户端 / 试一个任务」，提供 Qoder、WorkBuddy、Codex、Claude Code、
DeepSeek Harness、ZCode、其他 Agent / 通用 JSON，以及 MiMo Desktop、MiniMax Agent、
Kimi Code、Hermes 四个提示词入口

先备份原有配置，再按所选入口合并；Codex 使用 TOML，Claude Code 使用 PowerShell 命令
四个提示词入口会要求 Agent 核对当前版本、配置范围和本机 stdio 能力，不猜配置路径
云端 Agent 不能直接运行本机 exe；导出成功不等于已经连接
客户端真实发现九个工具并成功调用 `doctor`，才算连接验证通过

也可以导入安装生成的 `<安装根>\kaoju-mcp.json`
CLI `connect --client` 仅支持 qoder / workbuddy / generic，不等同于 GUI 的 11 个入口
实际采集后还须读取原文并核对 URL、时间、产物路径与清单哈希

### 验收与升级边界

v0.4.0 的四个目标均新编译；已实测正常安装、坏源失败、空缓存降级、运行中取消清场和「完成」退出
已核验 11 个入口的导出；隔离 Codex app-server 真实发现九工具、调用 doctor 并完成本地回环浏览器采集
产物字节数和 SHA-256 与 manifest 一致，不宣称 11 个客户端均已接通

源码全量零 deselect，实际为 **1784 passed、2 failed**，不是全绿
两条失败是已接受的宿主环境差异：新装的外部 DeepSeek Harness 缺少旧浏览器 worker、DDI skill 与设置文件，
导致仓库 doctor 的两个 GOOD 断言失败；测试和判级均未删改
安装后的 package doctor 为 GOOD、nonpass=[]（5 项 PASS、20 项按设计 SKIP），这本身不证明浏览器采集可用

**干净 Windows 首装、活跃或锁定数据库的升级迁移未验证**
升级前备份数据并退出占用资料库的程序，不要在采集中升级
卸载保留非空证据数据目录；应从解压的发行目录运行外部安装器，不在安装目录内自卸载

```powershell
.\payload\runtime\kaoju-installer\kaoju-installer.exe --mode uninstall --target "$env:LOCALAPPDATA\kaoju"
```

### 版本历史

| 版本 | 主要变化 |
| --- | --- |
| [v0.4.0（当前）](https://github.com/Jowitt13/kaoju-release/releases/tag/v0.4.0) | 新 Windows 向导、官方下载与缓存复用、取消清场、失败/降级恢复、11 个 Agent 接入入口 |
| [v0.3.1](https://github.com/Jowitt13/kaoju-release/releases/tag/v0.3.1) | 修复编译采集引擎包元数据和安装器配置文件名，加入编译态安装/采集闸 |
| [v0.3.0](https://github.com/Jowitt13/kaoju-release/releases/tag/v0.3.0) | 九工具、后台作业与取消、失败分类；其公开包的 acquire_paper 有缺陷，已由 v0.3.1 修复 |
| [v0.2.2](https://github.com/Jowitt13/kaoju-release/releases/tag/v0.2.2) | 统一数据根、证据保留卸载、挑战页识别和来源模板修复 |
| [v0.2.1](https://github.com/Jowitt13/kaoju-release/releases/tag/v0.2.1) | 交付两条采集链路与扩展依赖许可文本 |

更早版本与校验文件保留于下方历史档案，请用手中版本对应的哈希，不混用

## English

kaoju is a local research toolkit for MCP-capable Agents: discover sources, collect pages and papers,
and keep originals, parsed artifacts and traceable evidence locally. It is not a standalone chatbot
or a substitute for source and image-license review. Search and collection use external services.

[Download the single EXE installer](https://github.com/Jowitt13/kaoju-release/releases/download/v0.4.0/kaoju-setup-0.4.0.exe)
(180,736 bytes) and verify its SHA-256 above. It downloads and verifies the unchanged v0.4.0 archive,
then opens the original Chinese wizard; manual extraction is not needed. This is online-only, needs
at least 2.5 GiB of temporary free space, and is **unsigned**. Windows may display a security warning;
verify the official source and hash rather than disabling protection. Normal exit removes its own
download directory; forced termination or power loss may leave temporary files.

The [original ZIP](https://github.com/Jowitt13/kaoju-release/releases/download/v0.4.0/kaoju-0.4.0.zip)
remains available unchanged for manual/CLI installation: unpack it, enter the directory containing
`release.json`, then run the wizard command shown above. Browser-extension installation requires Python 3.11, `uv`
and network access; the compiled MCP runtime needs no separate Python. Browsers are downloaded at install time.

This release adds a Chinese Windows wizard, official browser installation with compatible-cache reuse,
explicit failure/degraded recovery, process-tree cancellation, and 11 Agent onboarding exports.
MiMo Desktop, MiniMax Agent, Kimi Code and Hermes are prompt-only entries, not claimed native integrations.
The wizard never edits existing client configuration automatically. Exporting configuration is not proof of connection.

All four targets were newly compiled. Normal installation, bad-source failure, empty-cache degradation,
running cancellation and Finish-button exit were exercised. All 11 exports were checked; an isolated
Codex app-server discovered all nine tools and completed a loopback browser capture with artifact hashes verified.

The full source regression had **1784 passed and 2 failed, zero deselect**. The two owner-accepted failures
are repository-doctor assertions caused by missing legacy components in the host's newly installed external
DeepSeek Harness; they were not removed or hidden. Installed package doctor returned GOOD/nonpass=[]
(5 PASS, 20 by-design SKIP). Clean-Windows installation and active/locked-database migration remain unverified.
Back up data and close programs using the library before upgrading. Source code remains private;
downloaded copies have no activation or feature gate. Historical releases and checksum files are retained below.

---

## Historical archive / 历史档案（v0.3.1 及更早）

以下为旧版发布档案，不代表当前默认下载；原历史条目与校验值保留
The entries below describe earlier releases, not the current default download.


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
