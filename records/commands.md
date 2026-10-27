# records/commands.md — 本次阅读的真实操作记录（2026-10-27）

按时间顺序，仅记录支撑本次结论的关键操作；PowerShell 在临时目录 `$env:TEMP\paperead-0372ec…` 中完成提取与渲染。

## 1. Skill 与材料确认

- 枚举 `C:\Users\Administrator\.bohrium\skills\paper-evidence-reader\` 全部文件并计算 SHA-256（结果见 hashes.md）。
- 逐一读取 SKILL.md、references/method.md、decision.md、problem.md、code.md（未修改）。
- `Test-Path D:\Downloads\s41524-025-01625-2.pdf` → 存在；Get-FileHash → A2C5F6…F1E72（2,860,002 B）。

## 2. PDF 提取与页数核对

- `pdfinfo` → **命令不存在**（工具缺失，未重试同名方案）。
- `pdftotext -layout <pdf> paper.txt` → 63,599 B。
- 页数：对 paper.txt 数换页符 `` `f `` → 8 页；与页脚“npj Computational Materials | (2025)11:137”第 1–8 页一致。
- 题名/DOI/作者：提取文本第 1 页与页眉 DOI 逐页一致；版本标识 (2025)11:137；Received 9 January 2025 / Accepted 26 April 2025；许可 CC BY-NC-ND 4.0（第 8 页）。

## 3. 原页渲染（处理双栏/公式/图）

- `pdftoppm -png -r 150 -f 3 -l 4 <pdf> page` → page-3.png、page-4.png（查看图 3、图 4 及上下文）。
- `pdftoppm -png -r 300 -f 4 -l 4 -x 1250 -y 1260 -W 1170 -H 160 … drw` → 放大确认 $D_{RW}=\frac13\frac{\omega}{\pi n^{2/3}}$（解决 pdftotext 乱码“DRW ¼ 13 πnω2=3”）。
- `pdftoppm -png -r 200 -f 4 -l 4 -x 130 -y 90 -W 480 -H 820 … fig4ab` → 图 4A/B 箭头 ω_L,c、ω_T,c 估读。
- `pdftoppm -png -r 300 -f 4 -l 4 -x 260 -y 1820 -W 920 -H 720 … fig4c` → 图 4C 中 λ=a 交叉点估读。
- 注：pdftoppm 的 -x/-y/-W/-H 以输出分辨率下的像素计；fig4ab 裁剪的偏移量凭页面布局近似给定，经读图确认已覆盖目标区域；所有估读均以图内坐标轴刻度重新标定，不依赖裁剪坐标。

## 4. 补充材料获取

- web_fetch `https://www.nature.com/articles/s41524-025-01625-2`（2026-10-27）→ 文章页提取 104,618 字符，用于定位 SI 锚点并抽查网页版与 PDF 一致性。
- web_fetch `https://static-content.springer.com/esm/art%3A10.1038%2Fs41524-025-01625-2/MediaObjects/41524_2025_1625_MOESM1_ESM.pdf`（2026-10-27）→ SI 提取 7,171 字符（图 S1–S4 说明；系统性字符损失已标注）。SI 原始 PDF 二进制未下载，只有提取文本。

## 5. 写作顺序（与 task.md 约定一致）

1. task.md（锁定）→ 2. prompts/prompt-original.md → 3. outputs/ai_raw.md（首版）→ 4. 独立核查（回查提取文本 + 原页渲染，逐项判定）→ verification.md → 5. outputs/ai_revised.md → 6. README/environment/records。
- ai_raw.md 写入后未被覆盖；ai_revised.md 为单独文件。

## 6. 遇到的问题与解决（摘要）

| 问题 | 解决 |
| --- | --- |
| pdfinfo 缺失 | 换页符计数 + 页脚核对 |
| 双栏行内公式乱码（$D_{RW}$ 等） | 300 dpi 局部放大人工核对 + 量纲检验 |
| SI 字符损失 | 只按语义引用，标注有损 |
| 图内无数值 | 全部标“估读”，关键估读给出像素标定依据 |
