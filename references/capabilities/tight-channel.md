## R

> The more of these features present, the better it is to only buy [sell]: PBs last mostly 1–3 bars. Size of PB less than 2–3 times as big as smallest scalp. Size of PB less than 2 times the size of average bar. Most PBs only 1/3rd to 1/2 of prior leg. Sell [Buy] setups using stop entries are mostly losers. Gaps between PB and BO points — losses offset gains. (Video 43A, PDF p409; Video 44A, PDF p493)

满足以上特征越多，越应只顺势交易。前 5 条来自 OCR 文本层；第 6 条（PB 与突破点间存在缺口）OCR 完全缺失，仅见于渲染图（p409/p493 reviewed）。

## I

紧通道是一种极端趋势状态：回撤极浅、极短、几乎不给逆势方任何获利空间。判定不靠单一阈值，而是累积 6 个可观察特征——满足越多，"只顺势"的确定性越高。核心操作含义是：在紧通道中试图逆势交易（用止损单入场）基本都是亏损的，因为回撤幅度不够覆盖成本与风险；即便限价单在回撤低点接到货，止损单的亏损也会抵消盈利。第一次反向运动通常是次级的（70% 概率只是小反转），不应据此判断趋势结束。紧通道最终会以楔形顶/底或演变为 TR 告终，但在那之前，唯一正确的策略就是顺势。

## A1

**worked_example · retrospective: true**

来源：case09/case23（Video 49A, PDF p1067 / Video 43A, PDF p410）。

复盘图展示一段 Emini 5 分钟紧牛通道：连续约 40 根 K 线上升，每次回撤仅 1–3 根、幅度不超过 2 点。图中多次标注空头尝试卖出均被迅速吞没，形成 HL 双底后继续上涨。作者指出：紧牛通道中空头反转尝试反复失败，赌空头止损被打是多头获利的来源。

回顾要点：该案例同时例证了 c01（紧牛通道逆势必亏）和 p40（绝不逆势）两条规则。注意这是事后复盘图，右侧走势已知，不得据此推导胜率。

## A2

触发场景：
1. 用户问「这是紧通道吗 / Is this a tight channel」→ 执行 6 特征核对清单
2. 用户问「紧通道能不能逆势 / Can I fade a tight channel」→ 判停：只顺势
3. 用户看到微通道（Micro Channel）问怎么处理 → 紧通道的极端形式，只能顺势
4. 用户说「回撤很小不敢追 / Pullback too small to enter」→ BTC/STC 见 strong-bo-entry
5. 用户问「紧通道什么时候结束」→ 见 breakout-transition

区分：
- 本卡不处理宽通道（双向操作），宽通道见 `broad-channel`
- 本卡不处理强突破期入场（BTC/STC），见 `strong-bo-entry`
- 本卡不处理通道结束后的状态切换，见 `breakout-transition`

关键词：紧通道 / tight channel / micro channel / 只顺势 / 逆势必亏 / pullback too shallow

## E

### 输入契约

必需字段：
- K 线图或行情描述（含至少 20 根以上连续 K 线）
- 时间框架（默认 5 分钟；其他周期须声明）
- 当前 Always In 方向（若未提供，先调用 `always-in-direction`）

缺失任一时询问用户，不得猜值。

### 步骤

1. **逐条核对 6 特征**（p409/p493 reviewed）：
   - ① PB 多为 1–3 根 K 线
   - ② PB 幅度 < 2–3× 最小剥头皮尺度（Emini = 1 点 = 4 ticks；其他品种须自行标定）
   - ③ PB 幅度 < 2× 平均 K 线大小
   - ④ 多数 PB 仅到前腿的 1/3–1/2
   - ⑤ 用止损单逆势入场基本都是亏损单
   - ⑥ **PB 与突破点之间存在缺口（Gaps between PB and BO points）：限价单与止损单的盈亏互相抵消**
     - ⚠️ 此条 OCR 文本层完全缺失，仅见于 p409/p493 渲染图（reviewed；仍为作者断言）

   完成标准：能明确回答每条「是/否/不确定」。满足 ≥4 条即可初步判定为紧通道；满足 6 条为高度确定。无量化门槛——"the more … the better"（作者断言，无统计口径）。

2. **判定通道方向**：
   - 牛市紧通道 → 只做多
   - 熊市紧通道 → 只做空

3. **操作规则**：
   - 只顺势入场（BTC/STC 或顺势限价单）
   - 第一次反向运动通常次级（p430/p515：First Reversal Usually Minor，70% 概率；作者断言，无统计口径）
   - 逆势必亏（c01/c02）：不做任何逆势交易

4. **判停点**：
   - 信息不足以判定 ≥4 条特征 → 暂停结论，要求补充数据
   - 用户要求逆势操作 → 判停并引用 c01/c02
   - 特征少于 3 条 → 可能不是紧通道，转 `market-cycle-diagnosis` 重新诊断

### 输出契约

| 字段 | 类型 | 说明 |
|------|------|------|
| channel_type | enum | tight_bull / tight_bear / not_tight |
| feature_checklist | table | 6 条特征的逐条核对结果 |
| allowed_actions | list | 允许的操作集（如 "only buy", "BTC only"） |
| warnings | list | 禁止事项与风险提示 |

## B

**反场景**：
- 当 PB 深度超过 50%、持续 5+ 根 K 线时，不是紧通道——可能是宽通道或 TR，转 `broad-channel` 或 `trading-range`
- 当出现 2–5 根强反向 K 线且收盘超越通道边界时，紧通道可能已结束，转 `breakout-transition`

**作者警告的失败模式**：
- c01：紧牛通道逆势做空必亏（p410）
- c02：紧熊通道逆势做多必亏（p494）
- 特征累积口径为"越多越确定"，无判定门槛与权重（nr-07 型缺口）；agent 应向用户说明判定依据而非断言结论

**批判盲点**：
- 6 特征均为定性描述，材料未给量化阈值或评分体系
- 示例数值（10 ticks、2.75 points 等）绑定 Emini 且为个案，不作通用阈值
- 所有百分比（70% 次级反转等）为作者断言，无统计口径

【全局边界 · 适用于本 Skill 全部能力】
1. 本书所有百分比（10/40/50/60/70/75/80/90%）均为作者 Al Brooks 的主观断言，材料未提供样本期、样本量、置信区间或计算方法；不得表述为客观概率或历史统计结果。
2. 所有硬数字（最小剥头皮尺度、时段窗口、K 线序号、Tick 阈值）绑定 Emini 5 分钟图与美股交易时段；用于 A 股、外汇、加密货币等其他市场时须自行重新标定，本 Skill 不提供换算方法。
3. 「强突破 / 强对手方 / 强信号 K 线 / 足够买卖压」等限定词在材料中无量化门槛，属作者定性判断；应列出可观察特征并说明判定不确定性，不得断言确定性结论。
4. 书中案例图均为事后复盘（右侧走势已知），不得据此推导胜率或期望值。
5. 本 Skill 只承载作者主张的规则与口径，用于方法论检索与结构化分析；不构成投资建议，不预测市场，不给出买卖指令。用户据此交易的盈亏与本 Skill 无关。
6. 作者方法存在根本软肋：入场规则的可证伪性弱（「任何 K 线都能入场」+「止损与入场点无关」），单次结果不能证实或证伪规则；连续亏损时应提示用户复核前提，而非继续套用同一规则。

## 图文证据

涉及图形、编号或图文对应时，先实际打开完整图与核查记录，再按需放大局部。当前宿主不能看图时说明限制；记录中的推断不能冒充图中事实。

- 图例 fig-tight-bull-channel — 来源 src-brooks-htpa，PDF 页序 409，书本页码 未核对；源文件 SHA256 `02e6d9cca2ffabd977ecd63c2944d1a73652dc3649cbb6cada90d3e2d50a79da`
  - [完整图](../../resources/figures/tight-channel/page-0409.png) · [图文核查记录](../../resources/figures/tight-channel/figure-notes.md)
- 图例 fig-tight-bear-channel — 来源 src-brooks-htpa，PDF 页序 493，书本页码 未核对；源文件 SHA256 `02e6d9cca2ffabd977ecd63c2944d1a73652dc3649cbb6cada90d3e2d50a79da`
  - [完整图](../../resources/figures/tight-channel/page-0493.png) · [图文核查记录](../../resources/figures/tight-channel/figure-notes.md)

## 配套资源

路径相对于本文件；脚本需先检查运行条件，不因附带而自动执行。

- [resources/figures/tight-channel/page-0409.png](../../resources/figures/tight-channel/page-0409.png)
- [resources/figures/tight-channel/page-0409.txt](../../resources/figures/tight-channel/page-0409.txt)
- [resources/figures/tight-channel/page-0493.png](../../resources/figures/tight-channel/page-0493.png)
- [resources/figures/tight-channel/page-0493.txt](../../resources/figures/tight-channel/page-0493.txt)
- [resources/figures/tight-channel/figure-notes.md](../../resources/figures/tight-channel/figure-notes.md)
