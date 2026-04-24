# Summary: LLM Wiki Pattern

Source: [Karpathy LLM Wiki gist](https://gist.githubusercontent.com/karpathy/442a6bf555914893e9891c11519de94f/raw/llm-wiki.md)

The LLM Wiki pattern proposes replacing query-time-only RAG with a persistent knowledge artifact: an LLM-maintained markdown wiki that is continuously updated as sources are ingested. Instead of re-synthesizing from raw files each time, the system compiles understanding into structured pages (concepts, entities, summaries, comparisons), preserving cross-links and contradictions over time.

The architecture has three layers: immutable raw sources, writable wiki pages, and a schema/config file that governs workflows and conventions. Operationally, the system cycles through ingest, query, and lint. Ingest reads a source and updates many pages; query synthesizes answers from existing wiki pages and can promote good outputs back into the wiki; lint checks for structural and content health issues such as stale claims, weak linking, and missing pages.

The pattern uses `index.md` as a content catalog and `log.md` as a chronological operation record. Together they enable efficient navigation and continuity across sessions without requiring heavyweight infrastructure at small-to-medium scale. The key claim is that LLMs eliminate the maintenance burden that makes human-maintained wikis decay, while humans stay responsible for curation, judgment, and direction.
