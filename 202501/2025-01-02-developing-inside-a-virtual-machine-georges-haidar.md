# Developing inside a virtual machine | Georges Haidar
- URL: https://blog.disintegrator.dev/posts/dev-virtual-machine/
- Added At: 2025-01-02 00:30:54
- [Link To Text](2025-01-02-developing-inside-a-virtual-machine-georges-haidar_raw.md)

## TL;DR
作者在Speakeasy新工作中，选择在MacBook上使用VMWare Fusion Pro虚拟机作为主要开发环境，配置Ubuntu 24.04操作系统。通过iTerm2和Visual Studio Code远程开发扩展，实现了高效的工作流。虚拟机环境提供了系统隔离和稳定性，尽管存在剪贴板功能缺失等小问题，整体体验非常满意，未来仍有优化空间。

## Summary
1. **背景与动机**：
   - **新工作环境**：作者在Speakeasy开始新工作，需要管理多语言工具链和依赖，促使他重新思考开发环境。
   - **开发机器问题**：过去开发机器因安装过多服务和依赖而变得臃肿，存在安全隐患。

2. **虚拟机开发环境**：
   - **灵感来源**：受Mitchell Hashimoto的启发，作者选择在MacBook上使用虚拟机作为主要开发环境。
   - **具体配置**：
     - **主机**：2023款MacBook Pro，M2 Pro CPU，32GB RAM。
     - **虚拟机软件**：VMWare Fusion Pro，性能表现优异，几乎无感知。
     - **操作系统**：Ubuntu 24.04（arm64），选择原因是快速设置且稳定。

3. **开发工具与工作流**：
   - **终端与编辑器**：
     - **iTerm2**：用于SSH连接到虚拟机，支持tmux集成，提供流畅的终端体验。
     - **Visual Studio Code**：使用远程开发扩展，所有编辑器扩展安装在虚拟机内。
   - **Git/GitHub工作流**：
     - **SSH密钥管理**：使用1Password存储和管理SSH密钥，通过1Password的SSH代理在虚拟机内访问。
   - **网络服务访问**：使用Tailscale为虚拟机创建DNS名称，方便从主机访问TCP服务。

4. **优点**：
   - **系统隔离**：虚拟机内的开发工具和扩展不会影响主机性能，提供一定的安全防护。
   - **透明性**：VMWare几乎无感知，系统响应迅速，即使虚拟机内运行繁重任务。
   - **稳定性**：长期使用后，系统依然保持高效，避免了开发工具和服务的积累问题。

5. **缺点与调整**：
   - **剪贴板功能缺失**：`pbcopy`和`pbpaste`在主机和虚拟机之间不可用，作者已适应这一限制。
   - **文件共享**：不使用磁盘共享，依赖Mountain Duck通过SFTP挂载虚拟机文件，偶尔需要拖放文件。

6. **总结**：
   - **平衡与满意**：作者认为当前的虚拟机开发环境在安全性和稳定性方面表现出色，尽管有一些小不便，但整体体验非常满意。
   - **未来改进**：虽然已有良好基础，作者仍认为有进一步优化的空间。
