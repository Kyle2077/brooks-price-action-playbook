## R

> Broad Channel and TR: Are Same for 90% of Bars. Broad Channel is similar to TR: expect deep PBs. PB often falls more than 50% and sometimes 100%. (Video 45A, PDF p574; Video 46A, PDF p684)

宽通道在 90% 的 K 线上等同于倾斜的交易区间（p574 渲染核对，reviewed；仍为作者断言）。操作方式与 TR 相同：预期深度回撤，可双向交易。

## I

宽通道是介于紧通道和水平 TR 之间的中间状态：它有方向性倾斜，但回撤深到足以让双方都获利。核心认知是"宽通道 ≈ 倾斜的 TR"——90% 的 K 线按 TR 规则处理（买低下卖高、双向），仅趋势性 10% 按通道规则。这意味着在宽通道中不应像紧通道那样只顺势，而应预期 50% 甚至更深的回撤，并在通道边界处赌突破失败（75% 失败率）。识别宽通道靠 4 个特征累积判定，无单一门槛。

## A1

**worked_example · retrospective: true**

来源：case24（Video 45A, PDF p574）。

复盘图展示宽牛通道与 TR 的双图并置：左图为宽牛通道，蓝色半透明矩形框出两段水平 TR 区间叠在整体上升结构上；右图为水平 TR 内含上升通道。作者以此说明二者在 90% 的 K 线上操作规则相同。

回顾要点：该案例直接例证了 p38（Broad Channel and TR: Same for 90% of Bars）。注意这是事后复盘图，不得据此推导胜率。

## A2

触发场景：
1. 用户问「这是宽通道吗 / Is this a broad channel」→ 执行 4 特征核对清单
2. 用户问「宽通道能不能双向 / Can I trade both sides」→ 可以，90% 的 K 线按 TR 规则
3. 用户问「回撤会多深 / How deep will pullback go」→ 常超 50%，有时 100%
4. 用户说「通道突破了我追不追 / BO above channel, chase?」→ 75% 失败，考虑 fade（c42）
5. 用户问「宽通道和 TR 有什么区别」→ 90% 等同，区别仅在倾斜方向

区分：
- 本卡不处理紧通道（只顺势），紧通道见 `tight-channel`
- 本卡不处理水平 TR 的详细操作，见 `trading-range`
- 本卡不处理通道结束后的状态切换，见 `breakout-transition`

关键词：宽通道 / broad channel / 倾斜 TR / sloped trading range / 双向 / deep pullback / 50% PB

## E

### 输入契约

必需字段：
- K 线图或行情描述（含至少 30 根以上连续 K 线）
- 时间框架（默认 5 分钟）
- 当前 Always In 方向

缺失任一时询问用户，不得猜值。

### 步骤

1. **逐条核对 4 特征**（p578/p688）：
   - ① 上下腿大多持续 5 根以上 K 线
   - ② 平均腿幅度 ≥ 3× 最小剥头皮尺度（Emini = 3 点；其他品种须自行标定）
   - ③ 腿幅度 ≥ 2–3× 平均 K 线大小
   - ④ 回撤常超过 50%

   完成标准：能明确回答每条「是/否/不确定」。满足 ≥3 条即可初步判定为宽通道。无量化门槛——"the more … the better"（作者断言，无统计口径）。

2. **应用 90% 等同规则**（p574/p684 reviewed）：
   - 宽通道中 90% 的 K 线按 TR 规则处理：买低下卖高、双向交易
   - 仅趋势性 10% 按通道规则（顺势）

3. **深回撤预期**（p664/p774）：
   - 回撤常超过 50%，有时达 100%（完全回吐前腿）
   - 在 50% 回撤处风险等于回报，概率通常 60% 对 40%（作者断言，无统计口径）

4. **通道 BO 失败规则**（p675/p786）：
   - 宽牛通道上方的牛市突破有 75% 概率在约 5 根 K 线内反转回落（作者断言，无统计口径）
   - 宽熊通道下方的熊市突破对称：75% 概率反转回升
   - 操作含义：通道边界处的突破应考虑 fade 而非追入（c42）

5. **判停点**：
   - 信息不足以判定 ≥3 条特征 → 暂停结论，要求补充数据
   - 特征更像紧通道（PB < 50%、1–3 根）→ 转 `tight-channel`
   - 无明显倾斜 → 转 `trading-range`

### 输出契约

| 字段 | 类型 | 说明 |
|------|------|------|
| channel_type | enum | broad_bull / broad_bear / not_broad |
| feature_checklist | table | 4 条特征的逐条核对结果 |
| allowed_actions | list | 允许的操作集（如 "both sides", "fade BO at boundary"） |
| pb_expectation | string | 回撤深度预期（如 ">50%, sometimes 100%"） |
| warnings | list | 禁止事项与风险提示 |

## B

**反场景**：
- 当 PB 浅于 50%、持续仅 1–3 根时，不是宽通道——可能是紧通道，转 `tight-channel`
- 当通道失去倾斜变为水平时，转为纯 TR，见 `trading-range`

**作者警告的失败模式**：
- c42：宽通道/通道 BO 通常失败（75%）（p675/p786）
- 在宽通道中用紧通道思维只顺势会错过大量双向机会
- 在宽通道边界追突破是高亏损概率行为

**批判盲点**：
- 4 特征均为定性描述，材料未给量化阈值或评分体系
- "90% of bars" 为作者对二者重叠程度的估计，非测量结果
- 75% BO 失败率为作者断言，无样本期或计算方法
- "5 bars" 的时间窗口也无统计依据

【全局边界 · 适用于本 Skill 全部能力】
1. 本书所有百分比（10/40/50/60/70/75/80/90%）均为作者 Al Brooks 的主观断言，材料未提供样本期、样本量、置信区间或计算方法；不得表述为客观概率或历史统计结果。
2. 所有硬数字（最小剥头皮尺度、时段窗口、K 线序号、Tick 阈值）绑定 Emini 5 分钟图与美股交易时段；用于 A 股、外汇、加密货币等其他市场时须自行重新标定，本 Skill 不提供换算方法。
3. 「强突破 / 强对手方 / 强信号 K 线 / 足够买卖压」等限定词在材料中无量化门槛，属作者定性判断；应列出可观察特征并说明判定不确定性，不得断言确定性结论。
4. 书中案例图均为事后复盘（右侧走势已知），不得据此推导胜率或期望值。
5. 本 Skill 只承载作者主张的规则与口径，用于方法论检索与结构化分析；不构成投资建议，不预测市场，不给出买卖指令。用户据此交易的盈亏与本 Skill 无关。
6. 作者方法存在根本软肋：入场规则的可证伪性弱（「任何 K 线都能入场」+「止损与入场点无关」），单次结果不能证实或证伪规则；连续亏损时应提示用户复核前提，而非继续套用同一规则。

## 图文证据

涉及图形、编号或图文对应时，先实际打开完整图与核查记录，再按需放大局部。当前宿主不能看图时说明限制；记录中的推断不能冒充图中事实。

- 图例 fig-broad-channel-vs-tr — 来源 src-brooks-htpa，PDF 页序 574，书本页码 未核对；源文件 SHA256 `02e6d9cca2ffabd977ecd63c2944d1a73652dc3649cbb6cada90d3e2d50a79da`
  - [完整图](../../resources/figures/broad-channel/page-0574.png) · [图文核查记录](../../resources/figures/broad-channel/figure-notes.md)

## 配套资源

路径相对于本文件；脚本需先检查运行条件，不因附带而自动执行。

- [resources/figures/broad-channel/page-0574.png](../../resources/figures/broad-channel/page-0574.png)
- [resources/figures/broad-channel/page-0574.txt](../../resources/figures/broad-channel/page-0574.txt)
- [resources/figures/broad-channel/figure-notes.md](../../resources/figures/broad-channel/figure-notes.md)
