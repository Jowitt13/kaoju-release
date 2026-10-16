<div align="center">

<img src="assets/sculpture.png" alt="kaoju 的红白雕塑视觉" width="720" />

# 考据 kaoju

**世界不止于模型已经知道的**

为 Agent 而生的多源搜索工具，让一个问题连接论文、网页与图像，让搜索继续成为理解

[下载联网版](https://github.com/Jowitt13/kaoju-release/releases/download/v0.4.1/kaoju-setup-0.4.1.exe) · [下载离线版](https://github.com/Jowitt13/kaoju-release/releases/download/v0.4.1/kaoju-setup-0.4.1-offline.exe) · [发布说明](https://github.com/Jowitt13/kaoju-release/releases/tag/v0.4.1)

Windows x64 · MCP · 9 个工具 · 4 个搜索场景

</div>

## 让 Agent 的思考，连接真实世界

模型擅长组织已经学过的知识，而你的下一个问题，往往指向它还没有见过的世界

一篇刚发表的论文，一款刚更新的产品，一座值得细读的建筑，一个正在变化的话题——真正有价值的搜索，不只是找到几个链接，而是找到值得继续追问的方向

kaoju 把多源检索、图文搜索和按需正文采集接入你正在使用的 Agent。让它先找到信息，再展开比较、深入阅读，并把有用的资料留在本地，供下一次任务继续使用

**你提出问题，Agent 组织研究，kaoju 负责向外寻找**

## 搜索可以走得更远

### 从多个来源，打开一个问题

通过统一工具接入网页、学术与开放图像检索来源。论文检索可调用 arXiv、Semantic Scholar、Crossref、OpenAlex 等提供方；图像检索可调用 Wikimedia Commons、Openverse、Met 开放馆藏等来源

不必把问题限制在一种内容或一个站点里。让 Agent 按任务选择来源，围绕研究对象、方法、时间或地点，组织多个子查询

### 从搜索结果，走进正文

`deep_search` 支持多轮检索与结果融合，返回文本和图像候选；需要进一步阅读时，再用采集工具获取网页或论文内容。搜索和采集可以分开：找线索时保持轻量，值得深入时再展开

### 从一次搜索，积累下一次工作的起点

采集的原文与解析文本保存在你指定的本地数据目录。已有资料形成表后，Agent 可以只读查询资料库、回查已采集图片，不必每次都从空白开始

## 四个场景，把能力变成工作方法

随安装提供四个完整 Skills。它们不是四个独立应用，而是让 Agent 围绕不同问题组织检索、筛选和比较的方法

### 论文研究 · `kaoju-paper`

查找相关论文，梳理研究脉络，比较方法与观点，寻找值得继续研究的空白

> 用 kaoju 的论文研究场景，查找 RAG（检索增强生成）的近期论文，按方法分类，比较各自解决的问题与局限

### 竞品调研 · `kaoju-compete`

检索产品官网、功能与定价信息、用户反馈，比较定位、差异与机会

> 用 kaoju 的竞品调研场景，比较我给出的三个产品：先查官方定位、核心功能和定价，再整理用户反馈

### 建筑案例 · `kaoju-arch`

搜索建筑作品、案例页面与参考图，比较场地、空间、类型与设计策略

> 用 kaoju 的建筑案例场景，寻找高密度城区中的小型公共图书馆案例，比较采光、动线与公共空间策略

### 舆情动态 · `kaoju-watch`

按需检索人物、机构、产品或话题的近期信息，整理时间线，并与已有资料比较变化

> 用 kaoju 的舆情动态场景，整理我指定产品过去一个月的重要更新，并与我提供的旧资料比较

场景任务会受实际来源覆盖和客户端能力影响。舆情动态是按需搜索，不包含内置定时监测或自动通知

## 安装，然后连接你的 Agent

### 1. 选择一个安装器

- [**联网安装器**](https://github.com/Jowitt13/kaoju-release/releases/download/v0.4.1/kaoju-setup-0.4.1.exe) · 约 179 KiB：先下载一个小 EXE，运行后获取发行包；安装采集扩展时按需下载依赖和浏览器
- [**离线安装器**](https://github.com/Jowitt13/kaoju-release/releases/download/v0.4.1/kaoju-setup-0.4.1-offline.exe) · 约 913 MiB：提前下载完整安装资源，安装时不再下载依赖和浏览器

当前正式版 **v0.4.1**，面向 **Windows x64**。双击 EXE，按中文向导完成安装即可，无需手动解压。离线版解决的是安装资源下载，搜索在线资料仍需要网络

安装器暂未做数字签名。请从本仓库发布页下载，按随附的 [SHA-256 校验文件](https://github.com/Jowitt13/kaoju-release/releases/download/v0.4.1/SHA256SUMS.txt) 核对；不要关闭系统安全防护

### 2. 在完成页选择「连接 Agent」

向导提供 Codex、Claude Code、DeepSeek Harness、Qoder、WorkBuddy、ZCode、MiMo Desktop、MiniMax Agent、Kimi Code、Hermes 及通用入口，生成对应的配置、命令或接入提示词

按所选入口把提示词或配置交给客户端处理。向导不自动覆盖你的客户端配置；接入时保留已有服务、模型与密钥设置

### 3. 分别确认工具和场景可用

- **MCP 连接**：客户端发现九个工具，并真实调用 `doctor` 检查运行环境
- **Skills 加载**：客户端发现四个场景；不支持原生 Skills 的客户端，可按向导提供的场景任务手动读取对应文件执行
- **开始搜索**：提供研究对象、时间范围与交付要求，明确指定一个场景即可

复制提示词不等于已经接通，MCP 可用也不等于 Skills 已加载。纯云端 Agent 不能直接执行本机 EXE，需要能运行本地 MCP 的客户端环境

<details>
<summary><strong>开发者：九个 MCP 工具</strong></summary>

| 工具 | 能力 |
| --- | --- |
| `deep_search` | 多轮文本与图像候选检索、结果融合 |
| `search_papers` | 多提供方论文与文献检索 |
| `acquire_page` | 浏览器单页采集、正文解析，按需提取图片 |
| `acquire_paper` | 对已注册来源的 URL 发起论文或页面采集 |
| `search_images` | 按文本元数据回查本地已采集图片 |
| `query_library` | 对本地资料表执行只读 SQL |
| `register_source` | 注册采集来源 |
| `get_job_status` | 查询任务状态，取回后台任务结果 |
| `doctor` | 检查当前安装模式的运行就绪状态 |

`deep_search` 返回的是候选结果，不自动下载全部原文或图片；`search_images` 查询的是本地图片记录，不是全网图片搜索。来源可用性、站点访问限制及授权范围会影响实际结果。部分搜索服务可能需要额外配置，安装包不附带第三方服务凭据

收到 `queued`、`running` 或 `truncated` 时，保留 `job_id`，用 `get_job_status` 取回结果，不重复提交同一任务

</details>

## 关于考据

“考据”不是让每一次搜索变得繁琐，而是相信：理解世界，需要不断走向世界

模型提供思考的能力，搜索打开知识的边界。我们希望把寻找、阅读与比较交给同一个工作流，让 Agent 不只回答已经知道的，也能帮助你探索尚未理解的

kaoju 是给 Agent 使用的搜索工具，不是另一个聊天机器人，也不要求你换掉习惯的客户端

---

<details>
<summary><strong>English · Search beyond what your Agent already knows</strong></summary>

kaoju is a multi-source search toolkit for Agents. It connects web, academic and open-image discovery with on-demand page collection and a local library, through nine MCP tools

Four bundled Skills turn those tools into practical workflows: **paper research, competitive research, architectural precedents and topic updates**. Topic updates run on demand; no built-in scheduled monitoring is included

Install on Windows x64, open **Connect Agent**, and follow the client-specific instructions. MCP connection and Skill discovery must be verified separately; clients without native Skills can use the manual scenario prompts

[Online installer](https://github.com/Jowitt13/kaoju-release/releases/download/v0.4.1/kaoju-setup-0.4.1.exe) · [Offline installer](https://github.com/Jowitt13/kaoju-release/releases/download/v0.4.1/kaoju-setup-0.4.1-offline.exe) · [Release notes](https://github.com/Jowitt13/kaoju-release/releases/tag/v0.4.1)

Installers are unsigned. Verify the official download and published SHA-256; do not disable security protection. Offline installation does not make online search available without a network. Provider access and credentials may require additional setup

</details>

[版本记录与下载](https://github.com/Jowitt13/kaoju-release/releases) · [校验与本版说明](releases/kaoju-0.4.1/RELEASE_NOTES.md) · [反馈问题](https://github.com/Jowitt13/kaoju-release/issues)
