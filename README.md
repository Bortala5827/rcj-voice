# rcj-voice · 声音定制站（voice.955827.xyz）

面向海外华语用户的声音定制 / 歌曲演唱展示站。深夜暖调 UI、三语（中/繁/EN）、试听卡片流。

## 文件

- `index.html` — 单文件页面（自包含 CSS/JS，三语切换、卡片流、实时成交条、试听播放）
- `products.json` — 歌曲数据（标题/标签/点评三语 + 价格 + 试听 URL + 封面渐变）。**M1 收购后改这里即可，无需动代码**

## 数据说明

- 页面加载时 `fetch('products.json')`，成功用线上数据；本地 `file://` 打开时 fetch 被浏览器拒绝，自动回退到 JS 内置的示例数据（fallback）
- 每首歌 `preview` 字段：填 R2 试听直链（如 `/previews/v001.mp3`）后自动真实播放；为 `null` 时显示模拟试听
- `grad` 字段：封面渐变色（两色），换封面图时可改

## 部署（CF Pages + R2）

1. **GitHub 仓库**：新建 `rcj-voice`，push `index.html` + `products.json`
2. **CF Pages**：控制台新建 Pages 项目，连接该仓库（生产分支 main），构建命令留空（纯静态）
3. **域名**：Pages 项目 → Custom domains → 添加 `voice.955827.xyz`（CF 自动加 DNS 记录）
4. **R2 试听音频**：
   - R2 桶 → 绑定自定义域名：`voice.955827.xyz` 子路径（如 `/previews`）
   - 或直接在 Pages 同域放 `previews/` 目录（静态资源走 Pages 即可，更简单）
   - 试听命名：`previews/v001.mp3`、`covers/v001.png`（可选）
5. **替换数据**：M1 收购后改 `products.json` 的 `songs`（真实歌名/点评/价格 + `preview` 指向 R2 片段），push 自动更新

## 上线后

- 主站 955827.xyz 产品矩阵「服务与变现」组加 voice 卡（第 10 卡）+ i18n 字典
- 社媒导流：TikTok/Shorts 发 15-30s 试听，bio 挂 voice 链接
- 成交：卡片「购买」按钮外链咸鱼店铺（MVP）；后期 PayPal live 自收款 + 邮件交付
