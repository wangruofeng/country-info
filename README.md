# 国家信息速查

一个纯前端的单文件国家/地区信息查询工具，双击 `index.html` 即可使用，无需安装、无需后端、无任何外部依赖。

## 功能特性

- 🔍 **多维搜索**：中文名（含别名，如“漂亮国”“巴铁”）、英文名、两位/三位国家码（CN / CHN）、ISO 数字码（156）、货币码（USD）、货币中文名（人民币）、电话区号（+86 / 86）、顶级域（.cn）均可命中。
- 🗂️ **大洲分组**：亚洲、欧洲、北美洲、南美洲、非洲、大洋洲、南极洲七个分组浏览。
- 📋 **逐项复制**：详情面板展示 CCA2 / CCA3 / 数字码 / 顶级域 / 电话区号 / 官方名 / 首都 / 语言，每项均可一键复制。
- 💱 **货币信息**：货币代码、符号、中文名，附 `Intl.NumberFormat` 本地化格式示例（如 ¥1,234.56）。
- 🕐 **时区当前时间**：展示各国 IANA 时区及对应当前时间与 UTC 偏移，每 30 秒自动刷新。
- ⭐ **收藏 + 最近使用**：收藏与最近查看保存在本地（`localStorage country-info-favs` / `country-info-recent`，上限 24 个，去重前置）。
- 🌓 **深浅色主题**：一键切换，偏好保存在 `localStorage country-info-theme`。
- 📱 **响应式布局**：桌面端详情面板在右侧，移动端在底部。

## 使用方式

直接用浏览器打开 `index.html` 即可：

```bash
open index.html        # macOS
# 或拖入浏览器
```

搜索框输入任意关键词即可过滤；按 `/` 快速聚焦搜索框，`Esc` 清空搜索或关闭详情。

## 技术说明

- 单一 HTML 文件，原生 HTML / CSS / JavaScript，零依赖、零构建步骤。
- 数据内嵌为 JS 常量：国家信息来自 [mledoze/world-countries](https://github.com/mledoze/countries)（ODbL），时区映射来自 moment-timezone；共 250 个国家/地区。
- 所有解析与渲染均在浏览器本地完成，不上传任何数据。
- 动态渲染一律使用 `createElement` / `textContent`，避免 XSS 注入风险。
- 国旗使用系统 Emoji 字体渲染；Windows 桌面端不支持旗帜 Emoji，会显示为两位国家码字母（如 CN）。

## 在线访问

已通过 GitHub Pages 部署，可直接访问：

🔗 **https://blog.wangruofeng007.com/country-info/**

源码仓库：https://github.com/wangruofeng/country-info
