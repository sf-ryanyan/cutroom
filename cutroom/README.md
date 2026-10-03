# CUTROOM — 视频剪辑服务官网（单页 Landing Page）

一个纯静态单页网站，不需要任何框架、不需要编译、不需要服务器。
直接传到 GitHub Pages 就能上线。

---

## 一、文件说明

```
cutroom-site/
├── index.html          ← 整个网站都在这一个文件里（HTML + CSS + JS）
├── README.md           ← 本说明
├── .nojekyll           ← 必须保留，让 GitHub Pages 正常加载文件
├── CNAME.example       ← 绑定自己域名时用（改名为 CNAME）
└── assets/
    ├── images/         ← 放缩略图、首屏封面图、og 分享图
    └── videos/         ← 放首屏背景视频（可选）
```

---

## 二、上线步骤（GitHub Pages）

1. 在 GitHub 新建一个仓库，比如 `cutroom-site`，设为 **Public**
2. 把本文件夹里的所有文件上传到仓库根目录
   （网页操作：仓库页面 → Add file → Upload files → 拖进去 → Commit）
3. 进入仓库 **Settings → Pages**
4. Source 选 **Deploy from a branch**，Branch 选 **main**，文件夹选 **/ (root)**，点 Save
5. 等 1–2 分钟，页面地址是：
   `https://你的用户名.github.io/cutroom-site/`

### 绑定自己的域名（可选）

1. 把 `CNAME.example` 改名为 `CNAME`，里面写你的域名（如 `cutroom.com`）
2. 在域名服务商处添加 DNS 记录：
   - 根域名（cutroom.com）→ 加 4 条 A 记录，指向
     `185.199.108.153` / `185.199.109.153` / `185.199.110.153` / `185.199.111.153`
   - www 子域名 → 加 1 条 CNAME 记录，指向 `你的用户名.github.io`
3. 回到 Settings → Pages，填入域名，勾选 **Enforce HTTPS**

---

## 三、上线前必须改的 4 处

全部在 `index.html` 里，用编辑器搜索就能找到。

### 1. 品牌名

搜索 `CUTROOM`，全部替换成你的品牌名。
注意有两种写法：

- 导航和页脚的 logo：`CUT<span>ROOM</span>`（前半白色，后半橙色，自己拆分）
- `<title>` 和 `og:title` 里的 `Cutroom`

### 2. 联系方式（已填好，换人时改这里）

当前已统一为：

| 项目 | 内容 |
|---|---|
| 姓名 | Ryan Yan |
| 电话 | 415-968-9115 |
| 邮箱 | sfryanyan@gmail.com |

出现位置：询价区的联系卡片、页脚、表单出错时的提示。
搜索 `sfryanyan@gmail.com`（5 处）和 `415-968-9115`（3 处）即可全部替换。
注意电话有两种写法：显示用 `415-968-9115`，链接用 `tel:+14159689115`。

### 3. 表单接收地址

打开 index.html，找到 `<script>` 里最上面这一行：

```js
var FORM_ENDPOINT = "";
```

去 https://formspree.io 免费注册 → 新建一个 form → 拿到类似
`https://formspree.io/f/abcdwxyz` 的地址 → 填进引号里：

```js
var FORM_ENDPOINT = "https://formspree.io/f/abcdwxyz";
```

填好之后，访客提交的询价会直接发到你注册的邮箱。
留空的话表单只是演示，不会真的发出去。

### 4. 作品集（样片）

同样在 `<script>` 最上面，找到 `var WORK = [...]`。
每一条有 5 个字段：

```js
{cat:"short", title:"标题", meta:"0:28 · 9:16", vertical:true, thumb:"", embed:""},
```

| 字段 | 填什么 |
|---|---|
| `cat` | 分类：`short` / `promo` / `long` / `clip` |
| `title` | 作品名，显示在缩略图下方 |
| `meta` | 时长和尺寸，如 `0:28 · 9:16` |
| `vertical` | 竖版填 `true`，横版填 `false` |
| `thumb` | 缩略图路径，如 `assets/images/work-01.jpg` |
| `embed` | 视频嵌入地址（见下） |

**视频嵌入地址怎么拿：**

- YouTube：视频 ID 是 `watch?v=` 后面那串
  → 填 `https://www.youtube.com/embed/视频ID`
- Vimeo：视频 ID 是地址最后那串数字
  → 填 `https://player.vimeo.com/video/视频ID`

**现在 12 张缩略图已经填好了**，用的是 `assets/images/work-01.jpg` ~ `work-12.jpg`，
这些是程序生成的电影感抽象画面（原创，无版权问题），当模板展示用。
真样片做好后，把图片换成真缩略图、把 `embed` 填上视频地址即可。

只要任意一条的 `embed` 填了内容，作品集下方的提示框会自动消失。

---

## 四、图片说明

`assets/images/` 里的图都是程序生成的原创素材，可直接商用，也可以随时替换：

| 文件 | 用途 | 尺寸 |
|---|---|---|
| `work-01` ~ `work-12.jpg` | 作品集缩略图（01-03、10-12 竖版，04-09 横版） | 540×960 / 960×540 |
| `reel-1` ~ `reel-6.jpg` | 首屏样片带 | 420×525 |
| `hero-poster.jpg` | 首屏背景静图 | 1600×900 |
| `og-cover.jpg` | 社交分享缩略图 | 1200×630 |

### 想把首屏换成会动的背景视频

1. 准备一条 15 秒左右、无声、快节奏的片子，命名 `showreel.mp4`，放进 `assets/videos/`
2. 在 index.html 里搜索 `想换成会动的背景`，按注释里的说明操作

建议视频压到 5MB 以内，否则手机打开会很慢。

---

## 五、改价格

搜索 `$59`、`$89`、`$149`、`$179`、`$229`、`$299` 直接改数字。
加购在 `<div class="addons">` 那一块。

---

## 六、改配色

打开 index.html，最上面 `<style>` 里的 `:root` 那一段：

```css
--bg:#0C0E11;      /* 页面背景（深黑） */
--surface:#15181D; /* 卡片背景 */
--line:#262C35;    /* 分割线和边框 */
--fg:#EDEEF1;      /* 正文文字（白） */
--muted:#8A919D;   /* 次要文字（灰） */
--warm:#F26B3A;    /* 主强调色（橙），按钮用 */
--cool:#45A8A2;    /* 副强调色（青），小标签用 */
```

改这 7 个值，全站颜色跟着变，不用逐个找。

---

## 七、技术说明（给设计/技术人员）

- 纯静态 HTML + CSS + 原生 JS，无框架、无构建步骤、无依赖
- 字体：Google Fonts（Archivo + IBM Plex Mono）
- 深色单主题，已设置 `color-scheme: dark`
- 响应式断点：860px（平板）/ 620px / 520px / 420px（手机）
- 作品集分类筛选、弹窗播放、表单校验均为原生 JS，约 150 行
- 已做：安全区适配（iPhone 刘海）、键盘焦点可见、`prefers-reduced-motion` 降级
- 待办：如需多语言、博客或 CMS，建议迁到 Astro 或 Framer

页面结构（从上到下）：

1. 固定导航
2. 首屏 Hero（标题 + 双按钮 + 交付规格 + 样片带）
3. 服务概览（4 项）
4. 作品集（4 个分类标签 + 12 个作品位）
5. 价格（短片 3 档 + 中长片 3 档 + 4 个加购）
6. 流程（3 步）
7. 为什么选我们（4 条）
8. 询价表单（5 个字段）
9. 页脚
