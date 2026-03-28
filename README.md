🚀 Project Flow Manager | 项目流管理器 “让每一个项目，都像艺术品一样流动。”

这是一个基于 GitHub API 构建的极简、私密、且具备高度审美视觉的项目进度管理工具。专为追求高效与界面美感的独立开发者/产品经理设计。

📸 视觉哲学 (Design Philosophy) Ins-Style UI: 采用微渐变、毛玻璃滤镜（Backdrop Blur）与卡片式布局。

Aesthetic Palette: 经过挑选的 8 种马卡龙色系顶部饰条，自动区分不同项目。

Dynamic Response: 流畅的进度条动画与直观的状态反馈。

✨ 核心特性 (Key Features)

流程自定义 (Dynamic Workflow) 不仅仅是简单的 To-Do。你可以自由定义“立项-审核-执行-结算”等任何阶段。每个项目都能适配专属的生命周期。

GitHub 无感同步 (Cloud Native) 无需后端服务器。利用 GitHub API 实现数据的全自动持久化存储，让你的私人项目流随处可用且永不丢失。

智能归档库 (Smart Archive) 时光机: 记录每个项目的起始与终结。

极简卡片: 220px 紧凑布局，一眼纵览历史沉淀。

搜索与筛选: 支持按年份、流程分类及关键字实时检索。

安全锁: 归档超过 30 天的项目将自动锁定，防止手抖误删。

效率补丁 (Efficiency Tweaks) 📌 快捷置顶: 重要项目始终保持在视线焦点。 🕒 变更日志: 自动记录每一次步骤调整与备注更新。

💰 预算追踪: 实时掌控每个项目价值。

🛠️ 技术栈 (Tech Stack) Logic: Pure JavaScript (Vanilla JS)

Style: CSS3 Flex/Grid + Glassmorphism

Data: GitHub REST API

Platform: Cloudflare Pages / Vercel / GitHub Pages

🚀 快速开始 (Quick Start) Fork 本仓库。

在控制台输入你的 GitHub Personal Access Token 及仓库信息。

开启你的高效管理之旅。

Bash

不需要安装依赖，直接打开 index.html 即可运行 open index.html 📅 版本迭代 (Changelog) v1.3.12: 归档卡片样式大一统，日期合并，视觉密度再优化。

v1.3.10: 引入 220px 档案柜式栅格布局，移除冗余按钮。

v1.3.0: 接入 GitHub API，实现真正意义上的云端同步。

💌 结语 保持专注，让流程自然发生。

既然这个项目（暂且称之为 Project Flow v1.5.5）已经具备了 GitHub 云端同步、智能主题切换以及复杂的流程管理功能，那么部署它的核心就在于 GitHub 仓库的配置。

这份文档将引导一个“小白”用户从零开始，在 5 分钟内搭建起这套私人的项目流管理系统。

🚀 Project Flow 项目流管理系统部署指南
本系统是一个**无服务器（Serverless）**的纯前端项目。它通过 GitHub API 将数据存储在您的私人仓库中，实现多端同步和永久存储。

📥 第一步：准备 GitHub 仓库
由于系统需要读取和写入数据，我们需要准备两个基础文件。

创建一个新仓库：
登录 GitHub，点击 New repository。
仓库名称建议：workflow-data。
权限选择：建议设为 Private（私有），保护您的项目数据。
创建数据文件 data.json：
在仓库根目录新建一个文件，命名为 data.json。
内容填入：{"projects": [], "trash": []}。
创建流程模板文件 template.json：
在仓库根目录新建另一个文件，命名为 template.json。
内容建议填入以下初始模板：
{
  "通用流程": ["开始", "进行中", "已完成"],
  "开发流程": ["需求", "编码", "测试", "发布"]
}
获取模板直链：点击 GitHub 仓库中的 template.json 文件，点击右上角的 Raw 按钮，复制该地址。
提示：这个地址将填入代码中的 GLOBAL_TPL_URL 变量处。
🔑 第二步：生成 GitHub 访问令牌 (Token)
为了让网页能够把数据保存到您的 GitHub 仓库，您需要授权。

访问 GitHub 的 Settings > Developer settings > Personal access tokens (classic)。
点击 Generate new token (classic)。
Note（备注）：填写 Workflow-Key。
Expiration（过期时间）：建议选 No expiration（永不过期）。
Scopes（权限范围）：勾选 repo 这一整项即可（这将允许系统读写您的私有仓库）。
保存 Token：点击底部的 Generate token，务必立即复制并保存这个 Token，因为它只会出现一次！
💻 第三步：本地配置与部署
现在我们将代码（index.html）与您的 GitHub 仓库建立连接。

修改代码变量（找到 script 标签的前几行）：
将 GLOBAL_TPL_URL 的值替换为您在第一步复制的 template.json 的 Raw 链接。
启动网页：
将代码保存为 index.html。
使用任何浏览器打开该文件，或将其上传到您的个人服务器（如 OpenWrt 的 iStore 导航、Cloudflare Pages 等）。
初始化配置：
第一次打开页面，系统会自动弹出 🔑 云端配置 对话框。
User：填写您的 GitHub 用户名。
Repo：填写您的仓库名（如 workflow-data）。
Token：填入您在第二步生成的访问令牌。
点击 保存。
🛠️ 第四步：进阶使用与流程更新
1. 修改流程模板
如果您需要增加或修改业务流程：

直接在 GitHub 仓库中编辑 template.json。
回到网页端，点击 “⚙️ 流程设置”。
点击弹窗右上角的 “🔄 强制同步” 按钮。由于我们加入了随机指纹（Cache Busting）逻辑，系统会瞬间绕过 GitHub CDN 缓存，拉取最新定义的流程。
2. 日夜模式自动切换
06:00 - 18:00：自动切换至日间模式（浅灰背景）。
18:00 - 次日 06:00：自动切换至夜间模式（深黑背景，护眼适配）。
提示：系统每分钟会自动检查一次时间并进行无缝切换。
❓ 常见问题排查 (Q&A)
Q: 点击保存后，右上角的同步圆点一直是橙色的？
A: 请检查 GitHub Token 是否正确勾选了 repo 权限，以及仓库名称是否填错。
Q: 为什么我改了 template.json，网页端还没更新？
A: 请确保点击了“流程设置”弹窗里的“强制同步”按钮。如果还没变，检查 JSON 格式是否有效（缺少逗号或括号会导致解析失败）。
Q: 可以在手机上使用吗？
A: 可以。该项目采用了响应式设计，在手机浏览器中访问时，卡片会自动堆叠显示。
