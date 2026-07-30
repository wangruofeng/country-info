# country-info — 项目约定（给 AI 协作时参考）

纯前端、单文件的国家/地区信息速查工具。面向人类的说明见 `README.md`；本文件记录**改代码时必须知道的红线与约定**。项目与同级目录 `../emoji-picker`、`../json-viewer`、`../xml-viewer` 保持同一套设计与代码风格。

## 红线（不要破坏）

- **单文件、零构建、零依赖**：全部 HTML / CSS / JS 都在 `index.html` 一个文件里。**禁止**引入打包器（Vite/Webpack 等）、框架（React/Vue 等）、npm 依赖或构建步骤。新增能力用原生 JS 实现。
- **纯前端、无后端**：所有数据与计算在浏览器本地完成，不上传任何数据。
- 主题用根元素 `html.dark` 类切换，配色全部走 `:root` / `html.dark` 里的 CSS 变量。新增颜色请复用已有变量，不要硬编码。
- **渲染用户输入一律 `createElement` / `textContent`**，禁止用 `innerHTML` 拼接用户可控或动态内容（XSS 红线）。页头主题按钮、星标、复制等静态 SVG 图标常量除外。

## 文件结构

- `index.html` — 全部代码（结构 + 样式 + 脚本），内置 `COUNTRY_DATA` 数据集。
- `favicon.svg` — 蓝紫渐变圆角方块 + 白色 `🌐`。
- `.github/workflows/deploy.yml` — GitHub Pages 部署：仓库根即站点根，push 到 `main` 自动部署。
- `README.md` — 面向用户的功能说明与在线访问地址。
- `CLAUDE.md` — 本文件，记录红线、约定与数据结构。

## UI 约定

- **按钮文案保持极简**：图标已承担表意，文字尽量短（如「复制」）。
- 页头右侧两个图标按钮：GitHub 源码链接（仓库 `https://github.com/wangruofeng/country-info`，新标签页打开）、深浅色主题切换。
- 搜索框、大洲 tab、国家卡片网格、详情面板按 emoji-picker 风格使用卡片、阴影、圆角。

## 数据结构与新增国家约定

内置数据集 `COUNTRY_DATA` 为对象数组（按 a2 排序），每个对象字段：

```js
{
  a2: 'CN',                    // ISO 3166-1 alpha-2
  a3: 'CHN',                   // ISO 3166-1 alpha-3
  n3: '156',                   // ISO 3166-1 数字码
  en: 'China',                 // 英文常用名
  off: '中华人民共和国',        // 中文官方名
  cn: '中国',                   // 中文常用名，卡片主显示
  flag: '🇨🇳',                 // 国旗 Emoji（Windows 显示为字母，属已知限制）
  reg: '亚洲',                  // 大洲，必须是下面 7 个之一
  cap: 'Beijing',              // 首都（英文名）
  tel: '+86',                  // 电话区号（多后缀国家只保留根，如美国 +1）
  tld: '.cn',                  // 顶级域（多个时取第一个）
  tz: ['Asia/Shanghai'],       // IANA 时区数组（最多 12 个）
  lang: 'Chinese',             // 语言，' / ' 分隔
  cur: [{ c: 'CNY', s: '¥', n: '人民币' }],  // 货币数组：代码/符号/中文名
  kw: ['中国', 'china', 'cn', 'chn', '+86', '86', 'cny', '人民币', '大陆']  // 搜索关键词
}
```

大洲固定为：`亚洲`、`欧洲`、`北美洲`、`南美洲`、`非洲`、`大洋洲`、`南极洲`（中美洲与加勒比归入 `北美洲`）。

### 修改条目时必须维护 kw 关键词

1. 包含中文常用名、别名（如美国的「美帝」「漂亮国」）。
2. 包含小写英文名、a2、a3、区号（带 + 和不带 + 两种）、货币码与货币中文名。
3. 不要放无意义填充；关键词应能真实提升搜索命中率。

### 数据再生成

数据由一次性脚本从 mledoze/world-countries + moment-timezone 裁剪生成（脚本未入库，见会话记录 `/tmp/country-data/gen.mjs`）。更新数据时重新拉取上游、运行脚本、替换 `index.html` 中的 `COUNTRY_DATA` 常量即可，不要把脚本或上游 JSON 提交进仓库。

## 在线地址

已部署到 GitHub Pages：https://blog.wangruofeng007.com/country-info/
