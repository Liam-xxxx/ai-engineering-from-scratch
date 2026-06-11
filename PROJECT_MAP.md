# ai-engineering-from-scratch 目录结构指南

MIT 开源 AI 工程课程，共 503 节课、20 个阶段、约 320 小时。覆盖从线性代数到自主 Agent Swarm。
网站: https://aiengineeringfromscratch.com

---

## 顶层文件

| 文件 | 用途 |
|------|------|
| `README.md` | 项目入口，含完整课程大纲（20 个阶段 + 链接）、学习理念、Artifact 目录 |
| `ROADMAP.md` | 每个阶段/课程的状态追踪（✅/🚧/📋），驱动网站构建 |
| `AGENTS.md` | 贡献者和 AI Agent 的操作手册：仓库规范、课程契约、CI 门禁等 |
| `LESSON_TEMPLATE.md` | 新建课程的标准蓝图（文件结构、frontmatter 格式、章节规范） |
| `CONTRIBUTING.md` | 贡献指南 |
| `FORKING.md` | Fork 指南（团队内训、大学课程、Bootcamp 等场景） |
| `CHANGELOG.md` | 更新日志 |
| `SPONSORS.md` | 赞助页面与费率 |
| `requirements.txt` | 课程依赖（numpy、torch、transformers、anthropic 等） |
| `vercel.json` | Vercel 部署配置 |

---

## 顶层目录

### `phases/` — 课程核心

20 个阶段目录（`00` 到 `19`），每节课含 `docs/en.md`（课程正文）、`code/`（代码）、`outputs/`（产物：prompt/skill/agent）和 `quiz.json`（6 题测验）。

| 目录 | 阶段名 | 课时 |
|------|--------|------|
| `00-setup-and-tooling` | 环境搭建与工具链 | 12 |
| `01-math-foundations` | 数学基础 | 22 |
| `02-ml-fundamentals` | 机器学习基础 | 18 |
| `03-deep-learning-core` | 深度学习核心 | 13 |
| `04-computer-vision` | 计算机视觉 | 28 |
| `05-nlp-foundations-to-advanced` | NLP 基础到进阶 | 29 |
| `06-speech-and-audio` | 语音与音频 | 17 |
| `07-transformers-deep-dive` | Transformers 深度剖析 | 16 |
| `08-generative-ai` | 生成式 AI | 15 |
| `09-reinforcement-learning` | 强化学习 | 12 |
| `10-llms-from-scratch` | 从零构建 LLM | 24 |
| `11-llm-engineering` | LLM 工程 | 17 |
| `12-multimodal-ai` | 多模态 AI | 25 |
| `13-tools-and-protocols` | 工具与协议 | 23 |
| `14-agent-engineering` | Agent 工程 | 42 |
| `15-autonomous-systems` | 自主系统 | 22 |
| `16-multi-agent-and-swarms` | 多 Agent 与 Swarm | 25 |
| `17-infrastructure-and-production` | 基础设施与生产 | 28 |
| `18-ethics-safety-alignment` | 伦理、安全与对齐 | 30 |
| `19-capstone-projects` | 综合项目 | 85 |

### `scripts/` — 自动化工具

| 脚本 | 用途 |
|------|------|
| `audit_lessons.py` | 对所有课程目录做结构完整性校验（CI 阻塞门禁） |
| `build_catalog.py` | 遍历课程生成 `catalog.json` 机器可读索引 |
| `check_readme_counts.py` | 检查 README 中的硬编码数字是否与实际一致，支持 `--fix` |
| `install_skills.py` | 将所有课程的产物（skill/prompt/agent）安装到目标目录 |
| `lesson_run.py` | 冒烟检查每个课程的 Python 代码（语法编译，可选执行） |
| `link_check.py` | 校验所有 markdown 文档中的外部链接 |
| `scaffold-lesson.sh` | 脚手架脚本：快速生成新课程序目录和模板 |
| `scaffold_workbench.py` | 安装 "Agent Workbench" 到目标仓库 |
| `_lib.py` | 其他脚本的共享库 |

### `glossary/` — AI 术语参考

| 文件 | 用途 |
|------|------|
| `terms.md` | 60+ 个 AI 术语定义（"大家怎么说" vs "实际含义" vs "为什么这么叫"） |
| `myths.md` | 20 个常见 AI 误区辟谣 |

### `site/` — 静态网站

部署在 aiengineeringfromscratch.com（Vercel）。

| 文件 | 用途 |
|------|------|
| `build.js` | 构建脚本：解析 README + ROADMAP + glossary → 生成 `data.js` |
| `data.js` | 生成文件（666 KB），整个课程的结构化数据，CI 自动重建，**不要手动编辑** |
| `index.html` / `lesson.html` / `catalog.html` 等 | 各页面 HTML |
| `app.js` / `cmdpalette.js` / `header.js` / `progress.js` | 前端交互逻辑 |
| `figures.js` + `figures-*.js`（14 个文件） | 交互式图表渲染（SVG/Mermaid） |
| `style.css` | 样式表 |

### `.claude/` — Claude Code 集成

| 路径 | 用途 |
|------|------|
| `skills/check-understanding/SKILL.md` | `/check-understanding <阶段>` — 阶段测验 |
| `skills/find-your-level/SKILL.md` | `/find-your-level` — 水平定位测验 |

### `.github/` — CI/CD 与社区

| 路径 | 用途 |
|------|------|
| `workflows/curriculum.yml` | CI 工作流：audit（PR 阻塞门禁）、README 计数自动同步、站点自动重建 |
| `ISSUE_TEMPLATE/` | Bug 报告和新课程提案模板 |
| `PULL_REQUEST_TEMPLATE.md` | PR 检查清单 |

### 其他目录

| 目录 | 用途 |
|------|------|
| `outputs/` | 课程产物的顶层索引目录（prompts/skills/agents/mcp-servers），含 `index.json` 注册表 |
| `projects/` | 预留供学习者做项目（目前为空） |
| `web/` | 预留（目前为空） |
| `assets/` | `banner.svg` — README 顶部横幅图 |

---

## 数据流

```
README.md + ROADMAP.md + glossary/terms.md
        ↓  site/build.js 解析
     site/data.js（自动生成，勿手动编辑）
        ↓  Vercel 部署
   aiengineeringfromscratch.com
```

## 单节课的目录结构

```
phases/XX-phase-name/YY-lesson-name/
├── docs/
│   └── en.md          # 课程正文（frontmatter + The Problem / The Concept / Build It / Use It / Ship It / Exercises）
├── code/              # 可运行代码
├── outputs/           # 可复用产物（prompt/skill/agent/mcp-server）
└── quiz.json          # 6 题测验
```
