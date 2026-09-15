# 配方:PULSE · AI 实时观测站

> 难度 ★★★ · 创建 prompt + 7 个迭代批次 · 成品示例:[线上站点](https://d41c8754b3a14836980c67b0acfcddfa.prod.enterapp.pro/)

**你会得到**:一个「24 小时活着」的技术雷达。Hacker News / GitHub / DEV.to 三源热榜,AI 流式输出四段式中文解读;排名动量徽章;Agent 自主挑选条目做真实内容深潜;每周自动聚合技术周报,一键复制 Markdown。全局 15 分钟原子锁控制成本,全访客共享同一「当前时刻」。

## 为什么它是 ★★★

PULSE 不是一次构建完成的——它是**一个创建 prompt + 七个有界迭代批次**的产物。直接抄最终形态容易得到一盘散沙;按批次走,每一步都有可验证的中间态。

## 路径

1. **创建 prompt**:[../entries/2026-08-pulse-ai-observatory/prompts/00-creation.txt](../entries/2026-08-pulse-ai-observatory/prompts/00-creation.txt)——先建出基础版(单源 + 流式解读 + 15 分钟锁)
2. **逐轮迭代的叙事与顺序**:读 [provenance](../entries/2026-08-pulse-ai-observatory/provenance.md) 的 Rounds 表——内容丰富化 → 榜单雷达化(点评+动量)→ 多数据源 → 每周周报 → Agent 工具化深潜 → 换源。代表性批次 prompt 在同目录 `prompts/`
3. **每批的铁律**:prompt 里携带上一轮**已验证**的基线作为不变量,外加明确排除项(明天的范围今天排除)

## 可调的旋钮

| 想要什么 | 改哪里 |
|---|---|
| 换数据源 | 创建 prompt 的源清单(任何公开 API/RSS;不可达的源要有诚实降级) |
| 换领域 | 「技术圈」换成产品/设计/学术——人设段同步改 |
| 换刷新频率 | 15 分钟锁改 30/60 分钟(直接决定 LLM 成本) |
| 去掉周报/深潜 | 对应批次不做即可,基础版自成一体 |

## 验收清单

- [ ] 首屏有真实榜单数据(不是占位)
- [ ] 刷新两次:15 分钟内内容不变,锁生效
- [ ] 数据库表 public read 可查(anon key 直读验证)
- [ ] 三个视口无横向溢出,console 无 error
