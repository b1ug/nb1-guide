# nb1 Guide

<img src="assets/nb1-mascot.webp" alt="nb1 的小灯伙伴" width="96" height="96">

交互式 3D 视图使用 [blink(1) Models](https://github.com/b1ug/blink1-models)。依赖锁固定 MK2 的源码归档，构建时校验模型清单并复制资源。页面从本站加载模型，也可在本机离线使用。

[nb1](https://github.com/b1ug/nb1) 的文档与示例仓库，让 blink(1) 通过合适的本地软件形态被人和 Agent 使用。

本文档对应 [nb1 v0.1.4](https://github.com/b1ug/nb1/releases/tag/v0.1.4)，固定发行核心 `0a2199cab89621888782baa154522c37ad83b641`。VitePress 1.6.4 提供 28 个英中文页面、本地搜索和已批准的 Nightlab 呈现。默认英文，可显式切换中文，静态站点不申请硬件权限。生产目标为 **https://b1ug.github.io/nb1-guide/**；构建与实际部署分开，由 GitHub Pages workflow 记录发布状态。

[多设备选择](docs/getting-started.zh-CN.md#choose-among-several-lights) · [Trigger 路由](docs/trigger-routing.zh-CN.md) · [远程 MCP 与 HTTP](docs/remote-access.zh-CN.md)

[English](README.md)

## 阅读文档

| 内容 | 作用 |
| --- | --- |
| [导览](docs/overview.zh-CN.md) | 选择本地控制方式、找到各类指南。 |
| [入门](docs/getting-started.zh-CN.md) | 安装 v0.1.4、选设备并显式播放，预览可选。 |
| [API v1](docs/api-v1.zh-CN.md) | 字段、默认、范围、错误与恢复。 |
| [Agent 接入](docs/agents.zh-CN.md) | 同版 MCP 工具与 Skill。 |
| [Agent 通知](docs/agent-notifications.zh-CN.md) | 可选 Codex 回合结束通知及已验范围。 |
| [安装](docs/install.zh-CN.md) | 正式下载、Homebrew、前台服务、可选用户服务与升级。 |
| [支持](docs/support.zh-CN.md) | 排障、设备归属、平台与硬件证据。 |
| [变更记录](docs/changelog.zh-CN.md) | 区分开发候选与历史预发布。 |
| [术语](docs/api-v1-terminology.zh-CN.md) | Action、Sequence、Step、Job、Pattern、DeviceSequence。 |
| [浏览器工具](docs/browser.zh-CN.md) | 直连 WebHID、Chrome 扩展、设备交接、隐私与评审包。 |
| [架构](docs/architecture.zh-CN.md) | 文档站、独立浏览器工具与内嵌工作台的职责。 |

## 本地开发与预览

使用 **Node.js 22.12 或更新版本**及 npm。在本仓库的独立检出目录运行：

```sh
npm ci --ignore-scripts
npm run build
npm run preview
```

打开 `http://127.0.0.1:4175`。预览服务通过回环地址提供生成后的静态页面。生产路径构建用 `VITEPRESS_BASE=/nb1-guide/ npm run build`，预览时用同一环境变量，并打开 `http://127.0.0.1:4175/nb1-guide/`。需要边编辑边预览时，先停止预览，再运行：

```sh
npm run dev
```

开发服务使用同一回环地址与端口。这些命令用于文档开发与评审；硬件工具及其 daemon 的运行方式另见指南。

VitePress 固定为稳定版 `1.6.4`，其 Vite 依赖显式覆盖到已修补的 `6.4.6`，仍在 Vue 插件支持的 Vite 范围内。锁文件固定完整依赖图；更新依赖后需要重新构建，并检查搜索与导航。

## 内容源、生成页面与构建记录

日常编辑维护在 `docs/` 的 Markdown、`pages/` 首页、资源与站点配置中。准备步骤生成被忽略的 `site/` 目录，统一中英文章节锚点，并加入本地字体与 nb1 图像；VitePress 再生成被忽略的静态 `dist/` 目录。`site/` 和 `dist/` 属于构建产物，不是内容源。

本地构建同时提供 `/source/<source-path>.txt` 原始 Markdown、`/api-v1.openapi.json`、`/llms.txt` 与 `/content-provenance.json`。`/site-info.json` 记录源页面及散列；`/site-build.json` 记录产物散列、依赖锁定文件身份和静态链接检查。这些记录说明本地构建情况，不代表浏览器验收或硬件资格。本地提供搜索与运行时资源，无需 CDN 或追踪请求。

## 来源与范围

API、OpenAPI、安装及匹配 MCP／Skill 指引对应发行核心 `0a2199cab89621888782baa154522c37ad83b641`。[内容来源清单](content-provenance.json)记录上游与本地文件散列。中文保持相同代码标识、字段、命令与限制。历史硬件与通知证据保留原始日期和来源，不随新版本自动扩大。

[nb1 定稿形象](assets/nb1-mascot.webp)和 [favicon](assets/nb1-icon.png) 与内嵌工作台一致，是唯一生产品牌衍生。语言通过显式入口切换，默认保持英文。

## 选择合适的项目

| 交付物 | 提供什么 | 谁持有设备？ |
| --- | --- | --- |
| 这个文档站 | 静态指南、API 参考、下载与示例。 | 无；文档站不申请 USB 或 HID 权限。 |
| [nb1 Embedded Workbench](https://github.com/b1ug/nb1-debugger) | 由 nb1 HTTP server 提供的本机 `/demo/` 页面。 | 已运行的 nb1 daemon 持有原生 USB，页面调用同源 API。 |
| [nb1 WebHID](https://github.com/b1ug/nb1-webhid) | 独立开发预览，通过共享 Go／WASM 编译器直接使用 WebHID。 | 浏览器页面或实验性扩展，需显式授权并交接控制权。 |

Workbench 前端独立维护，通过校验后的静态产物导入 nb1；它是 UI，不是另一个 daemon。[在线浏览器预览](https://b1ug.github.io/nb1-webhid/)有独立的发布与兼容性政策；它的 **nb1 Light Reminders** Chrome 扩展仍为实验版本，尚未上架 Chrome Web Store。[一分钟提醒实测](https://b1ug.github.io/nb1-guide/zh/browser#load-the-chrome-companion)覆盖 macOS 上关闭弹窗后点亮一只实体 MK2。详见[架构](docs/architecture.zh-CN.md)与[浏览器工具](docs/browser.zh-CN.md)。

文档站与浏览器预览都是 GitHub Pages 项目，共享 `https://b1ug.github.io` 来源。WebHID 授权按 origin 生效，不按项目路径隔离。文档代码不调用 HID，但所在路径并不提供独立的浏览器权限边界。

开发文档站或重建前端需要 Node.js，普通 nb1 Go 构建不需要。Go module、可选 Git 源码检出和经 manifest 校验的 `dist/` 是不同的依赖机制；[构建边界](docs/architecture.zh-CN.md#build-dependencies)具体说明它们的区别。正常 nb1 构建无需递归克隆 Git，也不运行前端包管理器。

## 许可证

仓库沿用 nb1 的 [MIT 许可证](LICENSE)，保留原有版权声明；API 文档来源如上。

## Nightlab 展示层

文档导航、搜索、菜单、表格和代码区使用交接包的语义配色与四种字号。中英文首页沿用模型目录的场景光照，展示组装好的 mk2。上方 LED 为蓝色，下方 LED 为红色。WebGL 不可用时，双面示意图显示相同的演示颜色。首页按需加载模型，无需连接设备。外壳采用 CC BY-SA 4.0，PCB 布局及其衍生几何采用 CC BY-SA 3.0，Three.js 使用 MIT 许可。来源与接入变更记录见 [`public/nightlab/source-receipt.json`](public/nightlab/source-receipt.json)。原模型几何、字体与品牌图片字节保留；文档与协议说明同步发行来源。
