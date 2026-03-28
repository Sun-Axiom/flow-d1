这是一份为你量身定制的 **README.md**。它采用了你偏好的 **“ins 风格” (极简且美观)** 布局，并详细记录了前端与后端的部署流程。

你可以直接将以下内容保存为项目根目录下的 `README.md`。

---

# 📦 Project Flow Manager (V1.0.42)

一个基于 **Cloudflare Workers + D1 Database** 构建的极简主义项目流管理系统。支持自定义工作流、实时进度跟踪、项目归档以及物理删除功能。

![Version](https://img.shields.io/badge/Version-1.0.42-blue?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)
![Platform](https://img.shields.io/badge/Platform-Cloudflare-orange?style=flat-square)

## ✨ 特性
- **Ins Style UI**: 极简视觉设计，支持深色/浅色模式切换。
- **自定义流程**: 自由创建分类与步骤，适配不同业务场景。
- **动态归档**: 完善的归档库管理，支持按年份、流程、关键词多维筛选。
- **物理删除**: 彻底清理数据库冗余，保持系统轻量。
- **单位/金额管理**: 在极简布局中集成核心业务信息。

---

## 🚀 部署教程

### 1. 后端部署 (Cloudflare Worker)

后端负责处理 API 请求并操作 D1 数据库。

1. **创建 D1 数据库**:
   - 登录 Cloudflare 控制台，进入 `Workers & Pages` -> `D1`。
   - 创建一个新数据库，命名为 `flow-db`。
   - 在控制台的 **SQL 控制台** 执行以下初始化命令：
     ```sql
     CREATE TABLE projects (id TEXT PRIMARY KEY, n TEXT, tpl TEXT, un TEXT, am REAL, s INTEGER, memo TEXT, isPinned INTEGER, isArchived INTEGER, logs TEXT, createdAt INTEGER, archivedAt INTEGER);
     CREATE TABLE templates (id TEXT PRIMARY KEY, name TEXT, cat TEXT, steps TEXT);
     ```

2. **部署 Worker 代码**:
   - 创建一个新的 Worker，将 `worker.js` (即我们调试好的修复版) 代码粘贴进去。
   - 在 Worker 设置中，点击 **Settings** -> **Bindings** -> **Add Binding**。
   - 选择 **D1 database**，变量名填入 `DB`，并关联你刚才创建的 `flow-db`。

3. **获取 API 地址**:
   - 部署后，你会得到一个类似 `https://api-flow.yourname.workers.dev` 的地址。

### 2. 前端部署 (GitHub Pages)

前端是一个纯静态的 HTML 文件。

1. **修改 API 配置**:
   - 打开 `index.html`，将代码顶部的 `const API_URL = "..."` 修改为你刚才获取的 Worker 地址。

2. **上传至 GitHub**:
   - 将 `index.html` 推送到你的 GitHub 仓库（例如 `work-flow`）。

3. **开启 Pages**:
   - 在仓库设置中开启 GitHub Pages，选择 `main` 分支作为部署源。
   - (可选) 配置你的自定义域名，如 `flows.roll.ccwu.cc`。

---

## 🛠️ 技术栈
- **Frontend**: Vanilla JavaScript, CSS3 (CSS Variables), HTML5.
- **Backend**: Cloudflare Workers (Runtime).
- **Storage**: Cloudflare D1 (SQLite).
- **Icons**: Emoji based (Zero assets dependency).

## 📅 版本更新日志
### V1.0.42 (Current)
- **修复**: 解决了归档项目无法物理删除导致的 500/404 错误。
- **优化**: 归档库筛选栏布局调整，搜索框支持响应式填充。
- **新增**: 在归档卡片中显式标注“单位名称”。

---

## 📄 开源协议
本项目采用 [MIT](LICENSE) 协议开源。

---

> **Would you like me to ...**
> 帮你把这个 README 的内容直接推送到你的 GitHub 仓库中，还是你需要我再补充一些关于 D1 数据库自动备份的建议？
