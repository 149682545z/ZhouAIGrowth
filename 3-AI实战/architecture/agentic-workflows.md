# Agentic Workflows (构建智能体)

未来的 AI不仅仅是 Chatbot，而是 Agent（智能体）。如果说 Chatbot 是“大脑”，那 Agent 就是“大脑 + 手脚 + 工具”。

## 什么是 Agent？
**Agent = LLM + Planning + Memory + Tools**
- **LLM**：核心大脑，负责决策。
- **Planning**：任务拆解（如 CoT, ReAct）。
- **Memory**：记住用户的偏好和历史操作。
- **Tools**：联网搜索、读写文件、执行代码。

## 常见设计模式

### 1. ReAct (Reason + Act)
最经典的模式。
- **思考 (Reason)**：我现在需要查天气。
- **行动 (Act)**：调用天气 API。
- **观察 (Observation)**：API 返回北京 25度。
- **思考 (Reason)**：用户问是否需要带伞，25度晴天不需要。
- **回答 (Response)**：不需要带伞。

### 2. Multi-Agent (多智能体协作)
让多个专职 Agent 互相吵架、合作。
- **Manager Agent**：负责分派任务。
- **Coder Agent**：负责写代码。
- **Reviewer Agent**：负责检查代码，不通过就打回给 Coder。
- **优势**：各司其职，比全能型单体更稳定。

### 3. Reflection (反思)
Agent 执行完任务后，自己检查一遍：“我做得对吗？哪里可以改进？”。然后自我修正。
- **应用**：能极大提升代码生成的质量（例如 AlphaCode 的思路）。

## 常用框架
- **LangChain / LangGraph**：工业界标准，功能最全。
- **AutoGPT / BabyAGI**：早期的自主 Agent 探索。
- **CrewAI**：专注于多智能体角色扮演。
