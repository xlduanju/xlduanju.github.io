# 小蓝短剧 防丢失发布页

纯静态「官方发布页」：用户收藏这一个网址，主站域名变了也能在这里找到最新地址。
只放网站地址，不放安装包。

## 换最新地址：改 domains.json

`domains.json` 里的 `latest` 就是页面上的「官方地址」。域名变了：
打开 `domains.json`，点铅笔（Edit），改 `latest` 里的网址和 `updated` 日期，
点绿色 **Commit changes**，1~2 分钟后页面生效。

```json
{
  "latest": ["https://新域名.com"],
  "updated": "2026-11-06",
  "by": "manual"
}
```

以后要是想接域名机器人自动改，参考 xiaolan-nav-page 仓库里的 `vps-hook/`，
机器人改的也是这个文件，页面不用动。

## 导航站 / 注意事项：改 index.html 顶部 CONFIG

1. 打开 `index.html`，点铅笔（Edit）
2. 找到文件开头 `CONFIG`：
   - `permanentDomains`：导航站等长期有效地址，一行一个，行尾保留逗号
   - `telegram`：频道 / 群链接（现在是空的，有了就加）
   - `contactEmail`：自动回复邮箱（现在是空的）
   - `notices`：注意事项，一行一条
   - `latestDomains`：官方地址的兜底，只有 `domains.json` 读不到时才用
3. 顺手把 `updated` 改成当天日期，点 **Commit changes**

## 注意

- 短剧主站**没有泛解析**，`randomSubdomains` 保持 0（原样显示，不随机二级域名）
- 「可用性检测」靠加载站点上一张真实存在的小图：默认 `/favicon.ico`（xiaolanduanju.com 有）；
  xiaolanduanju.cn 和 xiaolandaohang.com 没有这张图，已在 `probePathByHost` 里按域名
  分别指定 `/logo.webp` 和 `/logo_sm.webp`。以后换域名如果检测一直「未必正常」，
  就是新站上没有这张图，去 `probePathByHost` 里给它指定一张真实存在的小图
- 只改 `CONFIG` 那一段和 `domains.json`，页面其他部分不用动
- 网址建议带 `https://`（漏写了页面也会自动补上）
- `og.png` 是分享卡片图（1200×630），源文件在 `og-src/og.html`，改完用 Chrome 无头重新截一张
- 统计用的是导航站同一个 GA4（G-YQ0XFMTFHJ），在 GA 里按主机名 xldjw.github.io 过滤看本页数据；
  以后想单独建一个属性，改 CONFIG 里的 `gaMeasurementId` 即可
- SEO：`<title>`、canonical、`robots.txt`、`sitemap.xml`、页面底部「关于」那段写死的文字都在仓库里；
  Search Console / Yandex 站长验证的 meta 标签以后加在 index.html 头部
