# 项目流管理器
> **V1.3.12** | 极简主义风格的项目进度管理利器。

基于 **Cloudflare Workers + D1 + Pages** 构建的轻量级项目追踪系统。支持多级流程自定义、可视化进度条、数据归档及物理删除，并集成 `X-Auth-Token` 身份验证保障数据安全。

### ✨ 功能亮点
* **🎨 Ins Style UI**: 极简设计，支持原生深色模式，响应式适配移动端。
* **🔒 身份验证**: 增强型安全机制，通过环境变量 `AUTH_KEY` 实现 API 访问控制。
* **📊 灵活流程**: 支持自定义分类与流程模板，步骤进度实时同步。
* **📂 归档系统**: 支持项目一键归档/恢复，归档库支持年份、模板筛选及关键词搜索。
* **🗑️ 物理删除**: 彻底清理无用项目，保持数据库整洁。
* **⚡ 边缘计算**: 全栈部署于 Cloudflare 基础设施，全球访问延迟极低。

---

## 🚀 快速开始与部署教程

### 1. 准备工作
* 一个 **Cloudflare** 账号。
* 代码托管于 **GitHub**。

### 2. 后端部署 (Cloudflare Workers + D1)
1.  **创建 D1 数据库**: 
    * 在 CF 控制台创建一个名为 `flow-db` 的数据库。
    * 执行初始化 SQL 创建 `projects` 和 `templates` 表。
2.  **配置 Worker**:
    * 新建一个 Worker (如 `flow-api`)。
    * **绑定 D1**: 在设置中将 `DB` 变量绑定到刚创建的数据库。
    * **设置暗号**: 在 **Settings -> Variables** 中添加环境变量：
        * 名称: `AUTH_KEY`
        * 数值: `你的自定义暗号` (例如 `MySecret123`)
3.  **部署代码**: 将后端 JavaScript 代码(worker.js)粘贴进编辑器并点击 **Deploy**。

### 3. 前端部署 (Cloudflare Pages)
1.  **修改配置**: 在 `index.html` 的 `<script>` 顶部，将 `API_URL` 修改为你 Worker 的实际地址。
2.  **关联 GitHub**: 在 Cloudflare Pages 中新建项目，连接你的 GitHub 仓库。
3.  **自动构建**: 选择静态部署，保存并点击部署。

### 4. 使用教程
1.  **首次登录**: 打开生成的 Pages 域名，页面会提示输入暗号。
2.  **配置模板**: 点击 **"⚙️ 流程设置"**，进入修改模式，根据业务需求创建分类（如：手作、外贸、研发）及具体步骤。
3.  **管理项目**: 
    * 主页点击 **"新建项目"**。
    * 点击下拉菜单即时切换进度，系统会自动记录操作日志。
    * 点击 **"归档"** 将完成的项目移入归档库。
4.  **清理数据**: 在 **"归档库"** 中，点击右上角红色小叉即可执行物理删除。

---

## 🛠️ 技术栈
* **Frontend**: Vanilla JS, CSS3 (CSS Variables), HTML5.
* **Backend**: Cloudflare Workers (Runtime).
* **Database**: Cloudflare D1 (SQLite).
* **Security**: Header-based Token Auth.

