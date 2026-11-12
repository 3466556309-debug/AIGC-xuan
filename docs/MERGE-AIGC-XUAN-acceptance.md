# AIGC-xuan 合并发布验收

- 验收时间：2026-11-12 20:43（Asia/Shanghai）
- 执行方：云端 dsh
- 验收结论：**通过**

## 1. 仓库与 Pages

- 仓库地址：https://github.com/3466556309-debug/AIGC-xuan
- 可见性：**Public（公开）**
- 默认分支：`main`
- Pages 发布分支：`gh-pages`，路径 `/`（仓库根目录）
- Pages 构建方式：`legacy`，已强制 HTTPS
- 仓库根目录入口页：https://3466556309-debug.github.io/AIGC-xuan/

两个新地址：

- 言语词库：https://3466556309-debug.github.io/AIGC-xuan/yanyu-cishu/
- 公考错题本：https://3466556309-debug.github.io/AIGC-xuan/gongkao-cuoti/

两个原地址（本轮验收后仍可打开）：

- https://3466556309-debug.github.io/yanyu-cishu/
- https://3466556309-debug.github.io/gongkao-cuoti/

## 2. 公网检查结果

### 2.1 首页

| 地址 | HTTP | 内容类型 | 页面标题 |
| --- | --- | --- | --- |
| `https://3466556309-debug.github.io/AIGC-xuan/` | 200 | `text/html; charset=utf-8` | AIGC-xuan · 两个网页工具 |
| `https://3466556309-debug.github.io/AIGC-xuan/yanyu-cishu/` | 200 | `text/html; charset=utf-8` | 言语词库 · 成语与实词 |
| `https://3466556309-debug.github.io/AIGC-xuan/gongkao-cuoti/` | 200 | `text/html; charset=utf-8` | 公考错题本 · 事业单位 D 类 |

### 2.2 关键资源

全部返回 200，内容类型正确：

| 资源 | HTTP | 内容类型 | 字节数 |
| --- | --- | --- | --- |
| `yanyu-cishu/js/app.js` | 200 | `application/javascript` | 54,797 |
| `yanyu-cishu/css/app.css` | 200 | `text/css` | 56,946 |
| `yanyu-cishu/sw.js` | 200 | `application/javascript` | 2,840 |
| `yanyu-cishu/manifest.webmanifest` | 200 | `application/manifest+json` | 634 |
| `yanyu-cishu/shared/seed.mjs` | 200 | `text/javascript` | 23,786 |
| `yanyu-cishu/vendor/pdfjs/pdf.min.mjs` | 200 | `text/javascript` | 352,645 |
| `yanyu-cishu/vendor/xlsx/xlsx.mjs` | 200 | `text/javascript` | 896,114 |
| `gongkao-cuoti/js/app.js` | 200 | `application/javascript` | 97,455 |
| `gongkao-cuoti/css/app.css` | 200 | `text/css` | 39,219 |
| `gongkao-cuoti/sw.js` | 200 | `application/javascript` | 1,810 |
| `gongkao-cuoti/manifest.webmanifest` | 200 | `application/manifest+json` | 924 |
| `gongkao-cuoti/js/db.js` | 200 | `application/javascript` | 10,216 |

补充检查：

- 按两个 Service Worker 的 `APP_SHELL` 逐项请求：言语词库 32/32 返回 200，公考错题本 12/12 返回 200，失败 0。
- 线上 `sw.js` 已确认使用新缓存名 `yanyu-cishu-aigc-xuan-20261112`、`gkc-aigc-xuan-20261112`。
- 两个 manifest 的 `start_url`、`scope` 均为相对路径（`scope` 都是 `./`；`start_url` 分别是 `./` 和 `./#/home`）。
- 抽取 8 个关键文件（两个首页、两个 `sw.js`、两个 `app.js`、`seed.mjs`、`app.css`）做 SHA-256 对比：本地副本与公网实际返回**完全一致**。
- 两个站点的 HTML/CSS/JS 中没有根路径 `/...` 资源引用；页面入口、模块导入、图标、manifest 和 Service Worker 均使用相对路径。

> 本轮验证以公网 HTTP、静态资源完整性、Service Worker 外壳清单和 JS 语法解析为主；没有在真实浏览器中逐项点击业务流程。两个站点的运行时代码沿用此前已上线的版本，只改了副本中的 Service Worker 缓存名。

## 3. 原仓库与原网址核对

| 项目 | 结果 |
| --- | --- |
| `yanyu-cishu` 仓库 | 仍在，公开，未归档；默认分支 `master` |
| `yanyu-cishu` 远程分支 | `master = 19dddb479734bd05eec4b2e1a1ef924c51ac8930`；`gh-pages = 0b61f336e7a0e23ffad36c2e5ed2cf4f61b871c7`（与操作前一致） |
| `yanyu-cishu` 原网址 | `https://3466556309-debug.github.io/yanyu-cishu/` 返回 200 |
| `gongkao-cuoti` 仓库 | 仍在，公开，未归档；默认分支 `main` |
| `gongkao-cuoti` 远程分支 | `main = 286a6d6596146801fd7ece588e36e4ce37cb42a6`（与操作前一致） |
| `gongkao-cuoti` 原网址 | `https://3466556309-debug.github.io/gongkao-cuoti/` 返回 200 |

未对原仓库执行 `git add`、`git commit`、`git push`、改远程、删除分支、改名、归档或 force-push。原仓库的 `pushedAt` 保持操作前时间（言语词库 2026-11-11，公考错题本 2026-11-10）。

## 4. 敏感数据与用户文件核对

- `main` 代码提交（不含本文档）共 245 个文件；加入本文档后为 246 个。`gh-pages` 发布分支共 244 个文件，总大小约 13.4 MB。
- 对两个分支的文件名扫描：没有 `app-data.json`、`.tmp-user-pdf/`、`.env`、`.pdf`、`wrangler` 登录态、token、私钥、备份目录或 `node_modules`。
- 对文本内容扫描：没有 GitHub token、API key、私钥、Cloudflare token 等密钥特征。
- 公网抽查以下路径均为 404，确认没有上传：
  - `/AIGC-xuan/yanyu-cishu/data/app-data.json`
  - `/AIGC-xuan/yanyu-cishu/.tmp-user-pdf/`
  - `main` 分支的 `data/app-data.json`
  - `main` 分支的 `.env`
- 言语词库只复制了 `pages-dist/` 静态产物（页面、JS、CSS、图标、vendor、manifest、SW），没有复制 `server/`、`worker/`、`migrations/`、`data/`、`.tmp-user-pdf/` 或任何用户 PDF。
- 公考错题本只复制静态网页文件（HTML、CSS、JS、图标、manifest、SW），没有复制本机 `dsh-v1.jsonl` 会话记录或 `serve.py`。

## 5. 路径与副本改动

- 两个站点原本就使用 `./` 相对路径，放进 `/AIGC-xuan/<子目录>/` 后不需要改页面资源引用。
- 只在 AIGC-xuan 副本中做了部署适配：
  - 言语词库 SW 缓存名：`yanyu-cishu-v4-20261111-pdf` → `yanyu-cishu-aigc-xuan-20261112`
  - 公考错题本 SW 缓存名：`gkc-v1.0.1` → `gkc-aigc-xuan-20261112`
  - 加了两行部署位置注释。
- 没有把这些改动写回原来的两个仓库。

## 6. 提交号与 Pages 发布号

| 项目 | 值 |
| --- | --- |
| `main` 代码提交 | `311299505c042d6217dae424fa44c90901557e9a` |
| `gh-pages` 发布提交 | `336c57e01cc3d6441eb78495991f465036cd9cde` |
| Pages 构建 ID | `1363141029` |
| Pages 构建状态 | `built` |
| Pages 构建用时 | 23,160 ms |
| Pages 构建地址 | https://api.github.com/repos/3466556309-debug/AIGC-xuan/pages/builds/1363141029 |
| Pages 来源 | `gh-pages` 分支，路径 `/` |

本验收文档是 `main` 分支上的后续单独提交（提交后 `main` 为 246 个文件），只增加文档，不改 `gh-pages` 发布内容，因此不会触发 Pages 重新构建，上面记录的发布提交和构建号就是当前线上版本。

## 7. 费用与合规

- 使用公开仓库 + GitHub Pages 免费额度：**0 元**。
- 未绑卡、未买域名、未开通任何付费套餐。
- 未执行任何 Cloudflare / Wrangler 命令，未登录或修改 Cloudflare 站点。
- 未删除、改名、归档、清空、force-push 或关闭原仓库。
- 未修改原仓库代码，未向原仓库 push。
- 未占用 8080，未改文轩本机配置。

## 8. 可复核命令

```bash
# 新站点首页
curl -sS -o /dev/null -w '%{http_code}\n' -L https://3466556309-debug.github.io/AIGC-xuan/yanyu-cishu/
curl -sS -o /dev/null -w '%{http_code}\n' -L https://3466556309-debug.github.io/AIGC-xuan/gongkao-cuoti/

# 原站点首页
curl -sS -o /dev/null -w '%{http_code}\n' -L https://3466556309-debug.github.io/yanyu-cishu/
curl -sS -o /dev/null -w '%{http_code}\n' -L https://3466556309-debug.github.io/gongkao-cuoti/

# 原仓库远程分支（应与上面记录一致）
git ls-remote https://github.com/3466556309-debug/yanyu-cishu.git refs/heads/master refs/heads/gh-pages
git ls-remote https://github.com/3466556309-debug/gongkao-cuoti.git refs/heads/main

# Pages 构建状态
gh api repos/3466556309-debug/AIGC-xuan/pages/builds --jq '.[0] | {status, commit, duration, url}'
```
