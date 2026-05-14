# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with this repository.

## Project Overview

An Obsidian vault ("Gen Obsidian Lib") — a machine learning knowledge base built on the **Karpathy LLM Wiki** pattern: raw materials are compiled into a structured, interlinked wiki.

## Git Workflow

- Commits are made directly to `main` branch.
- Commit messages should be short and descriptive.
- Push upstream after committing to sync the vault.

## Vault Structure

```
├── raw/                          # 原始素材层（只读，AI 不修改原文）
│   ├── 01-articles/             # 网页剪藏、技术文章
│   ├── 02-papers/               # 论文、研究报告
│   ├── 03-transcripts/          # 视频/播客字幕（B站、YouTube 等）
│   └── 09-archive/              # 已处理的素材归档
│
├── Wiki/                         # 知识编译输出层（LLM 写入，人类阅读）
│   ├── index.md                 # 全局内容索引（每页一行摘要）
│   ├── log.md                   # 操作日志（grep-friendly ingest/query 历史）
│   ├── sources/                 # 单篇素材的要点提取（1:1 对应 raw/ 文件）
│   ├── concepts/                # 概念层：方法论、架构模式、第一性原理
│   └── entities/                # 实体层：人物、公司、工具、项目
│
├── .obsidian/                    # Obsidian 配置（不手动修改）
├── copilot/                      # Copilot 相关
└── CLAUDE.md                     # 本文件
```

## 处理流程（ingest 工作流）

1. 原始素材放入 `raw/` 对应子目录
2. 在 `Wiki/sources/` 创建要点提取笔记（文件名：`标题-YYYY-MM-DD.md`）
3. 在 `Wiki/log.md` 记录操作
4. 更新 `Wiki/index.md` 添加新条目
5. 可选：将关联概念提炼到 `Wiki/concepts/`，关联实体记录到 `Wiki/entities/`

## 可用技能

- `/ingest` — 扫描 `raw/` 中的新素材，验证格式，编译为 Wiki 笔记

## Wiki 笔记规范

- sources/ 笔记文件名格式：`标题-YYYY-MM-DD.md`，一级标题不包含日期
- sources/ 笔记末尾必须添加指向 raw/ 中原始素材的反向链接
- 使用双向链接关联 [[Wiki/concepts/]] 和 [[Wiki/entities/]]
- 每次新增/修改后同步更新 index.md

## pages 模板

### sources/ 模板

```markdown
# 标题

> 来源：[名称](链接)
> 日期：YYYY-MM-DD

## 核心观点

## 关键要点

## 关联

- [[Wiki/concepts/相关概念]]
- [[Wiki/entities/相关实体]]
- [[raw/XX子目录/原始素材|原始素材]]
```

### concepts/ 模板

```markdown
# 概念名称

## 定义

## 核心原理

## 关联

- [[Wiki/sources/相关来源]]
- [[Wiki/entities/相关实体]]
```

### entities/ 模板

```markdown
# 实体名称

## 简介

## 关联

- [[Wiki/concepts/相关概念]]
- [[Wiki/sources/相关来源]]
```
