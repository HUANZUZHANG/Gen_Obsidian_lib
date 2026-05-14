---
name: ingest
description: Scan raw/ for new materials, validate format, and compile into Wiki/ knowledge base. Use when user says /ingest or asks to process raw materials.
user-invocable: true
---

# Ingest Skill

Scan `raw/` for new/unprocessed materials and compile them into the Wiki knowledge base.

## Workflow

### Step 1: Scan raw/ for unprocessed files

Look for markdown files in `raw/01-articles/`, `raw/02-papers/`, `raw/03-transcripts/` that have NOT yet been archived (i.e. not in `raw/09-archive/`).

Also check if there are any markdown files **directly inside `raw/`** (not in a subdirectory) — these are misplaced.

### Step 2: Validate format

Check each file against these rules:

| 规则 | 通过 | 不通过 |
|------|------|--------|
| 文件在 `raw/01-articles/`、`raw/02-papers/` 或 `raw/03-transcripts/` 内 | ✅ | ❌ 直接放在 `raw/` 根目录或未知子目录 |
| 文件是 `.md` 格式 | ✅ | ❌ 非 markdown 文件 |
| 文件名不含特殊字符（如 `#`） | ✅ | ❌ 含特殊字符 |

### Step 3: Handle format issues

If any file fails validation:
1. **列出所有不合规的文件**及其问题
2. **警告用户**：这些文件不符合当前 vault 格式
3. **询问用户**是否需要帮忙重新整理（移到正确的子目录、重命名等）
4. 如果用户确认，执行整理操作

### Step 4: Ingest (only for valid files)

For each valid unprocessed file:

1. **读取** raw 文件内容
2. **在 `Wiki/sources/` 生成总结笔记**：
   - 文件名格式：`标题-YYYY-MM-DD.md`
   - 一级标题不包含日期
   - 内容模板参考 CLAUDE.md 中的 sources/ 模板
   - 末尾添加指向 raw/ 中原始素材的反向链接
3. **将 raw 文件移入 `raw/09-archive/`** 归档
4. **更新 `Wiki/log.md`** — 添加一行操作记录
5. **更新 `Wiki/index.md`** — 在 sources/ 表格中添加新条目

### 输出格式

处理完毕后，给用户一个简短摘要：

```
✅ 处理完成
- 已处理：N 篇
- 已归档：N 篇
- 跳过：N 篇（格式不符）
- 新增 Wiki 笔记：标题-1.md、标题-2.md ...
```
