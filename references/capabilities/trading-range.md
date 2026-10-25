## R

> In TR, 80% of BOs up and down fail. Markets have inertia and resist change. (Video 47B, PDF p812)

TR 中 80% 的向上和向下突破都会失败（p812 渲染核对，reviewed；仍为作者断言）。该规则在 p394/p786/p828/p1004/p1012/p1015 有多次独立重述。市场具有惯性，抵抗变化。

## I

交易区间（TR）是市场最常见的状态，覆盖约 90% 的交易时间。核心操作逻辑建立在 80% 规则之上：既然绝大多数突破都会失败，那么默认策略就是赌突破失败——买低下卖高、用限价单剥头皮。TR 是限价单市场，不是止损单市场。买卖区的定义取决于当前状态：在纯 TR 中，买区 = 区间下 1/3、卖区 = 上 1/3；但在趋势中的回调阶段，买区 = 最近上涨腿的下 2/3、卖区 = 最近下跌腿的上 2/3。两种口径不可混用，必须先判状态再选公式。TTR（紧密交易区间）不交易，除非满足严格条件。每个 TR 最终以趋势结束。

## A1

**worked_example · retrospective: true**

来源：case25（Video 47B, PDF p812）。

复盘图展示三日 Emini 5 分钟 TR，粉/绿斜带标出上下失败的突破腿。图中清晰可见：每次突破前高或前低后都在 3–5 根 K 线内反转回区间内部。标题即为「80% Rule: Failed BO and Then Reversal Is Common」。

回顾要点：该案例直接例证了 c35（TR 中 80% 的突破会失败）。注意这是事后复盘图，不得据此推导胜率。

## A2

触发场景：
1. 用户问「这是震荡区间吗 / Is this a trading range」→ 执行 TR/TTR/BOM 分类
2. 用户问「TR 怎么做 / How to trade a TR」→ BLSHS + 限价单 + 80% 规则
3. 用户问「买卖区在哪 / Where is the buy/sell zone」→ 先判状态再选口径
4. 用户问「TTR 能不能交易 / Should I trade a TTR」→ 不交易（c30）
5. 用户问「TR 什么时候结束」→ TR 最终必以趋势结束（p875）

区分：
- 本卡不处理趋势状态的操作，趋势见 `market-cycle-diagnosis` + 各状态卡
- 本卡不处理第二条腿陷阱的详细机制，见 `second-leg-trap`
- 本卡不处理突破阶段结束的信号，见 `breakout-transition`

关键词：交易区间 / trading range / TR / TTR / BOM / 80% 规则 / 买卖区 / buy zone / sell zone / BLSHS / 限价单市场

## E

### 输入契约

必需字段：
- K 线图或行情描述（含至少 30 根以上连续 K 线）
- 时间框架（默认 5 分钟）
- 当前市场状态判定（若未提供，先调用 `market-cycle-diagnosis`）

缺失任一时询问用户，不得猜值。

### 步骤

1. **分类 TR 子类型**：
   - **普通 TR**：高度 ≥ 3× 平均 K 线或 ≥ 3× 最小剥头皮尺度，大多数 K 线 > 最小剥头皮尺度 → 可交易
   - **TTR（紧密交易区间）**：不满足上述条件 → 不交易（p871/p1035，c30）
   - **BOM（突破模式）**：TR 末期出现方向性突破迹象 → 等待确认，见 `breakout-transition`

2. **确定买卖区**（⚠️ 两种口径，先判状态再选）：
   - **显式映射（if-else）**：
     - `if 状态 == 纯 TR（无主导趋势腿）` → 用区间口径：买区 = 区间下 1/3，卖区 = 区间上 1/3
     - `elif 状态 == 牛趋势/牛通道中的回调` → 用腿口径：买区 = 最近上涨腿的下 2/3（卖区不适用，顺势段不逆势卖）
     - `elif 状态 == 熊趋势/熊通道中的反弹` → 用腿口径：卖区 = 最近下跌腿的上 2/3（买区不适用）
     - `else 状态未判定` → 判停，先调用 `market-cycle-diagnosis`，不得默认任一口径
   - **纯 TR 中**（p827/p872）：
     - 买区 = 区间下 1/3（TR_low 到 TR_low + 1/3 × TR_height）
     - 卖区 = 区间上 1/3（TR_high - 1/3 × TR_height 到 TR_high）
   - **趋势中的回调阶段**（p28，原文 `bottom 2/3rd of most recent leg up`）：
     - 买区 = 最近上涨腿的下 2/3（leg_low 到 leg_low + 2/3 × leg_height）
     - 卖区 = 最近下跌腿的上 2/3（leg_high - 2/3 × leg_height 到 leg_high）
   - ⚠️ 两种口径不可混用：必须先判定当前是"纯 TR"还是"趋势中的回调"，再选择对应公式

3. **应用 80% 规则**（p812 reviewed + p394/p786/p828/p1004/p1012/p1015 多源）：
   - TR 中 80% 的突破失败（作者断言，无统计口径）
   - 操作含义：默认 fade 突破，用限价单在买卖区入场
   - BLSHS（Buy Low Sell High Scalp）：买低下卖高并剥头皮

4. **订单类型**（p827/p872）：
   - TR 是限价单市场：用限价单赌突破失败
   - 第二次入场信号优于第一次
   - 止损单在 TR 中效果差（容易被假突破触发）

5. **TR 终结预期**（p875）：
   - 每个 TR 最终以趋势结束
   - TR 末期关注 BOM 信号与方向性突破确认

6. **判停点**：
   - TTR → 判停：不交易（c30），除非满足严格条件
   - 信息不足以判定 TR 边界 → 暂停结论，要求补充数据
   - 用户要求在 TR 中追突破 → 警告 80% 失败率（c35）

### 输出契约

| 字段 | 类型 | 说明 |
|------|------|------|
| tr_subtype | enum | normal_TR / TTR / BOM |
| buy_zone | price_range | 买区价位范围 + 所用口径声明 |
| sell_zone | price_range | 卖区价位范围 + 所用口径声明 |
| order_type | string | 建议订单类型（limit / stop） |
| bo_failure_rate | string | "80%（作者断言，无统计口径）" |
| warnings | list | 禁止事项与风险提示 |

## B

**反场景**：
- 当 TR 中出现连续 5+ 根强同向 K 线且收盘超越边界时，可能已进入突破阶段，转 `breakout-transition`
- 当 TR 高度缩小至 TTR 标准以下时，停止交易

**作者警告的失败模式**：
- c35：TR 中 80% 的突破会失败（p812）
- c45：TR 中概率接近 50%，好设置常失败、坏设置常成功（p815-816）
- c30：紧 TR 尾盘不应交易（p1035）
- 把趋势中的高概率设置直接搬到 TR 中使用是常见错误

**批判盲点**：
- 80% 为作者断言，无样本期/样本量/计算方法
- TTR 的量化边界仍较模糊，绑定 Emini 品种
- 买卖区两种口径（1/3 vs 2/3）的切换条件材料未给显式规则，依赖状态诊断
- TR 中概率结构（~50%）意味着单笔结果的信息量极低

【全局边界 · 适用于本 Skill 全部能力】
1. 本书所有百分比（10/40/50/60/70/75/80/90%）均为作者 Al Brooks 的主观断言，材料未提供样本期、样本量、置信区间或计算方法；不得表述为客观概率或历史统计结果。
2. 所有硬数字（最小剥头皮尺度、时段窗口、K 线序号、Tick 阈值）绑定 Emini 5 分钟图与美股交易时段；用于 A 股、外汇、加密货币等其他市场时须自行重新标定，本 Skill 不提供换算方法。
3. 「强突破 / 强对手方 / 强信号 K 线 / 足够买卖压」等限定词在材料中无量化门槛，属作者定性判断；应列出可观察特征并说明判定不确定性，不得断言确定性结论。
4. 书中案例图均为事后复盘（右侧走势已知），不得据此推导胜率或期望值。
5. 本 Skill 只承载作者主张的规则与口径，用于方法论检索与结构化分析；不构成投资建议，不预测市场，不给出买卖指令。用户据此交易的盈亏与本 Skill 无关。
6. 作者方法存在根本软肋：入场规则的可证伪性弱（「任何 K 线都能入场」+「止损与入场点无关」），单次结果不能证实或证伪规则；连续亏损时应提示用户复核前提，而非继续套用同一规则。

## 图文证据

涉及图形、编号或图文对应时，先实际打开完整图与核查记录，再按需放大局部。当前宿主不能看图时说明限制；记录中的推断不能冒充图中事实。

- 图例 fig-tr-80pct — 来源 src-brooks-htpa，PDF 页序 812，书本页码 未核对；源文件 SHA256 `02e6d9cca2ffabd977ecd63c2944d1a73652dc3649cbb6cada90d3e2d50a79da`
  - [完整图](../../resources/figures/trading-range/page-0812.png) · [图文核查记录](../../resources/figures/trading-range/figure-notes.md)

## 配套资源

路径相对于本文件；脚本需先检查运行条件，不因附带而自动执行。

- [resources/figures/trading-range/page-0812.png](../../resources/figures/trading-range/page-0812.png)
- [resources/figures/trading-range/page-0812.txt](../../resources/figures/trading-range/page-0812.txt)
- [resources/figures/trading-range/figure-notes.md](../../resources/figures/trading-range/figure-notes.md)
