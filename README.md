<!-- <div align="center">

# 📡 AI Daily Digest

**每天 5 分钟，掌握 AI 领域最值得关注的动态。**

全自动采集 · AI 智能筛选与总结 · 重要性评分 · 每日定时发布

[![Daily Digest](https://github.com/Jimmuji/ai-daily-digest/actions/workflows/daily.yml/badge.svg)](https://github.com/Jimmuji/ai-daily-digest/actions/workflows/daily.yml)
![GitHub last commit](https://img.shields.io/github/last-commit/Jimmuji/ai-daily-digest)
![GitHub stars](https://img.shields.io/github/stars/Jimmuji/ai-daily-digest?style=social)

[**📖 查看最新日报**](daily/) · [**⚙️ 快速部署**](#-快速开始) · [**💡 设计理念**](#-为什么做这个)

</div>

---

## 🤔 为什么做这个

AI 领域每天产出大量信息——新论文、新模型、新产品、新融资，散落在 HuggingFace、GitHub、TechCrunch、36Kr 等几十个平台上。

**问题是**：手动逐个刷太耗时间，全靠 AI 自动筛又不放心。

**AI Daily Digest** 的做法是：
> 脚本负责从多个源抓取原始数据，AI 负责筛选去重 + 生成结构化摘要。全程零人工干预，每天自动跑，结果直接存到 GitHub 仓库里。

---

## ✨ 它能做什么

```
📥 数据采集（免费 API / RSS）
 │
 ├── 📄 HuggingFace Daily Papers     ← 每日热门 AI 论文
 ├── 🔧 GitHub Trending (OSSInsight)  ← 热门 AI 开源项目
 ├── 📰 36Kr AI / SSPAI              ← 中文 AI 新闻
 └── 📰 TechCrunch / The Verge       ← 英文 AI 新闻
 │
 ▼
🧠 AI 智能处理（DeepSeek）
 │
 ├── 从 ~60 条原始资讯中筛选 10-15 条精华
 ├── 去重、按类别分组（新闻 / 论文 / 开源项目）
 ├── 每条 2-3 句话总结，保留关键信息和原文链接
 ├── 给每条资讯标注重要性：★☆☆☆☆ - ★★★★★
 └── 生成 "今日观察" 趋势点评
 │
 ▼
📤 自动发布
 │
 ├── 生成 Markdown → 存入 daily/ 目录
 └── 保存原始数据 JSON → 存入 data/ 目录，方便追踪来源
```

---

## 📋 日报示例

> 以下为 [2026-04-14 日报](daily/2026-04-14.md) 的部分摘录：

### 📰 行业新闻
1. **OpenAI 收购个人理财初创公司 Hiro**：OpenAI 正将财务规划能力整合进 ChatGPT 中，拓展其应用边界。
   - 重要性：★★★★☆ / 5
   - 为什么重要：这代表通用 AI 助手正在进入高价值垂直场景。
   - 来源：[TechCrunch AI](https://techcrunch.com/category/artificial-intelligence/)
2. **微软测试类 OpenClaw 的自主 AI 助手**：微软正研究将自主运行功能集成到 Copilot 中，旨在让其能为企业用户全天候自动完成任务...

### 📄 重要论文
1. **SPEED-Bench：投机解码的统一多样化基准**：投机解码是加速大模型推理的关键技术，该研究提出了支持吞吐量评估的新基准...

### 🔧 开源项目
1. **Hermes Agent 发布 0.9.0**：支持原生微信 Callback 功能，使智能体能够更好地与微信生态集成...

### 💡 今日观察
> 今日资讯呈现出 AI 领域"落地加速"与"生态分化"并行的鲜明特点...

---

## 🚀 快速开始

只需 3 步，Fork 后就能跑：

### 1. Fork 本仓库

点击右上角 **Fork** 按钮。

### 2. 配置 API Key

进入你 Fork 的仓库 → **Settings** → **Secrets and variables** → **Actions** → **New repository secret**：

| Secret 名称 | 值 | 说明 |
|-------------|-----|------|
| `API_KEY` | 你的 API Key | 默认使用 [DeepSeek](https://platform.deepseek.com/)（中文友好） |

> 💡 也支持 OpenAI 或任何兼容 API。可以在 **Settings → Secrets and variables → Actions → Variables** 里设置 `API_BASE_URL` 和 `API_MODEL`。

### 3. 启用 GitHub Actions

进入 **Actions** 标签页 → 点击 **I understand my workflows, go ahead and enable them**。

搞定！每天北京时间 **08:00** 会自动运行。也可以点击 **Run workflow** 手动触发。

---

## 🏗️ 项目结构

```
ai-daily-digest/
├── .github/workflows/
│   └── daily.yml            # GitHub Actions 定时任务
├── scripts/
│   ├── main.py              # 入口：采集 → 总结 → 保存
│   ├── sources.py           # 数据源：HuggingFace / GitHub / RSS
│   └── summarize.py         # AI 总结：调用 DeepSeek API
├── daily/                   # 📰 每日生成的日报（Markdown）
│   ├── 2026-04-14.md
│   └── ...
├── data/                    # 🔎 每日原始素材（JSON，便于追踪和调试）
│   ├── 2026-04-14.raw.json
│   └── ...
├── requirements.txt
└── README.md
```

---

## 🔧 自定义配置

### 更换 AI 模型

在 workflow 的环境变量中设置：

```yaml
env:
  API_KEY: ${{ secrets.API_KEY }}
  API_BASE_URL: ${{ vars.API_BASE_URL || 'https://api.deepseek.com' }}
  API_MODEL: ${{ vars.API_MODEL || 'deepseek-chat' }}
```

例如使用 OpenAI 时，把仓库变量 `API_BASE_URL` 设为 `https://api.openai.com/v1`，`API_MODEL` 设为 `gpt-4o-mini` 或其他可用模型。

### 重要性评分

脚本会先根据来源类别、关键词和大公司/高影响信号给每条素材一个 `importance_hint`。AI 生成日报时会结合原始内容重新判断，并在每条资讯下输出：

```markdown
- 重要性：★★★★☆ / 5
- 为什么重要：说明对开发者、产品、研究或产业的影响。
- 来源：[Source Name](URL)
```

### 添加数据源

编辑 `scripts/sources.py`，在 `RSS_SOURCES` 列表中添加新的 RSS 源：

```python
RSS_SOURCES = [
    ("https://rsshub.rssforever.com/36kr/search/articles/ai", "36Kr AI"),
    ("https://your-new-source.com/rss", "New Source"),  # ← 加这里
]
```

### 修改发布时间

编辑 `.github/workflows/daily.yml` 中的 cron 表达式：

```yaml
schedule:
  - cron: '0 0 * * *'   # UTC 00:00 = 北京时间 08:00
  - cron: '0 12 * * *'  # 加一行 = 每天跑两次
```

---

## 🗺️ Roadmap

- [x] 核心 pipeline：数据采集 → AI 总结 → 自动发布
- [x] 每条资讯保留来源链接
- [x] 重要性评分 / 标星
- [x] 保存原始抓取数据 JSON
- [ ] GitHub Pages 静态站点
- [ ] RSS 输出
- [ ] 趋势追踪（"本周 Agent 相关新闻出现 12 次"）
- [ ] 邮件 / Telegram 推送
- [ ] 更多数据源（Reddit、Hacker News、ArXiv）
- [ ] 每周回顾报告

---

## 🤝 Contributing

欢迎贡献！无论是新增数据源、优化 Prompt、改进输出格式，还是修 Bug，都非常感谢。

1. Fork 本仓库
2. 创建你的分支：`git checkout -b feature/xxx`
3. 提交更改：`git commit -m 'Add xxx'`
4. 推送到远程：`git push origin feature/xxx`
5. 提交 Pull Request

---

## 📄 License

MIT License - 随便用，注明出处即可。

---

<div align="center">

**如果觉得有用，欢迎 ⭐ Star 支持一下！**

</div> -->


下面是对融合优化后的 **AI Daily Digest Agent** 的完整技术说明，包括它的设计思路、核心模块、工作流程和部署方式。你可以把它当作一份系统文档，方便理解和维护。

---

## 🧠 系统概述

**AI Daily Digest** 是一个**全自动、零成本（免费）的 AI 行业日报生成系统**。它每天定时从 90+ 个高价值信息源（技术博客、学术论文、开源项目）抓取最新内容，利用大语言模型（默认 Google Gemini，也支持 DeepSeek）进行摘要、筛选和评分，最终输出一份结构化的中文 Markdown 日报。

所有代码托管在 GitHub 上，由 **GitHub Actions** 驱动，不需要你自己的服务器或定时任务。你只需要 Fork 项目、配置一条免费的 API Key，之后每天打开仓库就能看到最新日报。

---

## 🏗️ 架构设计

系统由四个核心层组成：

| 层级           | 作用                           | 关键技术                     |
|----------------|--------------------------------|------------------------------|
| **数据获取层** | 并行抓取 RSS、API              | Python `feedparser`, `requests` |
| **AI 总结层**  | 生成高质量中文日报             | Gemini API / DeepSeek API      |
| **调度与存储** | 定时触发、持久化结果           | GitHub Actions, Git 仓库       |
| **配置与安全** | 管理 API Key 和可选项          | GitHub Secrets, 环境变量        |

**数据流示意图：**
```
[GitHub Actions 定时/手动触发]
            |
            v
   [scripts/main.py 入口]
            |
    +-------+-------+
    |               |
    v               v
[HuggingFace]  [RSS + GitHub Trending]
    |               |
    +-------+-------+
            |
            v
    [原始数据去重 → data/日期.raw.json]
            |
            v
    [AI 总结 (Gemini/DeepSeek)]
            |
            v
    [日报 Markdown → daily/日期.md]
            |
            v
    [Commit & Push 回仓库]
```

---

## 📁 项目结构

```
ai-daily-digest/
├── .github/
│   └── workflows/
│       └── daily.yml          # GitHub Actions 工作流定义
├── scripts/
│   ├── main.py                # 主流程入口
│   ├── sources.py             # 所有数据源抓取逻辑（含90+RSS源）
│   └── summarize.py           # AI 总结模块（支持多后端）
├── requirements.txt           # Python 依赖
├── data/                      # 原始数据存档（自动生成）
│   └── YYYY-MM-DD.raw.json
└── daily/                     # 生成的日报（自动生成）
    └── YYYY-MM-DD.md
```

---

## ⚙️ 核心模块详解

### 1. 数据源 (`scripts/sources.py`)

该模块负责抓取**三类内容**，所有函数返回标准化字典。

- **HuggingFace 每日论文**  
  直接调用 HuggingFace 非官方 API（`https://huggingface.co/papers` 的 JSON 接口），获取当天最热门论文，解析标题、摘要、链接。

- **GitHub Trending 项目**  
  解析 `https://github.com/trending?since=daily` 页面，提取 AI 相关仓库的名称、描述、Star 数、链接。

- **RSS 订阅源（融合后的 90+ 源）**  
  基于 `vigorX777` 项目整理的 Andrej Karpathy 推荐的高质量科技博客，并结合了 `Jimmuji` 原有的中文源。它使用 `feedparser` 解析每个 RSS/Atom 源，并内置去重和低信号过滤逻辑。

  关键代码片段：
  ```python
  RSS_SOURCES = [
      # Karpathy 推荐的顶级技术博客
      ("https://simonwillison.net/atom/everything/", "simonwillison.net"),
      ("https://www.jeffgeerling.com/blog.xml", "jeffgeerling.com"),
      # ... 共90+ 源
  ]
  ```

  抓取时还会进行：
  - 重要性初始评分（根据来源权威性、关键词匹配）
  - 文章去重（URL 或标题标准化）
  - 中文内容优先保留

### 2. AI 总结模块 (`scripts/summarize.py`)

这是日报质量的核心。它接收原始数据，调用大语言模型生成结构化日报。

#### 提示词设计 (SYSTEM_PROMPT)

系统提示词明确要求 AI 扮演资深 AI 编辑，完成以下任务：
- 筛选最有价值的 10-15 条资讯
- 分为**行业新闻 / 重要论文 / 开源项目**三组
- 每条附带 **★ 重要性评分** 和 **“为什么重要”** 的点评
- 保留原文链接
- 最后写一段 **“今日观察”** 洞察
- 严格基于提供素材，不编造

#### 多后端支持

通过环境变量 `AI_PROVIDER` 切换，目前实现：
- **`gemini`**（推荐，免费）  
  直接调用 Gemini REST API，无需额外 SDK。模型默认为 `gemini-2.0-flash`，速度快且日常够用。
- **`deepseek`**（备用）  
  兼容 OpenAI 接口规范，可使用任何 DeepSeek 模型。

代码中抽象了 `summarize_with_gemini` 和 `summarize_with_deepseek` 函数，主函数根据 `provider` 分发。

### 3. 主流程 (`scripts/main.py`)

协调各模块运行：
1. 获取命令行参数（省份、日期？实际使用当前时间）
2. 调用 `sources.py` 抓取全部数据
3. 保存原始 JSON 到 `data/` 目录（便于追溯）
4. 调用 `summarize.py` 生成 Markdown 日报
5. 写入 `daily/` 目录，文件名为当天日期

### 4. 自动化调度 (`.github/workflows/daily.yml`)

```yaml
name: AI Daily Digest
on:
  schedule:
    - cron: '0 2 * * *'        # UTC 2:00，即北京时间 10:00
  workflow_dispatch:             # 允许手动触发
```

作业步骤：
- 检出代码
- 安装 Python 3.12 及依赖
- 以环境变量注入 `API_KEY`、`AI_PROVIDER` 等
- 执行 `cd scripts && python main.py`
- 将生成的 `data/` 和 `daily/` 提交回仓库

每次运行都会在仓库产生一个新提交，实现“每日推送”。

---

## 🚀 部署与使用（在 VS Code Insider 中）

**前提**：
- 拥有 GitHub 账号
- 本地装有 VS Code Insider 和 Git
- 有一个免费的 Gemini API Key（从 [Google AI Studio](https://aistudio.google.com/apikey) 获取）

### 步骤 1：获取项目代码

1. 在浏览器中 Fork 某个已集成的仓库（如你优化过的），或者直接创建一个新仓库并用上面的文件结构初始化。
2. 打开 VS Code Insider，通过 `Ctrl+Shift+P` → `Git: Clone`，克隆你的仓库到本地。

### 步骤 2：配置 API Key

1. 在 GitHub 网页打开你的仓库 → Settings → Secrets and variables → Actions。
2. 新建一个 Secret，名称 **`API_KEY`**，值粘贴你的 Gemini API Key。
3. 无需其他配置（工作流中已默认使用 `gemini` 提供商）。

### 步骤 3：手动测试运行

1. 在仓库页点击 Actions → AI Daily Digest → Run workflow。
2. 等待约 2 分钟，刷新仓库根目录，将会出现 `daily/2026-04-26.md` 文件。
3. 你可以在 VS Code 中 `Ctrl+Shift+E` 查看文件内容，也可以直接在 GitHub 网页阅读。

### 步骤 4：每天自动生成

定时器已设置好，之后无需任何操作。每天北京时间上午 10 点左右，日报就会自动出现在仓库中。

---

## 🔧 自定义与扩展

### 想调整信息源？
编辑 `scripts/sources.py` 中的 `RSS_SOURCES` 列表，注释或增加你喜欢的源（RSS 链接 + 显示名称）。增加后推送即可生效。

### 想切换 AI 模型？
修改 `.github/workflows/daily.yml` 中 `env` 部分：
```yaml
AI_PROVIDER: deepseek          # 改为 deepseek
API_MODEL: deepseek-chat       # 可换成 deepseek-reasoner 等
```
同时确保 Secrets 中的 `API_KEY` 是你对应 DeepSeek 的有效 Key。

### 想改变推送时间？
修改 `.github/workflows/daily.yml` 的 `cron` 表达式。注意 GitHub Actions 的 cron 使用 UTC 时间，`0 2 * * *` 对应北京时间 10:00（非夏令时）。

### 想增加邮件推送？
可在工作流末尾添加一个 `send-email` 步骤，使用 `dawidd6/action-send-mail` 等 Action，将 `daily/` 下的最新文件作为邮件正文发送。

---

## 🧪 常见问题排故

| 现象 | 可能原因 | 解决 |
|------|----------|------|
| 工作流报 401/402 | API Key 无效或欠费 | 检查 Secret 名称是否正确（`API_KEY`），值是否完整；如用 DeepSeek 需充值，建议切回免费 Gemini |
| 抓取不到新内容 | RSS 源失效或被墙 | 部分国外源可能需要代理，可替换为其他可访问源 |
| 未生成 daily 文件夹 | 工作流执行但未推送 | 检查 Actions 权限是否开启读写（Settings → Actions → General → Read and write permissions） |
| 日报内容过长或过短 | AI 总结策略问题 | 可在 `summarize.py` 中调整 `max_tokens` 或提示词中的条目数要求 |

---

## 📌 总结

你亲手构建的这套 **AI Daily Digest Agent**，已经是一套非常健壮且高效的自动化情报系统。它兼具 **最全的信息源**（Karpathy 推荐 + 论文 + 开源项目）和 **零成本的 AI 总结能力**，并且完全托管在 GitHub，无需维护成本。

如果你将来想把它移植到其他平台（如企业微信、Slack）或增强功能，这套模块化的架构也很容易扩展。现在，你完全可以每天花 3 分钟扫一眼日报，就能把握 AI 领域的脉搏了。