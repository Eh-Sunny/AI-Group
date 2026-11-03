# 💬 AI-Group

> 一个纯前端、单文件运行的「多 AI 角色群聊」聊天应用 —— 让多个大模型同台竞技、接力发言、自由辩论。

[![HTML](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)](https://developer.mozilla.org/zh-CN/docs/Web/HTML)
[![CSS](https://img.shields.io/badge/CSS3-1572B6?logo=css3&logoColor=white)](https://developer.mozilla.org/zh-CN/docs/Web/CSS)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript)
[![No Build](https://img.shields.io/badge/build-none-brightgreen)]()
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## ✨ 简介

**AI-Group** 是一个**零依赖、零构建、单文件**的 AI 聊天应用。打开 `index.html` 即可使用，所有数据保存在浏览器本地（localStorage），无需后端服务器。

你可以在一个对话中同时召集多个 AI 角色，让它们**接力发言**、**横向对比**或**相互辩论**，也可以回归传统的一问一答。兼容所有提供 OpenAI 接口格式（`/chat/completions`）的模型服务。

---

## 🎯 核心特性

### 🤖 四种对话模式

| 模式 | 说明 |
|------|------|
| **群聊模式** | 随机顺序、接力发言。后面的 AI 能看到前面 AI 的回复，避免重复 |
| **并列模式** | 所有 AI 同时回答，横向对比不同模型的输出 |
| **辩论模式** | 四阶段辩论：初步看法 → 相互评价 → 自由辩论 ×2 轮 |
| **传统模式** | 单个模型，一问一答 |

> 模式在对话创建时确定，对话开始后锁定，避免上下文混乱。

### 🧠 多模型与容错

- **多 API 配置**：可添加多个 API 端点（如 DeepSeek、OpenAI、通义千问、本地 Ollama 等）
- **主模型 + 备用模型**：主模型失败时自动按顺序切换备用模型，支持**拖拽排序**
- **多 AI 角色**：每个角色可独立绑定配置、模型、头像、系统提示词
- **流式输出**：SSE 实时流式渲染，支持显示**思考过程（reasoning）**
- **Token 统计**：实时显示 tokens 数量与生成速度（t/s）

### 📝 富文本与代码能力

- 完整的 **Markdown 渲染**：标题、列表、表格、引用、分隔线、行内代码、链接、加粗斜体等
- **代码块增强**：复制 / 下载 / **在线运行预览**（支持 HTML、CSS、JS、Markdown）
- **消息操作**：重新生成、继续生成、编辑用户消息后重新生成、随时中断

### 🧩 扩展生态

- **MCP（Model Context Protocol）**：连接 MCP 服务器，AI 对话中自动调用其工具
- **Skills 技能系统**：
  - 手动编写 skill.md（YAML Front Matter）
  - 从本地文件批量导入
  - **从 GitHub 仓库递归抓取**整个技能包
  - 关键词触发，自动注入上下文
- **插件系统**：编写自定义 HTML/JS，以独立悬浮窗形式在工具栏运行
- **知识库**：文件夹树、标签、多格式文档，支持本地搜索
- **外部平台**：对接主流知识库平台

### 📎 多格式文件上传

- 🖼️ **图片**：多模态视觉输入（Base64）
- 📄 **PDF**：`pdf.js` 解析文本
- 📝 **Word**：`mammoth.js` 解析 `.docx`
- 📃 **文本**：txt / md / json / 代码文件等
- 支持**拖拽上传**、附件预览、编辑消息时增删附件

### 💾 数据管理

- 多对话管理：历史记录、重命名、删除
- **一键导出 / 导入 JSON 备份**（可选择导出范围与合并/覆盖模式）
- 深色 / 浅色主题切换
- 全响应式布局：手机、平板、桌面全屏适配
- 浏览器返回键手势友好（History API）

---

## 🚀 快速开始

### 方式一：本地直接打开（推荐）

1. 下载或克隆本仓库：
   ```bash
   git clone https://github.com/你的用户名/AI-Group.git
   cd AI-Group
   ```
2. 用浏览器打开 `index.html`（推荐 Chrome / Edge / Safari 最新版）

> ⚠️ 部分浏览器对本地 `file://` 协议下的 `fetch` / `localStorage` 有限制，建议用本地服务器：
> ```bash
> # Python 3
> python -m http.server 8080
> # 或 Node.js
> npx serve
> ```
> 然后访问 `http://localhost:8080`

### 方式二：GitHub Pages 在线部署

1. 将代码推送到 GitHub 仓库
2. 进入仓库 **Settings → Pages**
3. Source 选择 `main` 分支、`/ (root)` 目录
4. 保存后访问 `https://你的用户名.github.io/AI-Group/`

### 首次配置

1. 点击右上角 **⚙ 配置中心** → **API 配置** → **＋ 新增配置**
2. 填写：
   - **API 地址**：如 `https://api.deepseek.com/v1`
   - **API Key**：你的密钥
   - 点击 **获取模型** 或手动添加模型名
3. 进入 **AI 角色配置**，新建 / 编辑角色，绑定配置、选择模型、填写提示词
4. 返回聊天界面，**@** 选择参与的 AI，开始聊天 🎉

---

## ⚙️ 兼容的 API 服务

只要是 **OpenAI 接口格式**即可（`POST {apiBase}/chat/completions`，`Authorization: Bearer {key}`）：

- DeepSeek
- OpenAI / Azure OpenAI
- 通义千问、Kimi、智谱 GLM、MiniMax
- Ollama（`http://localhost:11434/v1`）
- LM Studio、vLLM、One-API 等自建网关
- 任何兼容 `/v1/chat/completions` 的服务

---

## 🧭 使用指南

### 群聊 / 并列 / 传统模式

1. 在输入框输入问题，可用 **@** 选择参与的 AI（默认全部）
2. 点击 **↑** 发送，AI 将按当前模式回复
3. 生成过程中点击 **⏹** 可随时中断
4. 点击 AI 消息底部的 **↺** 重新生成，或 **▶️ 继续** 从中断处接续

### 辩论模式

1. 切换到「辩论模式」，输入话题
2. 系统自动依次执行四个阶段，每个阶段 AI 同时发言
3. 阶段之间会插入分隔标记，完整记录整场讨论

### 代码块操作

- **📋 复制**：复制到剪贴板
- **💾 下载**：按语言自动匹配扩展名
- **▶️ 运行**：HTML 直接渲染；JS 注入 Console 面板；CSS 生成示例页面；Markdown 实时渲染

### Skills 技能

- **配置中心 → Skills → ＋ 添加技能**
- 三种方式：手动编辑 / 本地文件导入 / GitHub 导入
- 技能使用 Markdown + YAML Front Matter：
  ```markdown
  ---
  name: 代码审查
  icon: 🔍
  keywords: review, 审查, 检查代码
  description: 对代码进行专业审查
  enabled: true
  ---

  你是一位资深代码审查专家，请从以下维度审查……
  ```
- 用户消息命中 `keywords` 时，技能指令会自动注入到 AI 上下文

### 插件

- **配置中心 → 插件 → ＋ 新增插件**
- 填写 HTML 内容与 JS 逻辑，保存后出现在输入框工具栏
- 支持附加资源文件（文本 / Base64），插件内通过 `window.pluginResources` 访问
- 可向主程序发送提示：
  ```js
  window.parent.postMessage({ type: 'toast', text: '操作成功' }, '*');
  ```

### 数据备份

- 侧边栏底部 → **📤 导出**：勾选要导出的内容（配置、角色、对话、知识库、平台、MCP、技能、插件），生成 JSON 文件
- **📥 导入**：支持**覆盖**或**合并**两种模式

---

## 🛠️ 技术栈

| 技术 | 用途 |
|------|------|
| 原生 HTML / CSS / JavaScript | 全部 UI 与交互，**无框架、无构建工具** |
| Fetch API + ReadableStream | SSE 流式响应解析 |
| localStorage | 全部数据的持久化存储 |
| History API | 支持浏览器返回键关闭弹层 |
| [pdf.js](https://mozilla.github.io/pdf.js/) (CDN) | PDF 文本提取 |
| [mammoth.js](https://github.com/mwilliamson/mammoth.js) (CDN) | Word `.docx` 文本提取 |
| OpenAI Chat Completions API | 模型调用（含 Tool Calls） |
| MCP (Model Context Protocol) | 外部工具接入 |

---

## 📁 项目结构

```
AI-Group/
├── index.html      # 单文件应用（HTML + CSS + JS 全在这里）
└── README.md       # 本说明文档
```

> 项目刻意保持**单文件**形态，便于分享、二次修改和部署到任意静态托管。

---

## ⚠️ 注意事项

- **API Key 安全**：所有配置（包括 Key）均以**明文**存储在浏览器 `localStorage` 中。请勿在公共设备上保存敏感 Key；也请勿将包含真实 Key 的导出文件上传到公开仓库。
- **CORS 限制**：浏览器直连 API 需要服务端允许跨域（CORS）。大多数公有云 API 已支持；本地自建服务请自行配置。
- **数据不跨设备**：数据只保存在当前浏览器，换设备请使用导出/导入功能。
- **模型能力差异**：不同模型的 Markdown、思考链、工具调用支持程度不同，展示效果会有差异。
- **工具调用**：MCP 工具调用依赖模型本身的 Function Calling 能力。

---

## ❓ 常见问题

**Q：打开后提示「请先添加 API 配置」？**
A：点击右上角 ⚙ → API 配置，添加至少一个可用的 API 端点与 Key，并获取模型列表。

**Q：AI 回复报错 HTTP 401 / 403？**
A：检查 API Key 是否正确、是否有余额、API 地址是否包含正确的 `/v1` 路径。

**Q：获取模型失败？**
A：部分服务不支持 `/models` 端点。可点击「手动输入模型名称」自行添加。

**Q：为什么 AI 会“扮演”其他角色？**
A：代码已内置身份约束提示词（群聊/辩论模式）。若仍出现，可在角色的系统提示词中进一步强调，或换用指令遵循能力更强的模型。

**Q：群聊模式下前面的 AI 回复太长，后面的 AI 重复内容？**
A：这是模型行为差异。可在提示词中强调「简洁精炼、避免重复」，或减少参与角色数量。

**Q：PDF / Word 解析失败？**
A：需要联网加载 CDN 上的 pdf.js / mammoth.js；扫描版 PDF 无文本层，无法提取。

---

## 🤝 贡献

欢迎提交 Issue 与 Pull Request！

1. Fork 本仓库
2. 创建特性分支：`git checkout -b feature/your-feature`
3. 提交改动：`git commit -m 'feat: add something'`
4. 推送分支：`git push origin feature/your-feature`
5. 发起 Pull Request

---

## 📄 License

**AI-Group** 基于 [MIT License](LICENSE) 开源，可自由使用、修改与分发。

---

## ⭐ Star History

如果这个项目对你有帮助，欢迎点个 Star ⭐ 支持一下！

---

<p align="center">AI-Group · Made with ❤️ and a single HTML file</p>