# Obsidian + LLM Workflow

该工作流把知识库维护拆成四个稳定环节：

1. 收集：通过 Web Clipper 把网页快速保存到 `raw/`。
2. 编译：让 LLM 依据 wiki skill 将 raw 内容转为 `wiki/` 下的结构化页面。
3. 导航：在 Obsidian 中通过链接和图谱浏览知识关系。
4. 迭代：新资料进入 raw 后持续执行 ingest，而非重做全量整理。

该模式的优势是降低整理成本：人专注于“选材料和提问题”，代理负责“归档、关联、维护”。

相关页面：[[concepts/incremental-ingest-pattern]], [[entities/Obsidian]], [[entities/Obsidian Web Clipper]]
