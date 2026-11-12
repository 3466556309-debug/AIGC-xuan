# AIGC-xuan

这是两个互相独立的网页工具的代码合集。它们放在同一个公开仓库里，用同一个 GitHub Pages 站点免费发布，方便一起打开、一起备份。

| 工具 | 新网址（GitHub Pages） | 原网址（仍然可用） |
| --- | --- | --- |
| 言语词库（成语与实词） | https://3466556309-debug.github.io/AIGC-xuan/yanyu-cishu/ | https://3466556309-debug.github.io/yanyu-cishu/ |
| 公考错题本（事业单位 D 类） | https://3466556309-debug.github.io/AIGC-xuan/gongkao-cuoti/ | https://3466556309-debug.github.io/gongkao-cuoti/ |

两个工具仍然是各自独立的：不共用账号，不共用数据，也不互相依赖。原仓库 `yanyu-cishu`、`gongkao-cuoti` 没有被删除、改名、归档或 force-push，原网址继续可用。

## 数据放在哪里

- 言语词库：词库和学习进度保存在每个人自己浏览器的 IndexedDB 里，不上传服务器。
- 公考错题本：错题、导图、附件和设置保存在本机浏览器的 IndexedDB 里，不上传服务器。
- 换设备或清理浏览器数据前，请先在各自工具的“设置”里导出备份。

## 目录

```text
AIGC-xuan/
  README.md
  index.html                          # Pages 根目录的简单入口页
  docs/MERGE-AIGC-XUAN-acceptance.md  # 本次合并发布的验收记录
  yanyu-cishu/                        # 言语词库静态网页版（可直接发布）
  gongkao-cuoti/                      # 公考错题本静态网页版（可直接发布）
```

## 这个副本改了什么

只改了 `AIGC-xuan` 副本里的部署适配内容：

- 两个站点原本就使用 `./` 相对路径，因此放进 `/AIGC-xuan/` 子目录后不需要改资源引用。
- 两边 Service Worker 的缓存名改成独立的新名字（`yanyu-cishu-aigc-xuan-20261112`、`gkc-aigc-xuan-20261112`），避免和原站同源缓存混用。
- 没有把任何路径改动写回原仓库。

## 发布方式

- 仓库：公开，`main` 分支保存完整合集与文档。
- Pages：独立 `gh-pages` 分支，根目录同时放 `yanyu-cishu/` 和 `gongkao-cuoti/` 两个子目录。
- 全部使用 GitHub Pages 免费额度：0 元、未绑卡、未买域名、未改 Cloudflare。

## 没有上传的东西

仓库和 Pages 发布包中不包含：`.tmp-user-pdf/`、用户 PDF（如「高频800词记忆版（绿色底图）.pdf」、花生十三讲义）、`data/app-data.json`、`.env`、Cloudflare/Wrangler 登录态或任何密钥。
