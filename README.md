# Agent Web Access Surfaces

一张图解释：Agent 访问网站时，到底是在读什么、操作哪里，以及为什么不同方案的效率、稳定性和适配性差别很大。

在线页面：https://dxxbb.github.io/agent-web-access-surfaces/

## 核心观点

“让 Agent 访问网站”不是一个技术方案，而是一组读写技术面的选择。

越靠近结构化接口，速度越快、成本越低、可测试性越强；越靠近真实屏幕，覆盖越广、适配性越强，但延迟、脆弱性和安全风险都会上升。

## 六个技术面

1. **公开 API**：官方承诺的结构化接口，例如 X API、GitHub API。
2. **前端内部接口**：网页前端自己调用的 JSON / GraphQL / private endpoint。
3. **HTML 文档**：服务器返回的初始文档，适合文档站和静态内容抽取。
4. **浏览器运行时**：JavaScript 执行后的 DOM、Accessibility Tree、network、screenshot。
5. **浏览器动作通道**：通过 Playwright、Stagehand、browser-use、Skyvern 等控制浏览器点击、输入、滚动。
6. **桌面动作通道**：通过 Computer Use / RPA 操作真实屏幕、鼠标、键盘和跨应用流程。

## 适合讨论的问题

- 为什么 Playwright 很强，但大模型厂商还要做 Computer Use？
- API、HTTP endpoint、HTML、DOM、screenshot、Computer Use 的本质区别是什么？
- OpenCLI、Stagehand、browser-use、Skyvern、Browserbase、Firecrawl 分别应该放在哪一层？
- 什么时候应该从浏览器探索下沉成接口 adapter？
- 做数据获取、账号态操作、复杂网页工作流、桌面应用自动化时，应该怎么选型？
- Claude app、Codex app、Gemini app、Antigravity 这类产品外壳分别调用了谱系里的哪一层能力？

## 快速结论

- 长期稳定的数据获取：优先 `公开 API -> 前端内部接口 adapter`。
- 文档站和知识库抽取：优先 `HTML/Markdown extraction`，例如 Firecrawl、Crawl4AI。
- 登录态强、交互复杂的网站：先用浏览器运行时和 Local Chrome Bridge 侦察，再用 Playwright/OpenCLI/adapter 固化。
- 高变化、低频、跨应用、无 DOM 的任务：才上 Computer Use / RPA。
- 不要把多轮 LLM 点击当成长期生产数据管道。它适合探索和兜底，不适合高吞吐采集。
- App 不是技术层。浏览器动作通道要分清两层：底层机制是 Playwright / CDP / extension / AX / screenshot；Codex browser use、Claude in Chrome、Gemini Agent、Antigravity 是产品能力。Gemini 这里讨论主流产品，不再把 Project Mariner 放主图。

## Files

- `index.html`：主页面。
- `assets/agent-website-access-surfaces.png`：生成的概念图备份。

## References

- [OpenCLI](https://opencli.info/docs/guide/getting-started.html)
- [Stagehand](https://www.browserbase.com/stagehand/)
- [browser-use](https://github.com/browser-use/browser-use)
- [Skyvern](https://github.com/Skyvern-AI/skyvern)
- [Playwright](https://github.com/microsoft/playwright)
- [Firecrawl](https://docs.firecrawl.dev/)
- [Crawl4AI](https://docs.crawl4ai.com/)
- [Codex app](https://openai.com/codex/)
- [Codex for almost everything](https://openai.com/index/codex-for-almost-everything/)
- [OpenAI Computer Use](https://platform.openai.com/docs/guides/tools-computer-use)
- [Claude Computer Use](https://docs.anthropic.com/en/docs/agents-and-tools/tool-use/computer-use-tool)
- [Claude in Chrome](https://support.claude.com/en/articles/12012173-getting-started-with-claude-for-chrome)
- [Gemini Agent](https://gemini.google/overview/agent/)
- [Google Antigravity](https://www.antigravity.google/)
- [Gemini Computer Use model](https://blog.google/innovation-and-ai/models-and-research/google-deepmind/gemini-computer-use-model/)
