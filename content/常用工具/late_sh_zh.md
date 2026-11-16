---
title: "late.sh"
_legacy_source: "常用工具/late_sh_zh.md"
_original_note: true
legacy_title_id: "latesh"
created: "2026-05-15T00:00:58+08:00"
modified: "2026-05-25T23:57:52+08:00"
tags: ["常用工具"]
---

> 一个舒适的终端开发者俱乐部。Lo-fi 音乐、休闲游戏、聊天和科技新闻，全部通过 SSH 访问。

```bash
ssh late.sh
```

`late.sh` 把聊天、音乐、游戏、新闻和个人资料这些功能放进了终端，通过 SSH 就能连接到共享空间。这里记一下功能和运行方式，自部署步骤先留作参考。

## 功能包含

- 包含仪表盘、聊天、个人资料、新闻和街机界面的 SSH TUI
- 实时全球聊天和共享活动动态
- 通过 Icecast/Liquidsoap 实现的音频流，支持浏览器与 CLI 配对
- 终端游戏，包括 2048、数独、Nonograms、扫雷和纸牌
- 用于着陆页、连接流程和配对客户端体验的 Web 前端
- 用于本地音频播放和同步可视化数据的伴随 CLI 工具

## 技术栈

基于 Rust 工作空间构建，包含 `late-cli`、`late-core`、`late-ssh`、`late-web` 四个 crate，由 PostgreSQL、Icecast 和 Liquidsoap 支撑。

## 快速开始

试用线上服务：

```bash
ssh late.sh
```

自行运行（需要 Docker）：

```bash
git clone https://github.com/mpiorowski/late-sh
cd late-sh
make start
```

本地实例启动后，用下面的命令连接：

```bash
ssh localhost -p 2222
```

这套启动方式会自动启动 PostgreSQL、Icecast 和 Liquidsoap。

## 伴随 CLI

除了 SSH 界面，还有一个配套 CLI，用来在本地播放音频和同步可视化：

macOS / Linux / Termux：

```bash
curl -fsSL https://cli.late.sh/install.sh | bash
```

在 Termux 上，安装脚本会获取 Android CLI 构建版本，而非 GNU/Linux 版本。

Windows PowerShell（x64）：

```powershell
irm https://cli.late.sh/install.ps1 | iex
```

Nix / NixOS：

```bash
nix run github:mpiorowski/late-sh#late
```

或从源码构建：

```bash
mise install        # 可选 — 配置所需的 Rust 工具链
cargo build --release --bin late
```

## 本地开发

本地开发时，也可以只把基础设施放进 Docker，Rust 应用本身留在本机运行，不必把整个构建过程都放进容器：

```bash
docker compose up -d postgres icecast liquidsoap
cargo run -p late-ssh
cargo run -p late-web
```

本机开发可以照常使用 Cargo 的默认配置，构建结果放在仓库本地的 `target/` 里。`/app/target` 只是 Docker／开发容器中的路径。

```bash
export CARGO_HOME=$HOME/.cargo
```

使用 `mise install` 获取所需的 Rust 工具链、`mold` 链接器和 `cargo-nextest`。

## 验证

如果准备向上游提交 PR，可以先运行：

```bash
make check
```

它会依次运行 `cargo fmt --check`、`cargo clippy` 和 `cargo nextest`。
部分集成测试通过 testcontainers 使用 Docker，跑这部分时还需要有可用的 Docker 环境。

## 相关笔记

- [Cargo 工作区与依赖管理](Rust/Cargo工作区与依赖管理.md)：多个 crate 放在同一个 workspace 里的组织方式。
