## R

> "HH Major Trend Reversal (MTR): Needs Strong Bears. Usually need strong bear leg with at least 5 bear bars, or weaker bear leg or TR with 10 or more bars." — Video 38A（PDF p48，渲染核对，reviewed；仍为作者断言）
>
> "Need Minimum Profit Target: Else Losing Strategy. Minimum target is 2x Actual Risk." — Video 38A（PDF p52）

**自译**：HH 主要趋势反转（MTR）需要强空头腿——通常需要至少 5 根强阴线，或更弱的阴线腿/交易区间持续 10 根以上 K 线。MTR 交易必须设定最小利润目标（至少 2 倍实际风险），否则是亏损策略。

## I

MTR 是材料中最高级别的反转结构，区别于次级反转（minor reversal）。成立需同时满足三要素：①强对手方腿（量化条件见 E 段）；②突破原有趋势线与均线；③恢复测试失败（如 High 2 牛旗被打破）。MTR 按形态分为六种类型：HH / HL / LL / LH / DB / DT。条件不齐备时仅为次级反转，不适用 MTR 规则集。Gap Bar 是确认买卖压的关键可观察代理——K 线极值与均线之间存在可见空隙。小形态只带来小反转（p71/p113/p115），因此 MTR 的腿部规模是必要条件而非充分条件。所有百分比与量化门槛均为作者断言，无统计口径。

## A1

**case21**（worked_example, retrospective: true, p48）：HH MTR 顶部。High 2 牛旗持续 20 根 K 线后，回撤有足够卖出压力突破牛趋势线和均线。图上标注「strong bear leg with at least 5 bear bars」，实际图中空头腿满足该条件。此案例验证了 MTR 第一要素——强对手方腿的量化门槛。

**case22**（worked_example, retrospective: true, p52）：MTR 入场后的最小利润目标管理。作者标注「Minimum target is 2x Actual Risk」，达到时分批获利 1/4 到 1/2。此案例验证了 MTR 若无最小利润目标则是亏损策略的规则。

两案例均为事后复盘（右侧走势已知），不得据此推导胜率或期望值。

## A2

触发场景：
1. 用户问「这是主要反转吗 / Is this a major trend reversal」→ 执行 MTR 三要素核查
2. 用户问「能不能抄底摸顶 / Can I pick a top or bottom」→ 先验 MTR 条件再回答
3. 用户描述「趋势线被突破了 / Trend line broke」→ 检查是否伴随强对手方腿
4. 用户提到「HH MTR / LL MTR / DB MTR」→ 按对应类型核查
5. 用户问「这个反转够大吗 / Is this reversal big enough」→ 检查腿部量化条件与最小目标

中英信号词：MTR、主要趋势反转、major trend reversal、HH/HL/LL/LH/DB/DT、gap bar、趋势线突破、trend line break

相邻区分：本卡不处理高潮反向（见 `climax-reversal`）；不处理 K 线计数入场（见 `bar-counting-entry`）；不处理市场周期状态诊断（见 `market-cycle-diagnosis`）。

## E

### 输入契约

| 字段 | 类型 | 必需 | 说明 |
|------|------|------|------|
| 当前趋势方向 | 枚举(bull/bear) | 是 | 决定检查 HH/HL 还是 LL/LH |
| 对手方腿部 K 线序列 | K 线列表 | 是 | 用于计数与强度判定 |
| 趋势线位置 | 价格或描述 | 是 | 判断是否被突破 |
| 均线位置 | 价格或描述 | 是 | 判断 Gap Bar |
| 入场价与止损价 | 价格 | 否 | 缺失时无法计算最小目标，应先询问 |

### 步骤

1. **识别对手方腿**：在原有趋势方向的反方向上，找到最近的连续同向 K 线序列。
   - 完成标准：能明确指出该腿的起止 K 线。

2. **核查腿部量化条件**（p48/p105 渲染核对，reviewed；仍为作者断言）：
   - 强对手方腿 = 至少 5 根强趋势 K 线（strong bear/bull leg with at least 5 bars）；或
   - 较弱腿或 TR = 10 根或以上 K 线（weaker leg or TR with 10 or more bars）。
   - 完成标准：满足上述任一条件。若不满足 → **判停**：不构成 MTR，降级为次级反转处理。

3. **核查趋势线与均线突破**：
   - 对手方腿的价格运动必须突破原有趋势线；且
   - 产生 Gap Bar = K 线极值与均线之间的空隙（gap between MA and high/low of bar，p48/p105 reviewed）。
   - 完成标准：趋势线被穿越 + 至少一根 K 线整体位于均线另一侧。若不满足 → **判停**。

4. **核查恢复测试失败**：
   - 原趋势方尝试恢复但失败（如 High 2 牛旗被打破、Low 2 熊旗被打破）。
   - 完成标准：恢复尝试后价格未创新高/新低。若不满足 → **判停**：可能只是回调而非反转。

5. **确定 MTR 类型**：
   - HH MTR：更高高点后反转下跌
   - HL MTR：更高低点后反转下跌
   - LL MTR：更低低点后反转上涨
   - LH MTR：更低高点后反转上涨
   - DB MTR：双底后反转上涨
   - DT MTR：双顶后反转下跌
   - 完成标准：匹配一种类型标签。

6. **计算最小利润目标**（p52/p109）：
   - 最小目标 ≥ 2× Actual Risk（入场价到止损价的距离）。
   - 若 Initial Risk 较小，可用 Initial Risk 替代。
   - 完成标准：输出具体目标价位。若无法设定 ≥ 2× AR 的目标 → **判停**：交易者方程为负，不应入场。

### 输出契约

| 字段 | 说明 |
|------|------|
| MTR 成立 | true / false |
| MTR 类型 | HH / HL / LL / LH / DB / DT |
| 三要素核对表 | 每项 pass / fail + 依据 |
| 最小利润目标 | 价格 + 对应的风险倍数 |
| 判停原因 | 若不成立，说明哪一步失败 |

## B

**反场景**：
- 对手方腿只有 3-4 根 K 线且不满足弱腿/TR ≥10 根条件 → 不是 MTR，只是次级反转。
- 趋势线未被突破 → 即使有高潮也只是通道内的正常回调。
- 没有 Gap Bar → 买卖压不足以构成主要反转。
- 小形态只带来小反转（p71/p113/p115）：腿部规模不够时不要预期大幅反转。

**作者警告的失败模式**：
- c40：Give-up Bar 标志趋势终结，但 give-up bar 本身不等于 MTR 成立——仍需三要素齐备。
- c24：趋势末端的大 K 线常是高潮终点而非新趋势起点；晚期追入是确认偏误。
- c15：只看支持自己方向的论据而忽略反面证据；TR 中强腿常是 2nd Leg Trap 而非 MTR。

**批判盲点**：
- 「强对手方」的「强」无量化门槛（nr-07），5 根/10 根是经验值而非硬阈值；agent 应列出可观察特征并说明判定不确定性。
- 所有案例图均为事后复盘（右侧走势已知），不得据此推导胜率。
- MTR 类型的分类边界模糊（如 HL vs DB），材料未给严格区分标准。

【全局边界 · 适用于本 Skill 全部能力】
1. 本书所有百分比（10/40/50/60/70/75/80/90%）均为作者 Al Brooks 的主观断言，材料未提供样本期、样本量、置信区间或计算方法；不得表述为客观概率或历史统计结果。
2. 所有硬数字（最小剥头皮尺度、时段窗口、K 线序号、Tick 阈值）绑定 Emini 5 分钟图与美股交易时段；用于 A 股、外汇、加密货币等其他市场时须自行重新标定，本 Skill 不提供换算方法。
3. 「强突破 / 强对手方 / 强信号 K 线 / 足够买卖压」等限定词在材料中无量化门槛，属作者定性判断；应列出可观察特征并说明判定不确定性，不得断言确定性结论。
4. 书中案例图均为事后复盘（右侧走势已知），不得据此推导胜率或期望值。
5. 本 Skill 只承载作者主张的规则与口径，用于方法论检索与结构化分析；不构成投资建议，不预测市场，不给出买卖指令。用户据此交易的盈亏与本 Skill 无关。
6. 作者方法存在根本软肋：入场规则的可证伪性弱（「任何 K 线都能入场」+「止损与入场点无关」），单次结果不能证实或证伪规则；连续亏损时应提示用户复核前提，而非继续套用同一规则。

## 图文证据

涉及图形、编号或图文对应时，先实际打开完整图与核查记录，再按需放大局部。当前宿主不能看图时说明限制；记录中的推断不能冒充图中事实。

- 图例 fig-hh-mtr — 来源 src-brooks-htpa，PDF 页序 48，书本页码 未核对；源文件 SHA256 `02e6d9cca2ffabd977ecd63c2944d1a73652dc3649cbb6cada90d3e2d50a79da`
  - [完整图](../../resources/figures/mtr-reversal/page-0048.png) · [图文核查记录](../../resources/figures/mtr-reversal/figure-notes.md)
- 图例 fig-ll-mtr — 来源 src-brooks-htpa，PDF 页序 105，书本页码 未核对；源文件 SHA256 `02e6d9cca2ffabd977ecd63c2944d1a73652dc3649cbb6cada90d3e2d50a79da`
  - [完整图](../../resources/figures/mtr-reversal/page-0105.png) · [图文核查记录](../../resources/figures/mtr-reversal/figure-notes.md)

## 配套资源

路径相对于本文件；脚本需先检查运行条件，不因附带而自动执行。

- [resources/figures/mtr-reversal/page-0048.png](../../resources/figures/mtr-reversal/page-0048.png)
- [resources/figures/mtr-reversal/page-0048.txt](../../resources/figures/mtr-reversal/page-0048.txt)
- [resources/figures/mtr-reversal/page-0105.png](../../resources/figures/mtr-reversal/page-0105.png)
- [resources/figures/mtr-reversal/page-0105.txt](../../resources/figures/mtr-reversal/page-0105.txt)
- [resources/figures/mtr-reversal/figure-notes.md](../../resources/figures/mtr-reversal/figure-notes.md)
