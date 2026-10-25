---
name: brooks-price-action-playbook
description: |
  Al Brooks《How to Trade Price Action》价格行为交易方法论手册（Video 37-49、51-52，排除 Video 50 剥头皮）。当用户拿着 K 线图或行情描述，问「现在是什么市场状态 / Always In 方向 / 该顺势还是逆势 / 止损放哪 / 目标看多少 / 这笔值不值得做 / 为什么我被套了」时调用；也覆盖日内时段判定与尾盘规则（现在算开盘/中段/尾段哪个时段、尾盘怎么做、当日高低点是否已形成、开盘 BOM 能不能追）。提供市场周期状态诊断、Always In 方向判定、交易者方程与 40-60 规则、五套互斥状态操作规则集（强突破/紧通道/宽通道/TR/开盘日内剧本）、反转结构（MTR/高潮/第二条腿陷阱）、止损与分批目标计算、三重保护与出场、被套处置、心理偏差自查。不处理：流动性/FVG/Killzone/订单块等 ICT 概念（改用 ict-intraday-playbook）、基本面与新闻驱动分析、剥头皮 Tick 指标（Video 50 未纳入）、实盘下单与投资建议。
metadata:
  cangjie.generated-by: cangjie-tools v2.5.0
  cangjie.variant: single
  cangjie.bundle-id: bundle.brooks-htpa
  cangjie.capability-count: 23
  cangjie.entrypoint-count: 1
---
# How to Trade Price Action（Brooks Trading Course, Video 37-49 & 51-52） — 全书能力入口

## 触发与不触发

**适用**：与本书能力域相关的咨询与任务（见下方路由表的意图列）。
**不适用**：
- ICT 体系概念（流动性、FVG、Killzone、订单块、SMT）——改用 ict-intraday-playbook
- 基本面、财报、新闻、宏观驱动的分析与预测
- 剥头皮 Tick 指标与 Tick 背离（Video 50 未纳入本次提取）
- 实盘下单、账户管理、仓位资金曲线优化、投资建议
- 非 Emini/美股时段品种的直接数值套用（须自行重新标定）

## 核心原则（常驻速览，概览类问题读到这里即可回答）

1. 先判定市场周期状态（突破/通道/交易区间）与 Always In 方向，再套用该状态专属且互斥的规则集；状态判错则整套操作反向
2. 每笔交易先过交易者方程：概率 × 回报 vs 风险必须为正期望；90% 的 K 线上多空概率都在 40%-60% 之间
3. 止损与入场点无关——同一笔交易无论从哪入场，止损位相同；必须始终有场内保护性止损，禁止心理止损
4. 强突破只顺势并买/卖收盘；紧通道只顺势；宽通道按倾斜的交易区间双向；TR 买低下卖高剥头皮；TTR 不交易
5. 前提改变就改变交易风格；所有趋势最终都让交易者失望，失望即出场以避免亏损而非为了获利
6. 书中所有百分比都是作者断言、无统计口径；硬数字绑定 Emini 与美股时段——给出结论时必须同时给出判定依据与不确定性

## 能力路由（先读本表，按意图加载 1 张能力卡）

| 用户意图 | 先读 | 补读/备注 |
|---|---|---|
| 判断现在是什么市场状态；这是趋势还是震荡；图上是突破还是通道；market cycle state；trend or trading range | references/capabilities/market-cycle-diagnosis.md | references/capabilities/always-in-direction.md、references/capabilities/trading-range.md、references/capabilities/tight-channel.md、references/capabilities/broad-channel.md、references/capabilities/breakout-transition.md、references/capabilities/traders-equation.md、references/capabilities/mtr-reversal.md、references/capabilities/intraday-structure.md、references/capabilities/timeframe-combination.md |
| 现在市场偏多还是偏空；Always In 是哪个方向；该做多还是做空；always in long or short；direction bias | references/capabilities/always-in-direction.md | references/capabilities/market-cycle-diagnosis.md、references/capabilities/breakout-transition.md、references/capabilities/trapped-disposal.md |
| 这笔交易值不值得做；盈亏比够不够；概率和回报怎么配；trader's equation；risk reward probability | references/capabilities/traders-equation.md | references/capabilities/stop-placement.md、references/capabilities/profit-targets.md、references/capabilities/market-cycle-diagnosis.md、references/capabilities/scale-in.md、references/capabilities/psychology-sizing.md |
| 止损放哪；止损设多远；怎么移动止损；initial risk actual risk；stop placement trailing | references/capabilities/stop-placement.md | references/capabilities/traders-equation.md、references/capabilities/protection-exit.md、references/capabilities/scale-in.md、references/capabilities/profit-targets.md、references/capabilities/strong-bo-entry.md |
| 目标看多少；什么时候止盈；怎么分批获利；profit target；take profit scaling out | references/capabilities/profit-targets.md | references/capabilities/traders-equation.md、references/capabilities/measured-move.md、references/capabilities/stop-placement.md |
| 这是紧通道吗；紧通道怎么做；能不能逆势；tight channel；micro channel | references/capabilities/tight-channel.md | references/capabilities/broad-channel.md、references/capabilities/market-cycle-diagnosis.md、references/capabilities/strong-bo-entry.md、references/capabilities/timeframe-combination.md |
| 这是宽通道吗；宽通道怎么做；能不能双向；broad channel；sloped trading range | references/capabilities/broad-channel.md | references/capabilities/tight-channel.md、references/capabilities/trading-range.md、references/capabilities/market-cycle-diagnosis.md、references/capabilities/timeframe-combination.md |
| 这是震荡区间吗；TR 怎么做；TTR 能不能交易；trading range；80% rule | references/capabilities/trading-range.md | references/capabilities/market-cycle-diagnosis.md、references/capabilities/second-leg-trap.md、references/capabilities/breakout-transition.md、references/capabilities/broad-channel.md、references/capabilities/climax-reversal.md、references/capabilities/bar-counting-entry.md |
| 突破结束了吗；什么时候换方法；风格要不要切换；breakout phase end；premise change | references/capabilities/breakout-transition.md | references/capabilities/strong-bo-entry.md、references/capabilities/market-cycle-diagnosis.md、references/capabilities/trapped-disposal.md、references/capabilities/always-in-direction.md、references/capabilities/trading-range.md |
| 突破来了怎么追；BTC/STC 是什么；强突破能不能等回调；buy the close；breakout entry | references/capabilities/strong-bo-entry.md | references/capabilities/breakout-transition.md、references/capabilities/tight-channel.md、references/capabilities/stop-placement.md、references/capabilities/bar-counting-entry.md、references/capabilities/opening-playbook.md |
| 这是主要反转吗；MTR 成立吗；能不能抄底/摸顶；major trend reversal；HH LL MTR | references/capabilities/mtr-reversal.md | references/capabilities/climax-reversal.md、references/capabilities/bar-counting-entry.md、references/capabilities/market-cycle-diagnosis.md |
| 这是高潮吗；能不能反向做；TBTL 是什么；climax；buy climax sell climax | references/capabilities/climax-reversal.md | references/capabilities/mtr-reversal.md、references/capabilities/measured-move.md、references/capabilities/trading-range.md |
| 这是第二条腿陷阱吗；能不能反向做这条腿；2nd leg trap；为什么追腿就亏 | references/capabilities/second-leg-trap.md | references/capabilities/trading-range.md、references/capabilities/trapped-disposal.md、references/capabilities/measured-move.md |
| 目标怎么算；等距测量；measured move；缺口测量；measuring gap | references/capabilities/measured-move.md | references/capabilities/profit-targets.md、references/capabilities/climax-reversal.md、references/capabilities/second-leg-trap.md、references/capabilities/magnet-levels.md |
| High 2 是什么意思；怎么数回调；bar counting；High 1 High 2 入场 | references/capabilities/bar-counting-entry.md | references/capabilities/mtr-reversal.md、references/capabilities/trading-range.md、references/capabilities/strong-bo-entry.md |
| 现在算日内哪个时段；尾盘怎么做；当日高低点形成了吗；intraday structure；end of day | references/capabilities/intraday-structure.md | references/capabilities/opening-playbook.md、references/capabilities/magnet-levels.md、references/capabilities/market-cycle-diagnosis.md、references/capabilities/protection-exit.md |
| 开盘怎么做；BOM 是什么；开盘突破能追吗；opening range；breakout mode | references/capabilities/opening-playbook.md | references/capabilities/intraday-structure.md、references/capabilities/magnet-levels.md、references/capabilities/strong-bo-entry.md |
| 关键价位在哪；磁体位怎么找；昨日高低点有什么用；magnet levels；support resistance | references/capabilities/magnet-levels.md | references/capabilities/intraday-structure.md、references/capabilities/opening-playbook.md、references/capabilities/measured-move.md |
| 用哪个周期看；两个周期矛盾怎么办；timeframe；higher time frame | references/capabilities/timeframe-combination.md | references/capabilities/market-cycle-diagnosis.md、references/capabilities/tight-channel.md、references/capabilities/broad-channel.md |
| 能不能加仓；加仓步长怎么定；scale in；摊平对不对 | references/capabilities/scale-in.md | references/capabilities/stop-placement.md、references/capabilities/traders-equation.md、references/capabilities/psychology-sizing.md |
| 什么时候出场；止损被打掉怎么办；三重保护是什么；exit rules；mental stop | references/capabilities/protection-exit.md | references/capabilities/stop-placement.md、references/capabilities/trapped-disposal.md、references/capabilities/intraday-structure.md、references/capabilities/psychology-sizing.md |
| 我被套了怎么办；要不要保本出；看不懂行情怎么办；trapped；disappointed | references/capabilities/trapped-disposal.md | references/capabilities/protection-exit.md、references/capabilities/breakout-transition.md、references/capabilities/second-leg-trap.md、references/capabilities/always-in-direction.md |
| 为什么我总是亏；目标混淆怎么办；仓位多大合适；trading psychology；I don't care size | references/capabilities/psychology-sizing.md | references/capabilities/scale-in.md、references/capabilities/protection-exit.md、references/capabilities/traders-equation.md |

**非能力类查询**：
- 书名/作者/章节/整书概览 → references/overview.md
- 术语解释 → references/glossary.md
- 决策规则速查（不需要原文依据时） → references/cheatsheet.md
- 完整意图与关键词索引（本表未覆盖的意图先查这里） → references/capability-index.md

## 加载规则

- 每次任务先读本文件，再按路由表加载 **1** 张能力卡；任务明确跨域时最多加载 2 张。
- 概览/书名类问题不加载能力卡，用「核心原则」与 overview.md 回答。
- 路由表与 capability-index.md 都无法命中的意图，明确告知超出本书范围，不要硬套。

## 边界与判停

- 用户提供的信息不足以判定市场状态（无图、无周期、无方向线索）时，先询问缺失字段，不得静默猜值
- 用户要求给出买卖指令或收益承诺时，说明本 Skill 只承载作者方法论、不构成投资建议，并停止
- 用户问的是流动性/FVG/Killzone 等 ICT 概念时，转介 ict-intraday-playbook
- 同一规则连续多次给出不利结果、用户质疑规则有效性时，提示复核前提（规则可证伪性弱），不继续机械套用
