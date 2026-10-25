## R

> "When context is good, 60% chance of TBTL (Ten Bars, Two Legs) sideways to down PB after Buy Climax." — Video 42B（PDF p372，渲染核对，reviewed；仍为作者断言）
>
> "18 bar bear Micro channel → 70% chance of TBTL PB or reversal." — Video 42B（PDF p381，渲染核对，reviewed；仍为作者断言）

**自译**：上下文良好时，买入高潮后有 60% 概率出现至少 10 根 K 线、2 条腿的横盘或回调。18 根 K 线的熊市微通道后有 70% 概率出现 TBTL 回调或反转。（两档概率均为作者断言，无统计口径；分档为语境推断，材料未显式确认。）

## I

高潮是趋势末段的加速运动，作者认为这是最高质量的反向机会。高潮类型包括：Buy Climax / Sell Climax（单次极端加速）、趋势末段 Micro Channel（连续 ≥5 根无回撤小 K 线，p381 reviewed）、连续高潮构成 Wedge（如 3 次连续 Sell Climax 形成楔形底，p383 reviewed）。高潮后预期 TBTL（Ten Bars, Two Legs）——至少 10 根 K 线、2 条腿的横盘或反转。一般高潮后概率约 60%，更极端场景（微通道 ≥18 根或连续 ≥3 次高潮）概率约 70%。反向入场时止损设在强信号 K 线外侧，许多人会在更低处加仓（p383）。所有概率为作者断言，无统计口径。

## A1

**c40**（counter-example, p211-214）：Give-up Bar 标志被困方最终投降，趋势动能耗尽。在高潮背景下，give-up bar 常是高潮终结后的第一个明确反转信号。此案例说明高潮识别后应关注 give-up bar 作为入场时机参考。

**c43**（counter-example, p382）：微通道后期的首次突破通常失败。持续多根 K 线的微通道本身就是高潮信号；对首次突破追入是被获利了结打压的典型亏损模式。此案例验证了微通道 = 高潮的识别规则。

两案例均为事后复盘，不得据此推导胜率。

## A2

触发场景：
1. 用户问「这是高潮吗 / Is this a climax」→ 执行高潮类型识别
2. 用户问「能不能反向做 / Can I fade this move」→ 先验高潮条件与 TBTL 预期
3. 用户提到「TBTL / Ten Bars Two Legs」→ 按本卡规则给出概率档位
4. 用户描述「连续大阳线/大阴线 / consecutive big bars」→ 检查是否为高潮
5. 用户问「微通道怎么处理 / What about this micro channel」→ 按高潮框架处理

中英信号词：高潮、climax、Buy Climax、Sell Climax、微通道、micro channel、TBTL、Ten Bars Two Legs、衰竭、exhaustion、反向、fade

相邻区分：本卡不处理 MTR 结构验证（见 `mtr-reversal`）；不处理 Measured Move 目标计算（见 `measured-move`）；不处理 TR 中的第二条腿陷阱（见 `second-leg-trap`）。

## E

### 输入契约

| 字段 | 类型 | 必需 | 说明 |
|------|------|------|------|
| 趋势方向与持续时间 | 枚举 + K 线数 | 是 | 判断是否处于趋势末段 |
| 近期 K 线序列 | K 线列表 | 是 | 识别高潮类型 |
| 已知支撑/阻力位 | 价格列表 | 否 | 高潮总是结束于 S/R（f11） |
| 之前是否有楔形/通道 | 布尔 | 否 | 影响上下文判定 |

### 步骤

1. **确认趋势末段**：趋势已持续 20+ 根 K 线（f11），或出现明显加速度变化。
   - 完成标准：能指出趋势起点与当前 K 线数。
   - **显式分支**：`if 趋势 ≥ 20 根` → 正常进入高潮类型判定；`elif 趋势 < 20 根 但存在加速度证据（Micro Channel ≥5 根无回撤小 K 线 p381 reviewed，或连续 ≥3 次同向高潮 p383 reviewed）` → 仍可判定高潮，置信度标「中」并注明以加速度替代长度条件；`else`（既不足 20 根又无加速度证据）→ **判停：不判定高潮**，转 `market-cycle-diagnosis` 复核状态，不得给出反向建议。

2. **识别高潮类型**：
   - **Buy/Sell Climax**：单次极端加速（大实体 K 线、连续同向、收盘靠近极值）。
   - **Micro Channel 高潮**：趋势末段连续 ≥5 根无回撤小 K 线（p381 渲染核对，reviewed；仍为作者断言）。≥18 根归入极端档。
   - **连续高潮构成 Wedge**：连续 ≥3 次同向高潮形成楔形结构（p383 reviewed）。
   - 完成标准：匹配一种类型。若不匹配 → 可能只是普通 BO 而非高潮。

3. **确定 TBTL 概率档位**：
   - **一般档 60%**：单次 Buy/Sell Climax 且上下文良好（p372/p1140 reviewed）。
   - **极端档 70%**：微通道 ≥18 根（p381 reviewed）或连续 ≥3 次高潮构成 Wedge（p383 reviewed）。
   - 完成标准：输出一档概率标签。**注意**：此分档为语境推断，材料未用显式语言标注区分条件（nr-01）。

4. **确认 S/R 位**：高潮总是结束于支撑/阻力位（f11）。检查当前价格是否接近已知磁体位。
   - 完成标准：能指出最近的 S/R 位。若无明确 S/R → 降低反向入场的置信度。

5. **反向入场条件**（p383 reviewed）：
   - 止损设在强信号 K 线外侧。
   - 许多人会在更低/更高处加仓（scale in lower/higher）。
   - 初学者应在可能的高潮处平仓而非反向入场。
   - 完成标准：输出入场价、止损价、是否适合反向。

### 输出契约

| 字段 | 说明 |
|------|------|
| 高潮类型 | Buy Climax / Sell Climax / Micro Channel / Wedge |
| TBTL 概率档位 | 60%（一般）/ 70%（极端）+ 分档依据 |
| 最近 S/R 位 | 价格 |
| 反向入场建议 | 入场价 + 止损价 + 适用性（初学者/专家） |
| 不确定性声明 | 分档为语境推断；概率为作者断言 |

## B

**反场景**：
- 趋势不足 20 根 K 线的加速 → 更可能是普通 BO 而非衰竭高潮。
- 没有到达已知 S/R 位的加速 → 高潮尚未完成，反向入场过早。
- 微通道不足 5 根 K 线 → 不构成 Micro Channel 高潮定义。
- 单次高潮后直接 V 型反转而无 TBTL → 虽然发生但不符合 60% 预期，属 40% 情形。

**作者警告的失败模式**：
- c43：微通道后期首次突破通常失败——追入微通道突破是高潮场景下的典型亏损模式。
- c40：Give-up Bar 是趋势终结信号，但忽视它继续在已终结趋势中持仓会导致亏损。
- c24：趋势末端的大 K 线看起来像确认实则是耗竭；恐惧驱动的确认偏误导致在最高点追入。
- c44：观察趋势 10-20 根 K 线后等到最强 K 线才入场，此时概率已低、止损已远。

**批判盲点**：
- TBTL 60%/70% 分档为语境推断，材料未显式确认「因为更极端所以升到 70%」（nr-01）；两档概率均为作者断言，无统计口径。
- 「上下文良好（context is good）」在 p372 未定义，图上仅以 TR 顶部、带尾线巨阳柱等特征示意，无量化门槛（nr-07）。
- 「极端」高潮的判定阈值（K线大小、连续根数）无数值定义；18 根和 3 次是案例值而非硬阈值。
- 三张 reviewed 图（p372/p381/p383）均为复盘，不得据此推胜率。

【全局边界 · 适用于本 Skill 全部能力】
1. 本书所有百分比（10/40/50/60/70/75/80/90%）均为作者 Al Brooks 的主观断言，材料未提供样本期、样本量、置信区间或计算方法；不得表述为客观概率或历史统计结果。
2. 所有硬数字（最小剥头皮尺度、时段窗口、K 线序号、Tick 阈值）绑定 Emini 5 分钟图与美股交易时段；用于 A 股、外汇、加密货币等其他市场时须自行重新标定，本 Skill 不提供换算方法。
3. 「强突破 / 强对手方 / 强信号 K 线 / 足够买卖压」等限定词在材料中无量化门槛，属作者定性判断；应列出可观察特征并说明判定不确定性，不得断言确定性结论。
4. 书中案例图均为事后复盘（右侧走势已知），不得据此推导胜率或期望值。
5. 本 Skill 只承载作者主张的规则与口径，用于方法论检索与结构化分析；不构成投资建议，不预测市场，不给出买卖指令。用户据此交易的盈亏与本 Skill 无关。
6. 作者方法存在根本软肋：入场规则的可证伪性弱（「任何 K 线都能入场」+「止损与入场点无关」），单次结果不能证实或证伪规则；连续亏损时应提示用户复核前提，而非继续套用同一规则。

## 图文证据

涉及图形、编号或图文对应时，先实际打开完整图与核查记录，再按需放大局部。当前宿主不能看图时说明限制；记录中的推断不能冒充图中事实。

- 图例 fig-tbtl-60 — 来源 src-brooks-htpa，PDF 页序 372，书本页码 未核对；源文件 SHA256 `02e6d9cca2ffabd977ecd63c2944d1a73652dc3649cbb6cada90d3e2d50a79da`
  - [完整图](../../resources/figures/climax-reversal/page-0372.png) · [图文核查记录](../../resources/figures/climax-reversal/figure-notes.md)
- 图例 fig-tbtl-70-micro — 来源 src-brooks-htpa，PDF 页序 381，书本页码 未核对；源文件 SHA256 `02e6d9cca2ffabd977ecd63c2944d1a73652dc3649cbb6cada90d3e2d50a79da`
  - [完整图](../../resources/figures/climax-reversal/page-0381.png) · [图文核查记录](../../resources/figures/climax-reversal/figure-notes.md)
- 图例 fig-tbtl-70-wedge — 来源 src-brooks-htpa，PDF 页序 383，书本页码 未核对；源文件 SHA256 `02e6d9cca2ffabd977ecd63c2944d1a73652dc3649cbb6cada90d3e2d50a79da`
  - [完整图](../../resources/figures/climax-reversal/page-0383.png) · [图文核查记录](../../resources/figures/climax-reversal/figure-notes.md)

## 配套资源

路径相对于本文件；脚本需先检查运行条件，不因附带而自动执行。

- [resources/figures/climax-reversal/page-0372.png](../../resources/figures/climax-reversal/page-0372.png)
- [resources/figures/climax-reversal/page-0372.txt](../../resources/figures/climax-reversal/page-0372.txt)
- [resources/figures/climax-reversal/page-0381.png](../../resources/figures/climax-reversal/page-0381.png)
- [resources/figures/climax-reversal/page-0381.txt](../../resources/figures/climax-reversal/page-0381.txt)
- [resources/figures/climax-reversal/page-0383.png](../../resources/figures/climax-reversal/page-0383.png)
- [resources/figures/climax-reversal/page-0383.txt](../../resources/figures/climax-reversal/page-0383.txt)
- [resources/figures/climax-reversal/figure-notes.md](../../resources/figures/climax-reversal/figure-notes.md)
