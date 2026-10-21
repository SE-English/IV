# 不规则动词表 · 点读版（GitHub Pages 静态托管）

一个**纯静态、可离线分享**的英语不规则动词表网页：点击任意单词即可发音、朗读时高亮当前词、支持手机浏览器、可新增单词，并内置「一键分享」与「导出鉴权」。

## 功能
- 🔊 **点读发音**：点原形/过去式/过去分词听英文，点释义听中文。优先用浏览器内置语音；微信/QQ 内置浏览器无内置语音时自动改用在线发音。
- 🟡 **朗读高亮**：单读、整行、朗读全部时，当前词黄色高亮并自动滚动到视野内。
- ➕ **新增/批量**：顶部「✚ 新增单词」可单条或批量添加，数据自动保存。
- 💾 **本地 SQLite 持久化**：编辑内容保存在浏览器内的 **SQLite WASM（sql.js）+ IndexedDB**；加载失败时自动回退 localStorage。无需服务器。
- 🔗 **一键分享**：把当前内容编码进链接（`#d=...`），复制发给同学，对方打开即载入其本地 SQLite。纯静态，无需后端。
- 🔐 **导出鉴权**：「📤 导出网页」需输入公钥+私钥（SHA-256 比对），连续错 3 次隐藏导出按钮。

## 本地预览
直接用浏览器打开 `index.html` 即可（点读需浏览器支持语音；SQLite 引擎在线时从 `vendor/sqljs/` 加载，离线则回退 localStorage）。

## 部署到 GitHub Pages（免费）
1. 在 GitHub 新建一个**公开**仓库（例如 `irregular-verbs`）。
2. 把本目录（含 `index.html`、`vendor/`、`README.md`、`.nojekyll`）推上去：
   ```bash
   git init
   git add .
   git commit -m "initial: irregular verbs point-read site"
   git branch -M main
   git remote add origin https://github.com/<你的用户名>/<仓库名>.git
   git push -u origin main
   ```
3. 仓库 **Settings → Pages → Build and deployment → Source** 选择 **Deploy from a branch**，分支选 **main**，目录选 **/ (root)**，保存。
4. 稍等一两分钟，访问 `https://<你的用户名>.github.io/<仓库名>/` 即可。

> 也可改用 GitHub Actions 部署：在仓库加 `.github/workflows/pages.yml`（上传根目录为 Pages artifact）。二选一即可，不要同时启用两种来源。

## 说明
- GitHub Pages 是**纯静态**托管，没有服务器端数据库。所谓「保存到 SQLite WASM」是在**每个访客自己的浏览器**里落库；「一键分享」通过把数据编入链接实现跨设备传递，因此无需任何后端或密钥。
- 导出鉴权为前端校验，仅防误用；真正权限控制需后端，本静态站点不含后端。
