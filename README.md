# houyidb.top 站点

> 静态站点（纯 HTML/CSS/JS），无构建步骤、无外部字体/图片/CDN。
> 独立公共仓：`houyidb-community/houyidb-site`。
> 部署方式：GitHub Pages，`main` 分支根目录（Deploy from a branch）。
> 自定义域名：仓库根目录 `CNAME` = `houyidb.top`。

## 1. 目录

```
.
├── index.html            中文首页
├── performance.html      中文性能页（仅 HouyiDB 自测数据）
├── docs.html             中文文档入口
├── en/                   对应英文页
├── styles.css            基础样式
├── pages.css             次级页面样式
├── app.js                移动端导航 / 复制按钮 / 目录高亮
├── assets/               logo 与 favicon
├── CNAME                 houyidb.top
└── README.md             本文件
```

本地预览：

```bash
python3 -m http.server 8000
# 打开 http://127.0.0.1:8000/
```

## 2. GitHub Pages 部署

1. 仓库 `houyidb-community/houyidb-site`，默认分支 `main`。
2. **Settings → Pages → Build and deployment → Source** 选择
   **Deploy from a branch**，分支 `main`，目录 `/ (root)`。
3. 推送 `main` 后等待 Pages 构建完成。
4. 在 Pages 设置中确认自定义域名为 `houyidb.top`（`CNAME` 文件会自动填入）。
5. DNS 校验通过、证书签发后，勾选 **Enforce HTTPS**。

## 3. DNS 配置（阿里云）

| 类型 | 主机记录 | 记录值 |
|------|----------|--------|
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| AAAA | `@` | `2606:50c0:8000::153` |
| AAAA | `@` | `2606:50c0:8001::153` |
| AAAA | `@` | `2606:50c0:8002::153` |
| AAAA | `@` | `2606:50c0:8003::153` |
| CNAME | `www` | `houyidb-community.github.io` |

要点：

- **apex 不要用 CNAME**；A/AAAA 与 CNAME 不要在同一主机记录混用。
- 先删除指向旧主机的冲突记录，TTL 建议 300–3600 秒。
- 证书签发最长可能需要 24 小时；期间可先用 `http://` 或 GitHub 默认域名。
- 验证：

```bash
dig +short houyidb.top A
dig +short houyidb.top AAAA
dig +short www.houyidb.top CNAME
curl -I https://houyidb.top/
```

## 4. 内容约定

- 性能页数字只来自 HouyiDB 自身实测报告；不加入外部系统数据、不写跨场景
  总分、不写对比性排名结论。
- 中文页与 `en/` 英文页保持同构，新增章节同时补齐两种语言。
- 不引入外部字体、图片、脚本或 CDN；图标一律内联 SVG。
- 文档入口指向主仓 `houyidb-community/houyidb` 的 `main` 分支。
