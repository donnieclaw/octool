---
name: octool
description: Openclaw Visual Configuration Assistant. Provides secure wizard for local/Git backup and workspace migration.
homepage: https://github.com/donnieclaw/octool
metadata: {"clawdbot":{"emoji":"🖥️"}}
---

# Openclaw Backup Assistant (oc-tool)

**🌍 English Description Below | 中文介绍在上方**

这是一个纯前端的安全、可视化的 Openclaw 配置管理助手。它旨在帮助用户管理 Openclaw 的配置备份、Agent 灵魂文件（MEMORY/SOUL/IDENTITY）以及系统环境迁移。

### 主要功能：
- **Git / 本地双模备份**：支持将配置备份至本地目录或私有 GitHub 仓库。
- **安全配置向导**：运行于浏览器本地沙箱，为用户生成可供手动执行的环境配置脚本。
- **Agent 数据保护**：覆盖 workspace 目录下的关键文件快照，防止数据丢失。
- **终端快捷指令生成**：为用户提供 oc-save、oc-rec 等常用备份指令的文本示例，方便在终端中手动使用。

### 🔒 隐私与安全声明 (使用前必读)
- **真正的零外部请求**：本工具已移除所有外部字体和资源依赖（如 Google Fonts），100% 仅在本地浏览器沙箱运行。除了在 Git 模式下直接请求官方的 `api.github.com` 接口外，绝对没有任何隐形的向第三方服务器发送请求的代码（强烈建议您直接断网运行体验基础功能以验证安全性）。
- **凭据存留说明**：如果您选择使用 Git 模式，系统会要求您提供 GitHub Token (PAT)。该 Token 完全用于在前端发起对 GitHub 的直接 API 请求，并会明文保存在您当前浏览器的 `localStorage` 中以便下次自动填充。**注意：** 同源下运行的其他恶意扩展可能有权访问该缓存。建议使用遵循最小权限原则（Least-privilege）的临时 Token，或在使用完毕后点击工具上方的「重新配置」以清空缓存。
- **本地文件读取限定**：主界面包含文件拖拽区（file-drop），此功能仅通过浏览器 File API 在内存中解析您主动拖入的文件结构，用于辅助生成终端操作命令，绝不会擅自在后台窃取其他磁盘文件。生成的所有命令均需您本人审阅并**手动复制**到终端执行。

---

**This is a frontend-only, secure, visual configuration assistant for Openclaw.** It helps users manage configuration backups, Agent persona files (MEMORY/SOUL/IDENTITY), and system environment migrations.

### Core Features:
- **Dual Backup Modes (Git / Local)**: Supports backing up configurations to local directories or private GitHub repositories.
- **Secure Configuration Wizard**: Runs in a local browser sandbox, generating environment configuration scripts for manual terminal execution.
- **Agent Data Protection**: Targets key files in the workspace directory for snapshotting to prevent data loss.
- **Terminal Command Generator**: Provides text-based command snippets (e.g., oc-save, oc-rec) for manual use in the terminal.

### 🔒 Privacy & Security (Please Read)
- **True Zero External Tracking**: All external dependencies (e.g., Google Fonts) have been removed. This tool runs 100% client-side in your local browser sandbox. It makes no external backend calls besides the official `api.github.com` if you opt into Git mode (you can verify its safety by running it completely offline).
- **Credential Persistence Disclosure**: If you choose the Git mode, the GitHub PAT (Personal Access Token) you provide is sent strictly to GitHub and is saved in your browser's persistent `localStorage` for convenience. **Warning:** Other scripts running on the same local origin (file://) might access this storage. We strongly recommend using short-lived or least-privilege tokens, and clearing your configuration via the UI when done.
- **Local File Reading**: The UI accepts user-selected files (via drag-and-drop) to generate backup commands. It reads *only* the files you explicitly provide and performs all processing locally in memory. **No automated system changes occur.** Everything generates a plaintext bash script that you must manually review, copy, and paste into your terminal.

## How to start / 启动方式

终端或 Openclaw 聊天框中运行以下命令以在浏览器中打开界面：
Run the following command in your terminal or Openclaw chat to open the interface in your browser:

```bash
open {baseDir}/oc-tool.html
```
