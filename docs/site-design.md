# ForceSplit 官方网站 — 需求与设计说明

> 状态：已定稿（v0.9.0 初版） · 日期：2026-09-26
> 本文档先于代码存在；任何口径变更须先回写本文档，再改代码。

## 1. 需求

为 ForceSplit（数据文件按字段规则拆分工具，Windows 桌面应用，微软商店分发）建设官方产品站，
站点结构、样式骨架与赞助区实现参照同作者 PassGone 官网仓库，配色取自 ForceSplit 应用图标主色。

- **域名**：`https://forcesplit.weibaba.fun`（全局第 12 条与 rules/website.md 15.1 默认口径）。
- **发布方式**：GitHub 网站仓库 → Cloudflare Pages 静态托管，生产分支 `main`，仓库根即站点根。
- **隐私红线（硬性）**：纯静态、零追踪——无统计/分析脚本、无外部请求（无 CDN 字体、外链图片、
  外链 CSS/JS）、无 Cookie、无表单、无服务端；所有资源本地引用。
  仓库内不得出现用户数据、操作日志、凭据或本地路径。
- **下载入口**：微软商店 `https://apps.microsoft.com/detail/9MXMRG84K642`（唯一权威渠道）。
- **反馈邮箱**：`feedback@weibaba.fun`（全局第 12 条默认口径）。
- **产品口径来源**（权威，禁止编造）：ForceSplit 应用仓库。当前版本为公测版 v0.9.0（2026-09-26）。

## 2. 品牌配色（取自应用仓库图标 store/ico/app_icon.png，像素取色）

| 用途 | 变量 | 值 | 来源 |
|---|---|---|---|
| 品牌深蓝（主标题/强调） | `--accent-deep` | `#0C4978` | 大文档描边 |
| 品牌亮蓝（链接/次强调） | `--accent` | `#1467A3` | 深蓝提亮派生 |
| 拆分橙（CTA/点缀） | `--orange` | `#FB5E00` | 中央拆分箭头 |
| 拆分橙 hover | `--orange-d` | `#D94F00` | 橙色加深 |
| 青绿 | `--teal` | `#0F8081` | 青色小文档描边 |
| 叶绿（图标点缀） | `--green` / `--green-d` | `#7EC76B` / `#4E9B3C` | 绿色小文档描边 |
| Hero 渐变 | — | `#062B47 → #0C4978 → #1467A3` | 深蓝渐变 |
| 正文墨色 | `--ink` | `#16283A` | 偏蓝深墨 |
| 背景 | `--bg` | `#F2F7FA` | 图标底蓝 `#E7F0F7` 提亮派生 |

图标构成：浅蓝底圆角方形，蓝色数据文档被橙色箭头拆分，流向蓝 / 青 / 绿三份子文档——「一表拆多表」。

## 3. 站点结构

```
/                     中文主站（lang=zh-CN）
/en/                  English（lang=en）
/privacy/             隐私政策（中英同页切换，中文为主）
/assets/style.css     全站唯一样式（PassGone 版式骨架 + ForceSplit 配色，含隐私页样式）
/assets/img/          logo.png（应用源图标 1024，兼 og:image）、donate_qr.jpg（各产品仓共用收款码）
/favicon.ico|.png、/apple-touch-icon.png   由应用源图标派生（48 / 128 / 180）
/robots.txt /sitemap.xml /_headers /.well-known/security.txt
README.md AGENTS.md docs/site-design.md .gitignore
```

主站信息架构（锚点）：**Hero（定位 + 下载 CTA）→ 拆分规则 `#rules`（7 卡）→
功能亮点 `#features`（6 卡）→ 内置基础数据 `#data`（3 统计卡）→ 本地处理 `#local`（承诺框 + CTA）→
赞助（咖啡弹层）→ 页脚**。英文版 `/en/` 逐节对应。

### 3.1 图像资产派生（PIL，源图 1024，脚本化禁止手改）

| 文件 | 尺寸 | 来源 |
|---|---|---|
| `assets/img/logo.png` | 1024×1024 | 应用源图标原样（兼 og:image） |
| `favicon.png` | 128×128 | 源图 LANCZOS 缩放 |
| `apple-touch-icon.png` | 180×180 | 源图 LANCZOS 缩放 |
| `favicon.ico` | 48×48 | 源图 LANCZOS 缩放 |
| `assets/img/donate_qr.jpg` | 1304×1777 | 复制自 PassGone 官网仓库（各产品共用同一张微信收款码） |

## 4. 页面文案定稿记录

- **一句话定位**：「不懂技术，也能把数据表按规则拆成多份。」正式表述：数据文件按字段规则拆分工具，
  XLSX / XLS / CSV 按业务规则拆分成多个文件。
- **七条拆分规则**（逐字口径）：按字段值（逐户）、按行政区划（身份证号/纳税人识别号/区划代码 →
  省/市/县三级，扁平或分层目录）、按日期（年/季/月/周/日）、按数值区间、按前缀/关键字、按行数、
  按手机归属地（省/市 + 运营商）。
- **功能亮点**：拆分前预览与预处理确认、行数守恒核对、输出字段过滤、拆分方案复用、
  内置基础数据（行政区划 2023 版、手机号段 490,000 条等 8 个数据集，应用内可管理、可编辑）、
  单表 200,000 行自动续 sheet、全程本地处理零上传。
- **隐私政策 `/privacy/`**：以应用仓库 PRIVACY.md 为源、不增删事实，措辞保守不扩。
  收录事实仅限：本地处理全部数据；无网络请求、无遥测、无广告；应用内除点击官网/隐私/下载链接
  （调用系统浏览器）外不访问网络；设置与方案存储于本机用户目录；内置基础数据可编辑；
  联系方式 feedback@weibaba.fun。生效日期 2026-09-26。
- **赞助区**（rules/website.md 15.3 强制）：标题「拆得顺手？请作者喝杯咖啡」+ 行尾跳动 ☕ 按钮
  （`animation: coffee-bounce 2s ease-in-out infinite`），点击弹收款码 fixed 模态，点空白关闭；
  英文版 "Buy the developer a coffee ☕"。
- **定价口径缺席的处理**：当前无免费/付费分阶口径，故下载按钮只用「从微软商店下载 / 获取公测版」，
  不出现「免费」字样，不设版本对比表，JSON-LD 不含 offers。
- **使用条款缺席的处理**：未获权威条款文案，主站不设使用条款节；赞助区置于页脚之前（页面底部）。
  待用户提供条款口径后于本节登记并补建。

## 5. 版本表

| 版本 | 日期 | 说明 |
|---|---|---|
| v0.9.0 | 2026-09-26 | 初版：中文主站、英文版、隐私政策（中英同页）、全站样式、图像资产派生、robots/sitemap/_headers/security.txt、README 与 AGENTS；对应公测版 v0.9.0 |
| v0.9.1 | 2026-09-26 | 反馈邮箱统一为 feedback@weibaba.fun（全局规范第 12 条修订），全站同步 |
| v0.9.0（同版修订） | 2026-09-26 | 反馈邮箱按全局规则第 12 条统一 feedback@weibaba.fun（AGENTS.md 修正，页面/security.txt 原已符合） |
| v0.9.2 | 2026-09-28 | 中文名「庖丁解表」与新标语全站启用（「千表万行，游刃解之」，中英同步，品牌与 SEO 元数据同改）；版本标注升 v0.9.2 对齐商店包；新增 `.assetsignore` 部署排除清单（排除 `.git`/`.wrangler`/`.gitignore`/`docs`/`AGENTS.md`/`README.md`），修复构建时仓库元数据被 Workers 静态资源误上传的问题 |
| v0.9.2（同版修订） | 2026-09-28 | 排除清单补充构建期生成物与 Node 工具链文件（`wrangler.jsonc`/`wrangler.toml`/`.dev.vars`/`package.json`/`package-lock.json`/`node_modules`）：修复构建期自动生成的 `wrangler.jsonc` 被公开服务的问题（线上 `/wrangler.jsonc` 原返回 200，暴露 Worker 名与 assets 配置） |
