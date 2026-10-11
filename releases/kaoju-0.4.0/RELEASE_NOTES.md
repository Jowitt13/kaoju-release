# 考据 kaoju v0.4.0

给 Agent 使用的本地研究工具：通过 MCP 检索与采集资料，把原文、解析结果、出处和校验清单留在本地
九个 MCP 工具与论文、竞品、建筑案例、舆情四个剧本保留

## 本次更新

- Windows 中文图形向导，固定尺寸、红白雕塑视觉、思源宋体中文、系统等线英文和可折叠位置
- 三帧鸟形阶段动画，每帧约 0.25 秒、整轮约 0.75 秒，不显示虚假的下载百分比
- 官方 patchright/playwright CLI 浏览器安装，兼容缓存可复用，不强制重下载
- 失败与超时保留诊断，支持重试和明确标注的浏览器降级安装
- 取消按进程树清场，安装任务与清场均收束后才正常关闭，清场异常可见
- 11 个 Agent 接入入口，复制配置、命令或接入提示词，不自动改客户端配置
  MiMo Desktop、MiniMax Agent、Kimi Code、Hermes 为提示词入口，不宣称原生集成已验证

## 下载与安装

下载附件 `kaoju-0.4.0.zip` 及 `kaoju-0.4.0.zip.sha256`，核对后完整解压
不要只复制安装器 exe，在包含 `release.json` 的发行目录运行：

```powershell
.\payload\runtime\kaoju-installer\kaoju-installer.exe --mode wizard --source .
```

默认浏览器扩展安装需要 Windows、Python 3.11、`uv` 和访问官方服务的网络
编译 MCP 运行时不需要另装 Python，浏览器不在 ZIP 内
导出配置后需由客户端实际发现九工具并调用 doctor；复制成功不等于已连接
产品公开下载，无激活步骤或功能门槛

```text
file    : kaoju-0.4.0.zip
bytes   : 292927113
sha256  : 9a5746b50a3c70f4ae004a42adad1bca45ea9967ae2380dc057a6d38525edb1a
files   : 4758
hashes  : 4757 (SHA256SUMS.txt does not hash itself)
source  : 59f9167a6662ce2415507368a09eb41a096b27cf
```

[逐文件校验清单](https://github.com/Jowitt13/kaoju-release/blob/v0.4.0/releases/kaoju-0.4.0/SHA256SUMS.txt)
与 ZIP 内清单逐字节一致；从发行目录可用 `sha256sum -c SHA256SUMS.txt` 核对
源码提交是编译输入身份，源码仓库保持私有；安装器资格基线 v0.20 不是产品版本号

## 实测结果与限制

- 四个目标均新编译，非旧 dev0 包改名；ZIP 全文件哈希、图片、字体与 88 项源码输入核验通过
- 编译向导已实测正常安装、坏源失败、空缓存降级、运行中取消清场和「完成」退出
- 11 个入口导出合同核验通过；隔离 Codex app-server 接通九工具并完成本地回环浏览器采集，
  实际产物字节数与 SHA-256 与 manifest 全等；不扩张为 11 个真实客户端均已接通
- 安装器与打包子集 281 passed；零 deselect 全量实际为
  **2 failed, 1784 passed, 1 warning in 581.87s**，EXIT=1，不是全量全绿
- 两条失败为已接受的宿主差异：`test_readiness_block_contract` 与
  `test_repo_mode_needs_no_flag_and_stays_good` 的仓库 doctor GOOD 断言
  新装外部 DeepSeek Harness 缺少旧 browser worker、DDI skill 与设置文件，对应检查 SKIP
  原测试、doctor 判级与失败记录未改变，其他全量测试无失败
- 已装包 doctor GOOD、nonpass=[]（5 PASS、20 按设计 SKIP）；降级安装的 GOOD 不表示浏览器可用
- 干净 Windows 首装、活跃或锁定数据库迁移未验证；升级前备份并退出占用资料库的程序
- 正常安装的缓存复用仅按三项浏览器二进制 SHA-256/mtime 核对，不声称整棵缓存逐文件比较
- 本版不新增管理面板、证据工作台、自动引文核验或内建持续监测系统

## English

kaoju v0.4.0 focuses on a new Windows installer wizard, official browser downloads with compatible-cache reuse,
explicit failure/degraded recovery, process-tree cancellation and 11 Agent onboarding exports.
Unpack the complete ZIP and launch the wizard from the directory containing `release.json` using the command above.
Browser-extension installation requires Python 3.11, `uv` and network access; the compiled MCP runtime does not.

All four targets were newly compiled. Normal/bad-source/degraded/cancel/Finish flows were exercised;
11 exports were checked and an isolated Codex app-server performed a real loopback browser capture.
Full source regression: **1784 passed, 2 owner-accepted host-dependent repository-doctor failures, zero deselect**.
Installed package doctor was GOOD/nonpass=[]; this is not itself proof that browser acquisition is available.
Clean-Windows installation, active/locked-database migration and real integration of all 11 clients remain unverified.
Back up data and close programs using the library before upgrading. No previous releases or checksums were removed.

## 2026-10-12 补充：单 EXE 联网安装入口

[kaoju-setup-0.4.0.exe](https://github.com/Jowitt13/kaoju-release/releases/download/v0.4.0/kaoju-setup-0.4.0.exe)
为新增联网入口，使用透明雕塑图标，双击后下载并校验原 v0.4.0 ZIP 与内部清单，再启动原中文向导
无需手动解压，不是离线版；原 ZIP、旧附件、tag 与其校验值全部保留不变

```text
file   : kaoju-setup-0.4.0.exe
bytes  : 180736
sha256 : 68926a2f4229199d87225acbcbf98b98de41d2ba4073c00ca319b91318e7b5d4
```

[EXE 校验文件](https://github.com/Jowitt13/kaoju-release/releases/download/v0.4.0/kaoju-setup-0.4.0.exe.sha256)
本 EXE 未做数字签名，不声称 SmartScreen 信誉验证；请从官方页面下载并核对哈希
准备阶段至少需要 2.5 GiB 临时盘空间，原有 Python 3.11 / uv / 官方网络要求不变
正常退出清理自己的临时目录；强杀或断电不保证清理

包装器目标测试 24 passed；完整源码回归 1808 passed / 2 failed，零 deselect
两条仍是上文已接受的宿主 doctor 差异，不冒称全绿
前一包装候选已实测完整安装、完成按钮退出和临时目录清理；图标修订另以真实编译验证全部七个 ICO 尺寸嵌入
未重复宣称新一轮全部 GUI 状态或干净 Windows 验收

The new **unsigned, online-only** single EXE entry verifies and opens the original v0.4.0 package
without manual extraction. The original ZIP and tag are unchanged. The wrapper has 24 passing tests;
full regression is 1808 passed plus the same two accepted host-doctor failures, zero deselect.
