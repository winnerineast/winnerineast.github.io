项目核心：快速启动你的 SaaS
FireGEO 的目标是帮开发者省去繁琐的配置和搭建工作，让你专注于业务逻辑。无论是想开发一个 AI 驱动的聊天应用、品牌监控工具，还是需要用户认证和订阅计费的平台，FireGEO 提供了一站式解决方案。

• 零配置启动：通过简单的 `npm run setup` 命令，项目会自动安装依赖、测试数据库连接、生成认证表、应用数据库迁移，甚至配置计费系统
• 现代化技术栈：
  • 前端：Next.js 15.3、React 19、TypeScript 5.7，搭配 Tailwind CSS 和 shadcn/ui 组件库，界面美观且开发效率高
  • 数据库：PostgreSQL + Drizzle ORM，灵活且性能优越
  • 认证：Better Auth，提供安全的用户注册、登录和密码重置
  • 计费：集成 Stripe 和 Autumn，支持订阅管理和使用量计费
  • AI 和爬虫：支持 OpenAI、Anthropic、Google Gemini 等多种 AI 模型，以及 Firecrawl 进行网页爬取
  • 邮件：Resend 用于发送邮件通知

核心功能亮点
FireGEO 不仅仅是一个技术框架，它还内置了几个实用功能，适合打造面向用户的商业产品：

1. 用户认证系统（Better Auth）：
   • 支持邮箱/密码注册登录、会话管理和密码重置
   • 使用安全的 httpOnly cookie，确保用户数据安全
   • 提供可扩展的用户资料功能，适合个性化需求

2. 计费系统（Autumn + Stripe）：
   • 支持订阅制和使用量计费（比如按 AI 消息数量收费）
   • 提供 Stripe 客户门户，方便用户自助管理订阅
   • Webhook 集成，确保支付事件实时同步

3. AI 聊天界面：
   • 支持多种 AI 模型（OpenAI、Anthropic、Google Gemini、Perplexity），用户可自由切换
   • 提供对话历史、消息反馈、token 使用追踪等功能
   • 支持流式响应和部分模型的网页搜索功能

4. 品牌监控工具：
   • 通过 Firecrawl 进行网页爬取，分析品牌在网上的曝光度和竞争力
   • 提供 AI 驱动的品牌检测、排名评分和可定制的分析提示
   • 支持数据导出，适合市场分析或商业报告

项目适合谁？
FireGEO 特别适合以下开发者：
• 创业者：想快速验证 SaaS 产品创意，省去搭建基础架构的时间
• 全栈开发者：熟悉 Next.js 和 TypeScript，想快速构建带认证和计费的应用
• AI 应用开发者：需要集成多种 AI 模型和网页爬取功能
• 品牌管理从业者：希望开发工具来监控品牌声誉或竞争对手动态

https://github.com/mendableai/firegeo