# 检索增强生成 (RAG) 设计模式

RAG (Retrieval-Augmented Generation) 是解决 LLM “幻觉”和“知识过时”问题的核心架构。

## 什么是 RAG？
简单来说，就是“开卷考试”。
1. **检索 (Retrieval)**：先去知识库里找相关资料。
2. **增强 (Augmented)**：把资料和你的问题一起喂给 AI。
3. **生成 (Generation)**：AI 参考资料回答问题。

## 1. 基础 RAG (Naive RAG)
- **流程**：文档 -> 切片 (Chunking) -> 向量化 (Embedding) -> 向量数据库 -> 相似度搜索 -> LLM。
- **痛点**：检索不准（关键词匹配但语义无关）、切片割裂语义。

## 2. 进阶 RAG (Advanced RAG)

### A. 混合检索 (Hybrid Search)
同时使用**向量检索**（语义匹配）和**关键词检索** (BM25)。
- **优势**：既能懂“苹果”是水果（语义），也能精准匹配产品型号“iPhone 15 Pro Max”（关键词）。

### B. 重排序 (Re-ranking)
初步检索出 Top 50 个结果，然后用一个更精细的模型（Re-ranker）对它们的相关性打分，只取 Top 5 给 LLM。
- **效果**：大幅提升准确率，是 RAG 系统的“神之一手”。

### C. 上下文压缩 (Context Compression)
检索回来的文档可能很长，只提取其中与问题相关的段落，减少 Token 消耗，避免噪声。

## 3. 模块化 RAG (Modular RAG)
将 RAG 拆分为独立的模块，如 Search, Memory, Routing 等，根据任务动态组合。
- **Routing**：判断问题是简单的（直接用模型知识），还是复杂的（需要调用搜索工具）。
