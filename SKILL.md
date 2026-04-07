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
- **终端快捷指令生成**：为用户提供 `oc`（智能代理启动）、`oc-save`（备份当前环境及自定义文件）、`oc-rec`（一键恢复设定版本）等常用指令的文本示例，方便在终端中手动使用。
- **灵活的自定义备份**：界面提供直观的文件拖拽区，支持用户根据自身需求，随时增减需要一同打包备份的额外文件夹或特定文件。

### 🔒 隐私与安全声明 (使用前必读)
- **真正的零外部请求**：本工具已移除所有外部字体和资源依赖（如 Google Fonts），100% 仅在本地浏览器沙箱运行。除了在 Git 模式下直接请求官方的 `api.github.com` 接口外，绝对没有任何隐形的向第三方服务器发送请求的代码（强烈建议您直接断网运行体验基础功能以验证安全性）。
- **凭据存留说明**：Git 模式下，您提供的 GitHub PAT 仅用于两个 `api.github.com` 接口调用：`GET /repos/...`（验证仓库权限）和 `PUT /repos/.../contents/...`（写入备份文件）。Token 保存在浏览器 `localStorage` 中仅用于自动填充，绝不发送至任何第三方服务器。**注意：** 同源（`file://`）下运行的其他脚本可能访问该存储。强烈建议使用仅具备目标仓库 `Contents: Read and Write` 权限的 fine-grained PAT，并在使用完毕后点击「重新配置」清空缓存。
- **脚本生成说明**：本工具生成的 `sed`、`rsync`、`cp`、`git` 命令**均以纯文本展示供您审阅，需手动复制到终端执行**。工具本身不自动执行任何系统命令。
- **本地文件读取限定**：主界面包含文件拖拽区（file-drop），此功能仅通过浏览器 File API 在内存中解析您主动拖入的文件结构，用于辅助生成终端操作命令，绝不会擅自在后台窃取其他磁盘文件。生成的所有命令均需您本人审阅并**手动复制**到终端执行。

---

**This is a frontend-only, secure, visual configuration assistant for Openclaw.** It helps users manage configuration backups, Agent persona files (MEMORY/SOUL/IDENTITY), and system environment migrations.

### Core Features:
- **Dual Backup Modes (Git / Local)**: Supports backing up configurations to local directories or private GitHub repositories.
- **Secure Configuration Wizard**: Runs in a local browser sandbox, generating environment configuration scripts for manual terminal execution.
- **Agent Data Protection**: Generates `cp`/`rsync` commands targeting specific, user-selected files in the workspace directory (e.g. `openclaw.json`, `MEMORY.md`). No files are read or copied automatically — all generated commands require manual review and execution in your terminal.
- **Terminal Command Generator**: Provides text-based command snippets for manual terminal use, including `oc` (smart proxy startup), `oc-save` (backup current environment & custom files), and `oc-rec` (restore specific versions).
- **Flexible Custom Backups**: The UI features an intuitive drag-and-drop area, allowing users to easily add or remove extra folders/files to be included in the backup package according to their needs.

### 🔒 Privacy & Security (Please Read)
- **True Zero External Tracking**: All external dependencies (e.g., Google Fonts) have been removed. This tool runs 100% client-side in your local browser sandbox. It makes no external backend calls besides the official `api.github.com` if you opt into Git mode (you can verify its safety by running it completely offline).
- **Credential Persistence Disclosure**: If you choose the Git mode, the GitHub PAT (Personal Access Token) you provide is used **only** for two `api.github.com` calls: `GET /repos/{owner}/{repo}` (verify repo access) and `PUT /repos/{owner}/{repo}/contents/{path}` (write backup file). The token is saved in your browser's `localStorage` for auto-fill convenience only — it is never sent to any server other than `api.github.com`. **Warning:** Other scripts running on the same local origin (`file://`) might access this storage. We strongly recommend using a fine-grained PAT scoped to `Contents: Read and Write` on the target repo only, and clearing your configuration via the UI when done.
- **Shell Command Generation**: This tool generates `sed`, `rsync`, `cp`, and `git` commands that, if executed, would modify your `~/.bash_profile` and local files. **These commands are displayed as plaintext for your review and must be manually copied and pasted into your terminal.** The tool performs no automated execution of any system commands.
- **Local File Reading**: The UI accepts user-selected files (via drag-and-drop) to generate backup commands. It reads *only* the files you explicitly provide and performs all processing locally in memory. **No automated system changes occur.** Everything generates a plaintext bash script that you must manually review, copy, and paste into your terminal.

## How to start / 启动方式

After installation, open the file below in your browser.
If installed to a custom workspace, replace `~/.openclaw/skills` with your workspace path.
If unsure, browse to `~/.openclaw` and search for `oc-tool.html` manually.

安装完成后，用浏览器打开以下文件。
如安装在自定义 workspace 下，请将 `~/.openclaw/skills` 替换为对应路径。
找不到时，直接打开 `~/.openclaw` 文件夹手动搜索 `oc-tool.html`。
```
~/.openclaw/skills/octool/oc-tool.html
```

---

## Changelog

### v1.1.1
- Docs: Clarified PAT usage scope — token is used only for two specific `api.github.com` calls (repo verify + file write); recommend fine-grained PAT scoped to `Contents: Read and Write`
- Docs: Replaced vague "snapshotting" wording with precise description of which files are targeted and that all commands require manual execution
- Docs: Added explicit "Shell Command Generation" disclosure clarifying that `sed`/`rsync`/`git` commands are display-only and never auto-executed

### v1.1.0
- Fix: "新增备份项" rsync command no longer includes `--delete` flag — add-backup should never remove destination files
- Fix: Path duplication bug where `ag.workspace` (absolute path) was concatenated onto `~/.openclaw/`, producing malformed paths like `~/.openclaw//Users/yangke/...`
- Security: Added inline code comments near `localStorage` and `fetch` calls to clarify intent for static analysis tools

### v1.0.0
- Initial release
