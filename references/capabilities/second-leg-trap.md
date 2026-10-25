## R

> Strong 2nd Leg Is Trap: Hopeful Beginner Bets on Trend. 2nd Leg Trap: strong 2nd Leg reverses instead of leading to a Measured Move (MM). Beginner sees strong 2nd Leg Up and buys, expecting Measuring Gap (MG) and MM up. (Video 47C, PDF p833)

TR 或倾斜通道中强劲的第二条腿常是陷阱：它反转而非等距延续。初学者看到强第二条腿后追入，预期测量缺口和等距目标，结果被套。（p833 渲染核对，reviewed；仍为作者断言）

## I

第二条腿陷阱是 TR 和宽通道中最主要的盈利来源之一，也是初学者最常踩的坑。机制是：当市场处于 TR 或倾斜通道时，一条看似强劲的第二条腿让初学者误以为趋势启动，纷纷追入 expecting Measured Move。但因为没有真正的突破动能，这条腿在等距位置附近反转，套住所有追入者。专家识别这个模式后反向操作——fade 突破，赌被套者的被迫平仓成为反转燃料。图上标注了四类被套入场点（p833 reviewed）。反转入场需要宽止损或加仓，作者明确只建议专家使用（c26/c27）。

## A1

**worked_example · retrospective: true**

来源：case05（Video 49A, PDF p1058）+ case30（Video 51D, PDF p1327）。

case05 展示抛物线楔形顶后的空头突破失败形成 DB 结构，其中第二条腿的失败是核心机制。case30 展示 TR 中看似强劲的牛腿但无跟随，在等距位置附近反转下行。两案共同例证了 c05（2nd Leg Trap：TR 中强腿是假突破）。

回顾要点：p833 渲染图（reviewed）清晰标注四类被套入场点：①跟随 K 线收盘买入 ②大阳 K 线收盘买入 ③突破后买入 ④DB 突破买入。注意这些均为事后复盘图，不得据此推导胜率。

## A2

触发场景：
1. 用户问「这是第二条腿陷阱吗 / Is this a 2nd leg trap」→ 执行陷阱判定
2. 用户问「能不能反向做这条腿 / Can I fade this leg」→ 专家可反向，初学者避免
3. 用户说「追了第二条腿就被套 / Bought 2nd leg and got trapped」→ 识别被套并处置
4. 用户问「为什么追腿就亏 / Why does chasing legs lose money」→ 解释陷阱机制
5. 用户问「怎么利用被套者 / How to exploit trapped traders」→ 专家反向操作（p839-841）

区分：
- 本卡不处理趋势中的正常第二条腿（Measured Move），见 `measured-move`
- 本卡不处理 TR 的一般操作规则，见 `trading-range`
- 本卡不处理被套后的处置细节，见 `trapped-disposal`

关键词：第二条腿陷阱 / 2nd leg trap / 假突破 / fade breakout / 反向 / 被套 / trapped traders

## E

### 输入契约

必需字段：
- K 线图或行情描述（含至少两条腿的完整走势）
- 当前市场状态判定（TR / 宽通道 / 趋势；若未提供，先调用 `market-cycle-diagnosis`）
- 用户经验水平（初学者 / 专家；影响是否建议反向操作）

缺失任一时询问用户，不得猜值。

### 步骤

1. **陷阱判定条件**（p639/p749-750/p833 reviewed）：
   - □ 当前处于 TR 或倾斜通道（非强趋势）
   - □ 出现强劲的第二条腿（腿 2 明显陡于腿 1）
   - □ 第二条腿接近等距位置但未有效突破 TR/通道边界
   - □ 缺乏后续跟随（bad follow-through）
   - ⚠️ "强"无量化门槛（nr-07）；图中以"腿 2 明显陡于腿 1"示意

   完成标准：≥3 个条件满足 → 高概率陷阱；2 个 → 警惕但不确定；≤1 → 可能是正常第二条腿。

2. **四类被套入场点识别**（p833 reviewed）：
   - ① 跟随 K 线收盘买入（Beginner buys close of follow-through bar）
   - ② 大阳/阴 K 线收盘买入（Beginner buys close of big bull/bear bar after BO）
   - ③ 突破后买入（Beginner buys BO after strong rally）
   - ④ DB 突破买入（Beginner buys BO from DB）

3. **操作指引**（按经验水平分层）：
   - **初学者**：识别陷阱后不参与，等待明确的方向确认后再交易
   - **专家**（p839-841）：fade 突破，赌被套者被迫平仓
     - 反转入场时机：在第 3 或第 4 根反向 K 线收盘时卖出/买入
     - ⚠️ 宽止损/加仓仅专家提示（c26/c27）：初学者禁止加仓或使用宽止损

4. **判停点**：
   - 当前处于强趋势（非 TR/宽通道）→ 不适用本卡，第二条腿可能是正常的 MM
   - 用户为初学者且要求反向操作 → 判停：引用 c26/c27
   - 信息不足以判定状态 → 暂停结论，要求补充数据

### 输出契约

| 字段 | 类型 | 说明 |
|------|------|------|
| trap_likelihood | enum | high / medium / low / not_applicable |
| trapped_entry_types | list | 已识别的被套入场点类型 |
| action_by_level | table | 初学者/专家分别的操作建议 |
| warnings | list | 风险提示与能力门槛 |

## B

**反场景**：
- 当第二条腿有效突破 TR/通道边界且有强跟随时，不是陷阱而是真突破
- 在强趋势中，第二条腿通常是 Measured Move 的正常组成部分，不应 fade

**作者警告的失败模式**：
- c05：TR 中强腿是假突破（p833-835）
- c04：初学者买高卖低被困（p836-837）
- c26：初学者不应加仓或使用宽止损（p849）
- c27：加仓的风险收益比极差，仅专家可为（p447-449）
- 反转入场依赖宽止损或加仓，管理能力不足时使用会导致更大亏损

**批判盲点**：
- "强第二条腿"的强度无量化门槛（nr-07 型缺口）
- 陷阱判定依赖状态诊断（TR vs 趋势），而状态诊断本身有模糊地带
- p833 图上仅展示三次成功示例，不得据此推导概率
- 专家反向操作的胜率材料未给，仅定性描述为"betting on trapped traders"

【全局边界 · 适用于本 Skill 全部能力】
1. 本书所有百分比（10/40/50/60/70/75/80/90%）均为作者 Al Brooks 的主观断言，材料未提供样本期、样本量、置信区间或计算方法；不得表述为客观概率或历史统计结果。
2. 所有硬数字（最小剥头皮尺度、时段窗口、K 线序号、Tick 阈值）绑定 Emini 5 分钟图与美股交易时段；用于 A 股、外汇、加密货币等其他市场时须自行重新标定，本 Skill 不提供换算方法。
3. 「强突破 / 强对手方 / 强信号 K 线 / 足够买卖压」等限定词在材料中无量化门槛，属作者定性判断；应列出可观察特征并说明判定不确定性，不得断言确定性结论。
4. 书中案例图均为事后复盘（右侧走势已知），不得据此推导胜率或期望值。
5. 本 Skill 只承载作者主张的规则与口径，用于方法论检索与结构化分析；不构成投资建议，不预测市场，不给出买卖指令。用户据此交易的盈亏与本 Skill 无关。
6. 作者方法存在根本软肋：入场规则的可证伪性弱（「任何 K 线都能入场」+「止损与入场点无关」），单次结果不能证实或证伪规则；连续亏损时应提示用户复核前提，而非继续套用同一规则。

## 图文证据

涉及图形、编号或图文对应时，先实际打开完整图与核查记录，再按需放大局部。当前宿主不能看图时说明限制；记录中的推断不能冒充图中事实。

- 图例 fig-second-leg-trap — 来源 src-brooks-htpa，PDF 页序 833，书本页码 未核对；源文件 SHA256 `02e6d9cca2ffabd977ecd63c2944d1a73652dc3649cbb6cada90d3e2d50a79da`
  - [完整图](../../resources/figures/second-leg-trap/page-0833.png) · [图文核查记录](../../resources/figures/second-leg-trap/figure-notes.md)

## 配套资源

路径相对于本文件；脚本需先检查运行条件，不因附带而自动执行。

- [resources/figures/second-leg-trap/page-0833.png](../../resources/figures/second-leg-trap/page-0833.png)
- [resources/figures/second-leg-trap/page-0833.txt](../../resources/figures/second-leg-trap/page-0833.txt)
- [resources/figures/second-leg-trap/figure-notes.md](../../resources/figures/second-leg-trap/figure-notes.md)
