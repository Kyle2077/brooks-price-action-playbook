# 能力索引（完整版）

| capability_id | 标题 | 重要度 | 意图 | 关键词 | 能力卡 |
|---|---|---|---|---|---|
| cap.brooks-htpa.market-cycle-diagnosis | 市场周期状态诊断（突破→通道→TR→再突破） | critical | 判断现在是什么市场状态；这是趋势还是震荡；图上是突破还是通道；market cycle state；trend or trading range | 市场周期、market cycle、突破、breakout、通道、channel、交易区间、trading range、状态诊断 | capabilities/market-cycle-diagnosis.md |
| cap.brooks-htpa.always-in-direction | Always In 方向判定（多/空/中性与翻转触发） | critical | 现在市场偏多还是偏空；Always In 是哪个方向；该做多还是做空；always in long or short；direction bias | Always In、AIL、AIS、方向、bias、多空、翻转 | capabilities/always-in-direction.md |
| cap.brooks-htpa.traders-equation | 交易者方程与 40-60 规则（这笔值不值得做） | critical | 这笔交易值不值得做；盈亏比够不够；概率和回报怎么配；trader's equation；risk reward probability | 交易者方程、trader's equation、40-60、期望、盈亏比、risk reward、probability | capabilities/traders-equation.md |
| cap.brooks-htpa.stop-placement | 止损设置与追踪（Initial/Actual Risk、Base Stop、移动规则） | critical | 止损放哪；止损设多远；怎么移动止损；initial risk actual risk；stop placement trailing | 止损、stop、Initial Risk、Actual Risk、追踪止损、trailing stop、Base Stop、Skunk Stop | capabilities/stop-placement.md |
| cap.brooks-htpa.profit-targets | 利润目标与分批获利（2x 减半 / 3x 再减 25% / 摆动剩余） | high | 目标看多少；什么时候止盈；怎么分批获利；profit target；take profit scaling out | 利润目标、profit target、止盈、分批、scale out、2x risk、measured move 目标 | capabilities/profit-targets.md |
| cap.brooks-htpa.tight-channel | 紧通道识别与操作（只顺势，6 特征清单） | high | 这是紧通道吗；紧通道怎么做；能不能逆势；tight channel；micro channel | 紧通道、tight channel、微通道、micro channel、只顺势、逆势必亏 | capabilities/tight-channel.md |
| cap.brooks-htpa.broad-channel | 宽通道识别与操作（90% 的 K 线等同倾斜 TR） | high | 这是宽通道吗；宽通道怎么做；能不能双向；broad channel；sloped trading range | 宽通道、broad channel、倾斜TR、双向、深回撤、50% PB | capabilities/broad-channel.md |
| cap.brooks-htpa.trading-range | TR / TTR / BOM 识别与操作（80% 规则、买卖区、限价单市场） | high | 这是震荡区间吗；TR 怎么做；TTR 能不能交易；trading range；80% rule | 交易区间、trading range、TR、TTR、BOM、80% 规则、买卖区、buy zone、sell zone、限价单市场 | capabilities/trading-range.md |
| cap.brooks-htpa.breakout-transition | 突破阶段结束识别与方法切换（含前提改变则改风格） | high | 突破结束了吗；什么时候换方法；风格要不要切换；breakout phase end；premise change | 突破结束、方法切换、premise change、跟随不足、bad follow-through、风格切换 | capabilities/breakout-transition.md |
| cap.brooks-htpa.strong-bo-entry | 强突破入场（Buy/Sell The Close，只顺势） | high | 突破来了怎么追；BTC/STC 是什么；强突破能不能等回调；buy the close；breakout entry | 强突破、strong breakout、Buy The Close、Sell The Close、BTC、STC、追突破 | capabilities/strong-bo-entry.md |
| cap.brooks-htpa.mtr-reversal | MTR 主要趋势反转验证（三要素 + 腿部量化条件） | high | 这是主要反转吗；MTR 成立吗；能不能抄底/摸顶；major trend reversal；HH LL MTR | MTR、主要趋势反转、HH MTR、LL MTR、LH MTR、HL MTR、反转验证、gap bar | capabilities/mtr-reversal.md |
| cap.brooks-htpa.climax-reversal | 高潮识别与反向操作（Buy/Sell Climax、Micro Channel、TBTL 60/70 分档） | high | 这是高潮吗；能不能反向做；TBTL 是什么；climax；buy climax sell climax | 高潮、climax、Buy Climax、Sell Climax、微通道高潮、TBTL、Ten Bars Two Legs、反向 | capabilities/climax-reversal.md |
| cap.brooks-htpa.second-leg-trap | 第二条腿陷阱识别与反向（专家赌被套者） | high | 这是第二条腿陷阱吗；能不能反向做这条腿；2nd leg trap；为什么追腿就亏 | 第二条腿陷阱、2nd leg trap、假突破、fade breakout、反向、被套 | capabilities/second-leg-trap.md |
| cap.brooks-htpa.measured-move | Measured Move 目标计算（腿等距 / 缺口测量，双语义基准） | medium | 目标怎么算；等距测量；measured move；缺口测量；measuring gap | Measured Move、MM、等距、腿1=腿2、measuring gap、exhaustion gap | capabilities/measured-move.md |
| cap.brooks-htpa.bar-counting-entry | K 线计数入场信号（High/Low 1-4） | medium | High 2 是什么意思；怎么数回调；bar counting；High 1 High 2 入场 | K线计数、bar counting、High 1、High 2、High 3、Low 1、Low 2、入场信号 | capabilities/bar-counting-entry.md |
| cap.brooks-htpa.intraday-structure | 日内三段结构与时段规则（开盘/中段/尾段 + 当日高低点概率） | high | 现在算日内哪个时段；尾盘怎么做；当日高低点形成了吗；intraday structure；end of day | 日内结构、intraday、开盘、中段、尾段、end of day、当日高低点、12:00-12:35 | capabilities/intraday-structure.md |
| cap.brooks-htpa.opening-playbook | 开盘剧本（BOM / 前 18 根 K 线 / 开盘反转 / 50% 反转口径） | high | 开盘怎么做；BOM 是什么；开盘突破能追吗；opening range；breakout mode | 开盘、open、BOM、breakout mode、开盘反转、opening reversal、前18根、bar 18 | capabilities/opening-playbook.md |
| cap.brooks-htpa.magnet-levels | 磁体位识别（昨日 H/L/C + 更高时间框架支撑阻力 + 缺口） | medium | 关键价位在哪；磁体位怎么找；昨日高低点有什么用；magnet levels；support resistance | 磁体、magnet、昨日高点、昨日低点、支撑、阻力、缺口、support、resistance | capabilities/magnet-levels.md |
| cap.brooks-htpa.timeframe-combination | 时间框架组合（高周期找形态、低周期降风险） | medium | 用哪个周期看；两个周期矛盾怎么办；timeframe；higher time frame | 时间框架、timeframe、高周期、低周期、60分钟、5分钟、分形、fractal | capabilities/timeframe-combination.md |
| cap.brooks-htpa.scale-in | 加仓（Scale In）决策：概率换风险，先算最坏情形 | high | 能不能加仓；加仓步长怎么定；scale in；摊平对不对 | 加仓、scale in、摊平、最坏情形、仓位、position size | capabilities/scale-in.md |
| cap.brooks-htpa.protection-exit | 三重保护与出场触发（禁心理止损 / 相反信号 / 止损 / 收盘） | critical | 什么时候出场；止损被打掉怎么办；三重保护是什么；exit rules；mental stop | 三重保护、出场、exit、心理止损、mental stop、相反信号、动量退出、收盘退出 | capabilities/protection-exit.md |
| cap.brooks-htpa.trapped-disposal | 被套/失望处置决策（提前出场 / 保本退出 / 看不懂先退） | high | 我被套了怎么办；要不要保本出；看不懂行情怎么办；trapped；disappointed | 被套、trapped、失望、disappointed、保本退出、breakeven、先退出 | capabilities/trapped-disposal.md |
| cap.brooks-htpa.psychology-sizing | 心理偏差自查与仓位控制（目标混淆 / 拒绝认错 / I Don't Care Size） | high | 为什么我总是亏；目标混淆怎么办；仓位多大合适；trading psychology；I don't care size | 心理、psychology、目标混淆、拒绝认错、FOMO、I Don't Care Size、仓位校准、坏管理 | capabilities/psychology-sizing.md |
