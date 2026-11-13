# legal — 法务静态页（GitHub Pages）

本仓同时是**源文件仓**和**发布仓**：`main` 分支即 GitHub Pages 的发布源，
推上去即生效，不需要单独的构建步骤。

## 目录约定

**一项目一子目录**，子目录名 = 项目名（与 `Projects/` 下的工程目录对应）：

| 子目录 | 对应项目 | 线上地址 |
|---|---|---|
| `renovation/` | 装修预算（`Projects/renovation`，iOS App「装修预算」） | `https://mrkuosir.github.io/legal/renovation/privacy.html` / `terms.html` |

`renovation/privacy.html`（隐私政策）与 `renovation/terms.html`（用户协议）是
**线上法务页的唯一真源**——2026-11-13 起从装修仓 `worker/legal/` 迁到本仓，
装修仓不再保留副本。

## 改文案 / 改样式

1. 直接改 `renovation/*.html`；
2. `git commit` + `git push origin main`（Pages 自动重新发布，通常 1 分钟内生效）；
3. 装修仓 `./scripts/release-check.sh` 第 5 步会抓线上页面比对关键句（如「不发照片原图」），
   发布后应转绿。

页面必须**自包含**（无外部 CSS/JS/字体依赖），并保持 `prefers-color-scheme` 两套色值
（Light 底 `#F2ECE4` / Dark 底 `#1C1916`，文字/次文/分隔线对齐 App token），
否则在 App 内用 SFSafariViewController 打开时会从暖底"猛跳"到白/黑。
判据与背景见装修仓 `docs/ios/architecture/THEME_ARCHITECTURE.md`。

## 边界

- 本仓不放 API 密钥、后端代码或任何需要鉴权才可见的内容——Pages 是公开静态托管。
- 新增项目页面时：建子目录 → 放自包含 HTML → 在装修仓对应 App 里改 `AppConstants.legalBaseURL`
  （或同族常量）指向新路径，并在装修仓 `docs/ios/development/WORKER_DEPLOY.md` 登记。
