# 图证核查记录 — base-stop（p646）

- figure_id: fig-base-stop
- source_id: src-brooks-htpa（source_sha256 见 manifest.json）
- pdf_page: 646（Video 45D Slide 14）
- review_status: reviewed（2026-10-24 实际打开完整渲染图核对）

## 可见事实

- 标题：`Base Stop: On 2x Size of Biggest Prior BO`
- 规则原文（绿色）：`Selling in bull trend / Must get out if BO becomes too big / Put stop at 2x size of prior biggest BO`
- **示例数值在图上清晰可读**（解决 nr-05 的 OCR 疑虑）：
  - `Biggest prior BO was 17 ticks`
  - `Put stop just beyond 2x 17 ticks, so maybe 35 – 36 ticks`
  - 图上蓝色块标注 `10 tick BO` 与 `17 ticks` 两段先前突破幅度
- 入场标注（红色）：`Sell at prior high`
- K 线：Emini 日线级多日图（横轴 2/12–2/26），非 5 分钟图。

## 作者解释对应

- 与 p763（镜像：熊趋势中多头的 Base Stop）同源公式。
- 该止损用于**趋势内逆势/加仓持仓的宽止损**，非标准摆动止损；与 f20/p30「止损与入场点无关」不冲突，因 p30 针对顺势同向交易的腿底止损。

## 推断（标记为推断）

- 「prior biggest BO」的回溯范围（多少根 K 线/多少天内）图上未标，仅示意最近两段突破。回溯窗口仍属未定义（保留在卡片 B 段）。

## 缺口/冲突

- 回溯窗口未定义（保留）。
- 示例数值（17 ticks → 35–36 ticks）已**经渲染核对为真**，可用于教学示例，但绑定 Emini（nr-09）。
