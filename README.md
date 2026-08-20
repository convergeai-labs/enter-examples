# enter-examples

> 🌐 **English version** → [README.en.md](README.en.md)

<p align="center">
  <img src="assets/banner-enter-examples.png" width="760" alt="enter-examples — agent 在 Enter 上的作品陈列室">
</p>

<p align="center">
  <strong>真实上线、点开就玩的 Enter 作品陈列室——每个作品附 prompt 原文与逐轮验证记录</strong>
</p>

<p align="center">
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-22ff88" alt="MIT"></a>
  <a href="https://d41c8754b3a14836980c67b0acfcddfa.prod.enterapp.pro/"><img src="https://img.shields.io/badge/🔴_live-PULSE_观测站-22ff88" alt="live demo"></a>
  <a href="https://github.com/convergeai-labs/enter-skills"><img src="https://img.shields.io/badge/方法论-enter--skills-22d3ee" alt="skills"></a>
</p>

在 [Enter](https://enter.converge.ai)(AI 应用构建平台)上、由 agent 按 [enter-skills](https://github.com/convergeai-labs/enter-skills) playbook 驱动 Enter 创作的示例作品。每个条目都附带完整故事、截图、prompt 原文与 provenance 记录。

---

## 🛰️ PULSE — AI 实时观测站

<p align="center">
  <img src="entries/2026-08-pulse-ai-observatory/screenshots/06-agent-deep-dive.png" width="720" alt="PULSE — AI 实时观测站">
</p>

一个「24 小时活着」的技术雷达:AI 流式解读 Hacker News / GitHub **此刻**的讨论,所有访客共享同一个「当前时刻」;排名动量徽章追踪榜单变化;Agent 自主挑选 3 条新闻并用真实抓取的内容做深潜解读;每周自动生成技术周报,一键复制 Markdown 即可分享到团队周报渠道。

**▶ 在线预览**:[PULSE — AI 实时观测站](https://d41c8754b3a14836980c67b0acfcddfa.prod.enterapp.pro/)(已发布 prod;打开即当前共享快照,每 15 分钟最多重新生成一次)

零输入,首屏即内容。3 天 7 个有界批次构建完成,每个批次都在 Enter 之外独立验证——包括数据库直查与系统剪贴板读回。

| | |
|---|---|
| <img src="entries/2026-08-pulse-ai-observatory/screenshots/03-multi-source.png" width="340" alt="多源雷达"> | <img src="entries/2026-08-pulse-ai-observatory/screenshots/05-weekly-report.png" width="340" alt="每周技术周报"> |
| 三源雷达 + 动量徽章 | 每周技术周报 + 复制 Markdown |

### 它是怎么被 agent 造出来的

<p align="center">
  <img src="assets/agent-builds-living-site.png" width="720" alt="从 prompt 到活网站:agent 驱动 Enter 构建">
</p>

契约先行 → 一个富创建 prompt → 六个内聚批次(每批携带上一轮已验证基线作为不变量)→ 每批独立复验。Enter 负责执行,agent 负责规划与验证——Enter 的回执只是 claim,证据全部来自 Enter 之外的泳道。

📖 **完整故事 + agent 创作方法**:[entries/2026-08-pulse-ai-observatory/](entries/2026-08-pulse-ai-observatory/)
🛠 **方法论 skill**:[enter-project-ops](https://github.com/convergeai-labs/enter-skills/blob/main/skills/enter-project-ops/SKILL.md)

---

## 条目索引

| 条目 | 类型 | 一句话 |
|---|---|---|
| [2026-08-pulse-ai-observatory](entries/2026-08-pulse-ai-observatory/) | 实时 AI 技术雷达 | 零输入观测站:流式解读、三源雷达、动量徽章、Agent 深潜、每周周报——7 个已验证批次 |

更多条目筹备中——每个新的 Enter 作品都会带着它的 prompt 与 provenance 落到这里。
