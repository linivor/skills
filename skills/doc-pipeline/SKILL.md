---
name: doc-pipeline
description: 通过多步流水线从 Python 源代码生成 API 文档。当用户要求记录模块、生成 API 文档或从代码创建文档时使用。
metadata:
  pattern: pipeline
  steps: "4"
---

你现在正在执行一个标准的文档生成流水线 (Documentation Generation Pipeline)。请严格按照顺序执行以下每一步骤。**绝对不可跳过任何步骤，如果某一步失败或未获得用户确认，绝对不可进入下一步。**

## Step 1 — 解析与盘点 (Parse & Inventory)
分析用户提供的 Python 源代码，提取出所有的公共类 (public classes)、函数 (functions) 和常量 (constants)。
- 将提取出的盘点清单以 Checklists 的形式呈现给用户。
- **必须向用户提问**：“*这是您希望生成文档的完整公共 API 列表吗？如果有遗漏或不需要的部分，请告诉我。*”
- ⏸️ **等待用户确认后，再进入 Step 2。**

## Step 2 — 生成 Docstrings
针对清单中每一个缺少 docstring（文档字符串）的函数或类：
- 读取并加载 `references/docstring-style.md` 以获取规定的文档格式（如 Google Style, NumPy Style 或 Sphinx）。
- 严格按照该样式指南为目标生成 docstring。
- 将生成的 docstring 逐一或分组展示给用户以供审核。
- ⏸️ **必须明确询问用户是否满意这些 docstrings。在用户确认 (Approve) 之前，绝对不可进入 Step 3。**

## Step 3 — 组装文档 (Assemble Documentation)
- 读取并加载 `assets/api-doc-template.md` 获取最终文档的输出结构模板。
- 将之前确认的所有类、函数及其对应的 docstrings 编译、组装成一份完整的 API 参考文档草稿。

## Step 4 — 质量校验 (Quality Check)
将生成的文档草稿与 `references/quality-checklist.md` 进行对照审查，确保满足以下硬性指标：
- [ ] Step 1 中盘点的每一个公共符号都已包含在文档中。
- [ ] 每一个参数 (parameter) 都具备明确的类型声明 (type) 和描述说明 (description)。
- [ ] 每一个核心函数/类至少提供了一个实际的用法示例 (usage example)。
- 向用户报告质量校验的结果。如果发现问题，请在内部完成修复，然后向用户展示最终的完美文档。
