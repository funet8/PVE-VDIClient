# PVE-VDIClient

**Proxmox VE 虚拟桌面基础架构（VDI）客户端**

![VDI 客户端主页](screenshots/vdiview.png)

一个基于 Python 3 和 customtkinter 构建的跨平台 VDI 客户端，用于连接和管理 Proxmox VE 上的虚拟机。

## 功能特性

- 通过 **SPICE 协议**一键连接 Proxmox 虚拟机
- 支持**用户名/密码 + TOTP 两步认证**
- 图形化虚拟机列表，清晰显示运行状态
- 支持**重置**、**休眠**等虚拟机管理操作
- **Kiosk 全屏模式**，适合公共/自助终端场景
- 支持**多 Proxmox 集群**配置和管理
- 配置可从本地文件或远程 HTTP 获取
- 跨平台支持 Windows 和 Linux

## 截图

| 登录界面 | TOTP 认证 | 虚拟机列表 |
|---|---|---|
| ![登录界面](screenshots/login.png) | ![TOTP 认证](screenshots/login-totp.png) | ![虚拟机列表](screenshots/vdiview.png) |

## 前置依赖

- **Python 3.8+**
- **[virt-viewer](https://virt-manager.org/)**（SPICE 远程桌面客户端）
- Python 依赖（见下方安装说明）

## 快速安装

### 1. 安装 Python 依赖

```bash
pip install proxmoxer requests customtkinter
```

### 2. 安装 virt-viewer

- **Windows**：下载并安装 [virt-viewer](https://virt-manager.org/download/)
- **Linux (Debian/Ubuntu)**：`sudo apt install virt-viewer`

### 3. 配置并启动

1. 复制 `vdiclient.ini.example` 为 `vdiclient.ini` 并按需修改配置
2. 运行客户端：

```bash
python vdiclient.py
```

## 配置文件

客户端支持通过 INI 配置文件进行灵活配置。配置文件查找顺序：

- **Windows**：`%APPDATA%\VDIClient\vdiclient.ini` → `%PROGRAMFILES%\VDIClient\vdiclient.ini`
- **Linux**：`~/.config/VDIClient/vdiclient.ini` → `/etc/vdiclient/vdiclient.ini`

配置示例请参考 `vdiclient.ini.example`。

## 命令行参数

```bash
python vdiclient.py [选项]

选项：
  --config_location PATH    配置文件路径或 URL
  --config_type {file,http} 配置文件来源（文件或 HTTP）
  --config_username TEXT     HTTP 配置认证用户名
  --config_password TEXT     HTTP 配置认证密码
  --ssl_verify {True,False} 是否验证 SSL 证书
  --kiosk                   启用 Kiosk 模式
  --hostset TEXT            默认主机集名称
  --debug                   启用调试输出
```

## 打包构建

### Windows 可执行文件

运行 `build_vdiclient.bat`，使用 PyInstaller 打包：

```bat
build_vdiclient.bat
```

### MSI 安装包

```bash
python dist/createmsi.py dist/vdiclient.json
```

## 技术栈

| 组件 | 技术 |
|------|------|
| 图形界面 | customtkinter |
| Proxmox API | proxmoxer |
| 远程桌面协议 | SPICE（virt-viewer） |
| 打包工具 | PyInstaller + MSI |
| 版本 | v3.0.0 |

## 许可

本项目基于 Apache 2.0 许可协议开源，详见 LICENSE 文件。
