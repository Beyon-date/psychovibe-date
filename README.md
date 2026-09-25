# 你的身体，正在替你说那些说不出口的话

> 高一16班 研究性学习课题 · 心理学方向 · 课题代号「心身反应」

一个纯静态的校园课题展示网站：用段子和口语讲心理学，末尾挂一份匿名问卷收集研究数据。

---

## 目录结构

```
.
├── index.html              # 整个网站（HTML + CSS 内联，单文件）
├── README.md               # 本文件
└── assets/                 # 全部图片（7 张，文件名 = 角色名）
    ├── README.md           # ★ 图片对照清单（每张图是什么角色、用在哪）
    ├── 初音未来-首屏.png    # 初音未来 —— 首屏主视觉
    ├── 派蒙.png            # 派蒙 —— 第 1 节
    ├── 艾米莉亚.webp        # 艾米莉亚 —— 第 2 节
    ├── 洛天依.png           # 洛天依 —— 第 3 节
    ├── 波奇.png            # 后藤一里（波奇）—— 第 4 节
    ├── 洛琪希.png           # 洛琪希 —— 第 5 节
    └── 初音未来-第六节.png   # 初音未来 —— 第 6 节
```

**图片对应关系详见 [`assets/README.md`](assets/README.md)**

---

## 技术说明

- **零依赖**：没有框架、没有构建步骤、没有 npm、没有 CDN
- HTML 和 CSS 全部内联在 `index.html`（约 25 KB）
- 装饰元素（像素方块、斜纹分隔带、跑马灯）全部是 CSS/SVG 手写，**不占用图片**
- 页面**唯一的外部请求**是问卷链接 `wj.qq.com`
- 断网状态下除问卷外，网页可以完整正常显示

---

## 本地预览

直接双击 `index.html` 用浏览器打开即可（图片用相对路径，不会裂图）。

或者起一个本地服务：

```bash
python3 -m http.server 8000
# 然后访问 http://localhost:8000
```

---

## 部署到 GitHub + Vercel

### 第一步：上传到 GitHub

1. 在 GitHub 新建一个仓库（Public 或 Private 都行），**不要**勾选 "Add a README file"
2. 在本地项目目录执行：

```bash
git init
git add .
git commit -m "高一16班心理课题网站"
git branch -M main
git remote add origin https://github.com/你的用户名/仓库名.git
git push -u origin main
```

> 如果是在手机 / 网页端操作：GitHub 仓库页面 → `Add file` → `Upload files` → 把 `index.html` 和 `assets` 文件夹一起拖进去 → Commit。
> ⚠️ **`assets` 文件夹要整个上传**，不能只传 `index.html`，否则图片全部裂掉。

### 第二步：部署到 Vercel

1. 打开 [vercel.com](https://vercel.com)，用 GitHub 账号登录
2. 点 **Add New → Project**，选中刚才那个仓库，点 **Import**
3. 配置项保持默认即可（这是纯静态站，Vercel 会自动识别）：

   | 配置项 | 填什么 |
   |---|---|
   | Framework Preset | `Other`（或保持自动识别） |
   | Root Directory | `./` |
   | Build Command | **留空** |
   | Output Directory | **留空** |
   | Install Command | **留空** |

4. 点 **Deploy**，等十几秒，会得到一个 `xxx.vercel.app` 的网址

> 之后每次往 GitHub 推送新提交，Vercel 都会自动重新部署，不用手动操作。

### 可能踩的坑

| 现象 | 原因 | 解决 |
|---|---|---|
| 图片全部裂开 | `assets` 文件夹没上传，或传成了 `Assets`（大写） | Vercel 是 Linux，**区分大小写**，文件夹名必须是 `assets` |
| 图片部分裂开 | HTML 里的文件名和实际文件名大小写不一致 | 全部改成小写（本项目已统一为小写文件名） |
| 打开是 404 | 入口文件不叫 `index.html` | 根目录必须有 `index.html` |
| 样式全丢 | 上传时漏了文件 | 确认 `index.html` 是完整的单文件（CSS 在里面） |

---

## 日常维护

### 换问卷链接

打开 `index.html`，搜索 `wj.qq.com`，替换 `href` 里的地址即可：

```html
<a class="qbtn" href="https://wj.qq.com/s2/你的问卷ID/" target="_blank" rel="noopener">填写问卷 →</a>
```

### 改配色

所有颜色集中在 `index.html` 顶部的 `:root` 里，改一处就全局生效：

```css
:root{
  --mustard:#F6C51C;   /* 芥末黄 —— 首屏、第1/4节 */
  --orange:#F2762E;    /* 暖橘   —— 第5节 */
  --sky:#7FC8E8;       /* 天蓝   —— 第6节、问卷区 */
  --mint:#9FDCA8;      /* 浅绿   —— 第3节 */
  --lav:#C9A8E0;       /* 淡紫   —— 第2节（配艾米莉亚） */
  --ink:#1E1B18;       /* 墨黑 —— 描边、文字块 */
  --paper:#FFFDF5;     /* 奶白 —— 正文卡片底 */
  --red:#E23E2B;       /* 波普红 —— 强调色 */
}
```

各板块用 `class="sec"` / `sec orange` / `sec blue` / `sec mint` / `sec lav` / `sec paper` 控制。

### 换角色图

见 [`assets/README.md`](assets/README.md) 最后一节。

---

## 免责声明

本网站内容仅用于**校园研究性学习与心理学科普**，不能替代专业心理评估、诊断或治疗。

页面中的 Q 版角色插画来自网络公开图源，版权归原作者及权利方所有；本站为非商业的校园课题展示，如权利人认为使用不妥，请联系我们删除。
