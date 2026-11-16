---
title: "Git基础概念"
_legacy_source: "git使用指南/Git基础概念.md"
_original_note: true
legacy_title_id: "git基础概念"
created: "2026-04-18T00:26:44+08:00"
modified: "2026-04-18T00:26:44+08:00"
tags: ["git使用指南"]
---

Git 里先分清工作区、暂存区和版本库，再看文件在这些位置之间怎么变化，后面的命令就容易对应起来了。

## 工作区,暂存区和版本库

```text
工作区（Working Directory）
    ↓ git add
暂存区（Staging Area / Index）
    ↓ git commit
本地仓库（Local Repository）
    ↓ git push
远程仓库（Remote Repository）
```

## 文件状态流转

```text
Untracked（未跟踪）
    ↓ git add
Staged（已暂存）
    ↓ git commit
Unmodified（未修改）
    ↓ 编辑文件
Modified（已修改）
    ↓ git add
Staged（已暂存）
```

## 相关笔记

- [基本操作命令](git使用指南/基本操作命令.md)：用 add 和 commit 对应这些状态变化。
- [工作区暂存](git使用指南/工作区暂存.md)：用 stash 临时收起还没做完的修改。
