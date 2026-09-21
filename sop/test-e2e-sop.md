---
name: test-e2e-sop
description: USE FOR verifying pi-sop end-to-end save flow
triggers: e2e, 测试
last_verified: 2025-07-15
---

# pi-sop 端到端保存流程验证

本文档记录对 pi-sop 库执行的端到端（e2e）验证步骤，用于确认 SOP 保存链路在全新环境中可正常工作。

## 前置条件

- 可访问 pi-sop 共享库所在目录
- 拥有 git 与基本 shell 工具

## 验证步骤

1. **克隆空仓库**
   - 准备一个空的 git 仓库（或克隆已清空内容的 pi-sop 仓库）：
     ```bash
     git clone <empty-repo-url> /tmp/e2e-sop-test
     cd /tmp/e2e-sop-test
     ```
   - 确认仓库为空：`ls -la` 应只看到 `.git`。

2. **脚手架初始化（scaffold）**
   - 在空仓库中初始化 SOP 库结构：创建 `sop/` 目录及约定文件（如 `writing-sops.md`、`MANIFEST` 等）。
   - 确认目录结构符合 pi-sop 库约定：
     ```bash
     ls /tmp/e2e-sop-test/sop/
     ```

3. **保存 SOP（save）**
   - 通过 `sop_save` 工具保存一个测试 SOP：
     - name: `test-e2e-sop`
     - description: 明确的 USE FOR 描述
     - triggers: 逗号分隔的中英文关键词
     - content: Markdown 正文，含具体编号步骤
   - 保存后验证文件已落盘、MANIFEST/索引已更新（如有）。

4. **验收**
   - 确认保存操作返回成功结果。
   - 在新会话/新机器上确认该 SOP 可被发现与自动加载。

## 失败分支

- 若 scaffold 失败：检查目录权限与 git 状态。
- 若 save 后文件未落盘：检查库路径解析（是否指向克隆出的仓库而非默认路径）。
- 同名再次保存视为更新，不应产生重复条目。

## 结论

克隆空仓库 → 脚手架初始化 → sop_save 保存，全链路通过即视为 e2e 验证成功。
