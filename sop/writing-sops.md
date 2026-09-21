---
name: writing-sops
description: USE FOR creating or updating SOPs in the pi-sop library — format, frontmatter, MANIFEST conventions
triggers: save sop, 记录流程, write sop
last_verified: 2026-09-21
---

# Writing SOPs

本库（pi-sop）里的每个文件都是一条可复用的标准作业流程（SOP），
同时会被 pi 当作 skill 自动加载 —— 所以格式必须严格。

## File layout

- 一条 SOP = 一个文件：`sop/<name>.md`（平铺，不要子目录）
- `<name>` 用小写字母、数字、连字符（`^[a-z0-9]+(-[a-z0-9]+)*$`，≤64 字符）
- 写完必须更新 `MANIFEST.md`（`sop_save` 工具会自动做；手工编辑时用
  `/sop init` → 状态面板 → 重建 MANIFEST）

## Frontmatter (required)

```yaml
---
name: deploy-mysql-replica
description: USE FOR deploying MySQL replicas, setting up replication, GTID config
triggers: mysql replica, 主从, GTID
last_verified: 2026-09-21
---
```

| 字段 | 说明 |
|---|---|
| `name` | 与文件名一致，小写连字符 |
| `description` | **必需**，决定 pi 何时加载这条 skill。写清「什么时候用」，不要只写「是什么」 |
| `triggers` | 逗号分隔的检索关键词，中英文都写，方便 `/sop <关键词>` 命中 |
| `last_verified` | 最后一次被真实验证的日期（`YYYY-MM-DD`）。内容过期就更新它，别删 |

## Body

- 直接写可执行步骤（编号列表），不要写「我做了 X」这种叙事
- 命令要能复制粘贴，含必要的前置条件与验证方式
- 失败分支也写：出错长什么样、怎么回滚
- 只写被验证过的事实；不确定的标注「未验证」

## Rules

- 新增 SOP 自由；修改别人的 SOP 会产生一个待 review 的 commit，不要 force-push
- 所有 git 操作 best-effort：离线时只本地提交，下次会话自动补推
