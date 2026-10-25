## R

> Stop Is Same: No Matter Where You Buy. Location of stop does not depend on where you enter. (Video 41A, PDF p269; 同义重申于 p335/p475/p557)

> Base Stop: On 2x Size of Biggest Prior BO. Put stop at 2x size of prior biggest BO. (Video 45D, PDF p646)

止损位与入场点无关——同一笔交易无论从哪入场，止损位相同。Base Stop 设在此前最大突破幅度的 2 倍之外（p646 渲染核对，reviewed；仍为作者断言）。

## I

止损是交易者方程的风险端输入，也是三重保护之首。作者四次重申「止损与入场点无关」，这意味着止损位由市场结构决定（腿底、信号 K 线极值、此前最大突破幅度），而非由你的入场价决定。Initial Risk 是入场到初始止损的距离，Actual Risk 是入场到实际最大不利价的距离；低概率交易用 Actual Risk 计算回报倍数，高概率交易可用 Initial Risk 替代。追踪止损在每次新的强突破后移至腿底。Skunk Stop（两个好选择之间的坏折中）被明确禁止。止损远就缩小仓位，而不是放宽止损或放弃交易。

## A1

**p646 Base Stop 图证教学示例**（p646 渲染核对，reviewed；仍为作者断言，绑定 Emini）

原图（`resources/figures/stop-placement/page-0646.png`）展示 Emini 日线级多日图（横轴 2/12–2/26）：
- 此前最大突破幅度 = 17 ticks
- Base Stop = 2 × 17 ticks ≈ 35–36 ticks
- 图上另有 10 tick BO 标注作为对比

此示例数值经渲染核对为真，可用作教学演示。注意：该止损用于趋势内逆势/加仓持仓的宽止损，非标准摆动止损；回溯窗口（多少根 K 线/多少天内算「prior」）图上未标，仍属未定义（nr-05 遗留）。

## A2

触发场景与用户语言信号：

1. 用户问「止损放哪 / 止损设多远」→ 计算止损位与风险值
   - 关键词：止损 / stop / stop placement / risk
2. 用户问「Initial Risk 和 Actual Risk 区别」→ 解释并计算两者
   - 关键词：Initial Risk / Actual Risk / 初始风险 / 实际风险
3. 用户问「怎么移动止损 / 追踪止损」→ 给出移动触发清单
   - 关键词：追踪止损 / trailing stop / 移动止损 / move stop
4. 用户给出入场价和止损价 → 计算风险值并校验交易者方程
   - 关键词：入场 / entry / 止损价 / stop price
5. 用户问「能不能用心理止损」→ 明确禁止并解释原因
   - 关键词：心理止损 / mental stop / 不设止损

区分：
- 本卡不处理出场触发条件，见 `protection-exit`
- 本卡不处理交易者方程的概率端，见 `traders-equation`
- 本卡不处理加仓时的仓位缩放，见 `scale-in`

## E

### 输入契约

| 字段 | 类型 | 必需 | 说明 |
|------|------|------|------|
| 入场价 | 数值 + 单位 | 是 | 实际或计划入场价 |
| 市场状态 | 枚举 | 是 | Strong BO / Channel / TR（影响止损类型选择） |
| 方向 | 枚举 | 是 | Long / Short |
| 近期 K 线结构 | 图表或描述 | 是 | 用于确定腿底/信号 K 线极值/此前最大 BO |

缺失必需字段时先询问，不得猜值。

### 步骤

1. **确定初始止损位**
   - 顺势交易：止损放在入场腿的底部（多头 = 腿低点下方 1 tick；空头 = 腿高点上方 1 tick）（p270/p557）
   - 逆势/加仓：使用 Base Stop = 2 × 此前最大突破幅度（p646/p763）
   - 完成标准：给出止损价

2. **计算 Initial Risk 与 Actual Risk**
   - Initial Risk = |入场价 − 初始止损价|
   - Actual Risk = |入场价 − 实际最大不利价|（通常为入场后价格最不利到达的点）
   - 若尚无 Actual Risk 数据，用 Initial Risk 代替并注明
   - 完成标准：给出两个风险值

3. **选择风险基准**
   - 低概率交易（≤50%）：用 Actual Risk 计算回报倍数（需 ≥2x）
   - 高概率交易（≥60%）：可用 Initial Risk 替代（需 ≥1x）（p36-37/p285/p478/p561）
   - 完成标准：标明所选基准及理由

4. **设定追踪止损移动触发**
   - 每次新的强突破后，尤其是创新高/新低时，将止损移至新腿底/腿顶（p151/p270/p635/p744）
   - 牛趋势：trail stop to below bottom of bull leg (major HL)
   - 熊趋势：trail stop to above top of last strong bear leg
   - 完成标准：给出当前止损位 + 下一次移动触发条件

5. **检查 Skunk Stop 禁令**
   - 确认止损不在「早期退出」和「正确摆动止损」之间的折中位置（p1316/c17）
   - 完成标准：确认止损属于两个合理选择之一

### 输出契约

```
初始止损价: [值] [单位]
Initial Risk: [值] [单位]
Actual Risk: [值] [单位]（若无则标注「暂用 IR 代替」）
风险基准: [Initial Risk | Actual Risk]（附理由）
当前追踪止损位: [值] [单位]
下次移动触发: [条件描述]
Skunk Stop 检查: [通过 ✓ | 警告 ⚠️]
⚠️ 禁止心理止损：必须有市场中的保护性止损单
```

### 判停

- 「强突破」无量化门槛（nr-07）；追踪止损的移动触发依赖定性判断
- Base Stop 的回溯窗口未定义（nr-05 遗留）；agent 应说明此缺口
- 所有硬数字绑定 Emini；其他品种须自行标定

## B

### 反场景

- 使用心理止损 → 一次巨大亏损抹掉 20 次盈利（c08）
- Skunk Stop：在两个好选择之间折中 → 两头不讨好，杀死账户（c17）
- 止损远但不缩小仓位 → 总风险失控（c14）
- 基于小周期止损 → 被噪音扫出错失大利润（c16）

### 作者警告

- c08：心理止损保护的是自尊心而非账户；结果是一次巨大亏损抹掉最近 20 次盈利
- c17：Skunk Stop 是两个好选择之间的坏折中；路中间的臭鼬会被撞死。要么早期果断退出，要么用正确的摆动止损配合小仓位
- c14：止损远时必须按比例缩小仓位；若无法交易那么小，就不要做这笔交易
- c16：在哪张图入场就在哪张图做决策；切换到小周期管理是被恐惧驱动的必亏之路

### 批判层盲点

- Base Stop 公式的「prior biggest BO」回溯窗口未定义（nr-05 遗留）；图上仅示意最近两段突破，无明确时间/K 线数范围
- 「强突破」用于触发追踪止损移动，但无量化门槛（nr-07）
- Initial Risk vs Actual Risk 的切换边界只有定性描述，无量化条件
- p646 示例数值（17 ticks → 35–36 ticks）经渲染核对为真，但绑定 Emini（nr-09）

【全局边界 · 适用于本 Skill 全部能力】
1. 本书所有百分比（10/40/50/60/70/75/80/90%）均为作者 Al Brooks 的主观断言，材料未提供样本期、样本量、置信区间或计算方法；不得表述为客观概率或历史统计结果。
2. 所有硬数字（最小剥头皮尺度、时段窗口、K 线序号、Tick 阈值）绑定 Emini 5 分钟图与美股交易时段；用于 A 股、外汇、加密货币等其他市场时须自行重新标定，本 Skill 不提供换算方法。
3. 「强突破 / 强对手方 / 强信号 K 线 / 足够买卖压」等限定词在材料中无量化门槛，属作者定性判断；应列出可观察特征并说明判定不确定性，不得断言确定性结论。
4. 书中案例图均为事后复盘（右侧走势已知），不得据此推导胜率或期望值。
5. 本 Skill 只承载作者主张的规则与口径，用于方法论检索与结构化分析；不构成投资建议，不预测市场，不给出买卖指令。用户据此交易的盈亏与本 Skill 无关。
6. 作者方法存在根本软肋：入场规则的可证伪性弱（「任何 K 线都能入场」+「止损与入场点无关」），单次结果不能证实或证伪规则；连续亏损时应提示用户复核前提，而非继续套用同一规则。

## 图文证据

涉及图形、编号或图文对应时，先实际打开完整图与核查记录，再按需放大局部。当前宿主不能看图时说明限制；记录中的推断不能冒充图中事实。

- 图例 fig-base-stop — 来源 src-brooks-htpa，PDF 页序 646，书本页码 未核对；源文件 SHA256 `02e6d9cca2ffabd977ecd63c2944d1a73652dc3649cbb6cada90d3e2d50a79da`
  - [完整图](../../resources/figures/stop-placement/page-0646.png) · [图文核查记录](../../resources/figures/stop-placement/figure-notes.md)

## 配套资源

路径相对于本文件；脚本需先检查运行条件，不因附带而自动执行。

- [resources/figures/stop-placement/page-0646.png](../../resources/figures/stop-placement/page-0646.png)
- [resources/figures/stop-placement/page-0646.txt](../../resources/figures/stop-placement/page-0646.txt)
- [resources/figures/stop-placement/figure-notes.md](../../resources/figures/stop-placement/figure-notes.md)
