# Summary: Obsidian + LLM 实战构建知识库

Source: `raw/Obsidian-LLM构建自己的知识库.md`

这篇文章聚焦于 Karpathy 的 `llm-wiki` 方法如何落地为可执行工作流。核心路径是：在本地建立一个包含 `raw/` 与 `wiki/` 的仓库，用 Obsidian 作为浏览与关系图谱入口，用 Web Clipper 快速收藏网页到 `raw/`，再由 Codex/Claude 等代理按照 skill 指令将 raw 内容编译为结构化 wiki。

文章给出了非常实操的两种命令模式：全量编译（首次构建 wiki）和增量编译（仅 ingest 新放入 raw 的资料）。其中增量命令直接对应 `Please ingest the latest materials...` / `请ingest我最新放入raw里的资料到我的wiki`，强调“持续追加、持续编译”的维护模式，而不是一次性整理完所有内容。

另一个关键点是工具链拼装：除了 Karpathy gist，还建议配合 `lewislulu/llm-wiki-skill` 这类 skill 模板；同时使用 Obsidian ecosystem（如 clipper、图谱视图）提升收集和阅读效率。文章的价值不在理论解释，而在把「可持续知识管理」拆成了低门槛动作：收集 -> 放入 raw -> 执行 ingest -> 在 wiki 中检索与复用。
