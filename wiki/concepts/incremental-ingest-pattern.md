# Incremental Ingest Pattern

增量 ingest 的核心原则：新资料只需要放进 `raw/`，然后执行一次 ingest 操作，让代理只更新受影响的 summary、concept、entity 和索引，而不是重建全部 wiki。

推荐节奏：
- 首次全量编译建立骨架；
- 日常以“新增一批 raw -> ingest 一次”为主；
- 周期性运行结构清理和链接检查（compile/lint）。

这种模式能在保证 wiki 连续性的同时，显著降低维护阻力，适合长期知识累积。

相关页面：[[concepts/obsidian-llm-workflow]], [[summaries/obsidian-llm-build-personal-kb]]
