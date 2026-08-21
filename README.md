# Agent Web Access Surfaces

一张图解释：Agent 使用网站时接触的到底是哪一面、谁在决定下一步、使用哪种登录状态，以及怎样验证业务结果。

在线页面：https://dxxbb.github.io/agent-web-access-surfaces/

## 核心观点

“让 Agent 访问网站”不是一个技术方案，而是四个独立问题：

1. 接触哪个环境：服务端、浏览器还是整个桌面？
2. 通过什么接口观察和动作：API、文档、DOM/AX/Network、截图、鼠标键盘？
3. 谁决定下一步：脚本/状态机、模型辅助，还是 Agent loop？
4. 使用哪个 Session，最后怎样独立验证结果？

越靠近结构化接口，语义密度通常越高、运行闭环越短、吞吐越高；越靠近像素和真实桌面，覆盖越广、接入越快，但每次运行的观察—决策—动作—验证闭环通常更长。向右不是“能力更高级”，而是在用运行成本换覆盖。

## 六个技术面

1. **业务 API**：对象、字段、Schema、错误码与 CRUD/RPC。
2. **HTTP / 内部接口**：HTML、JSON、GraphQL、RSS、网站前端使用的 endpoint。
3. **文档与内容**：正文、链接、PDF、Markdown、表格与 metadata。
4. **浏览器结构**：DOM、Accessibility Tree、Network、Runtime、元素状态与 Locator。
5. **浏览器像素与动作**：Screenshot、布局、Locator/坐标、输入、滚动和上传。
6. **桌面与跨应用**：Window、系统 Accessibility、屏幕、鼠标、键盘和应用切换。

这六列是“接触面/技术路线”，不是严格协议分层，也不是能力等级。Browser Agent 通常是“模型控制器 + 浏览器自动化工具 + Session + Verify”的组合，不是第七个浏览器技术层。

## 适合讨论的问题

- 为什么 Playwright 很强，但大模型厂商还要做 Computer Use？
- API、HTTP endpoint、HTML、DOM、screenshot、Computer Use 的本质区别是什么？
- OpenCLI、Stagehand、browser-use、Skyvern、Browserbase、Firecrawl 为什么会横跨多层？
- 什么时候应该从浏览器探索下沉成接口 adapter？
- 做数据获取、账号态操作、复杂网页工作流、桌面应用自动化时，应该怎么选型？
- Claude、Codex 这类产品入口在一次任务中究竟调用了哪种观察与动作工具？

## 快速结论

- 明确业务对象：优先 API / Connector / CLI。
- 公开信息调研：Search → Fetch 原文 → 必要时 Browser。
- 稳定网页交互：优先 Playwright / Selenium / Puppeteer 等结构化浏览器控制。
- 开放任务、路径难预枚举：在浏览器底座上增加模型辅助或 Browser Agent。
- Canvas、远程桌面、原生 App、跨应用：使用 Computer Use / RPA，并加强审批与独立验证。
- 不要把多轮 LLM 点击当成高吞吐生产数据管道。

## 代表方案怎样定位

- **Playwright / Selenium / Puppeteer**：浏览器控制框架，可被脚本、模型辅助或 Agent 控制器调用。
- **Browserbase / Steel / Browserless**：浏览器 Session 与运行基础设施，不与 Playwright 并列为控制框架。
- **Stagehand / browser-use / Skyvern**：把模型决策与浏览器工具组合起来的 Agent/智能控制层。
- **Firecrawl / Crawl4AI**：以内容读取和解析为主，也可以启动浏览器渲染动态页面。
- **OpenCLI**：跨层 adapter 与统一命令面，实际可走 PUBLIC、COOKIE、INTERCEPT、UI、LOCAL 或外部 CLI。
- **Codex / Claude**：产品入口，可横跨 Search、HTTP/API、MCP、Browser、Chrome 和 Computer Use。仅凭产品名或页面可见性不能判断本次底层路径；要看工具 trace。
- **OpenAI / Claude Computer Use**：可运行在浏览器或桌面 GUI；视觉是常见方式，也可以混合 DOM、AX、Locator 与程序化动作。

执行器发出了动作不等于业务目标已经完成。可靠系统需要用业务对象、接收方状态或其他独立信号 Verify。

## Files

- `index.html`：主页面。
- `assets/agent-website-access-surfaces.png`：桌面主图。
- `assets/twitter-card.jpg`：社交分享图。

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
