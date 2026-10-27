# task.md — 阅读任务锁定（正式回答前写入）

锁定时间：2026-10-27（Asia/Shanghai）。本文件在正式回答前写入，之后不改动任务定义；如有修订在 verification.md 记录。

## 本次阅读问题（唯一）

**论文如何支持“传播振动（propagating vibrational excitations）贡献近乎全部热导”的判断？**

要求重建其证据产生和推断过程：解释所用方法、关键条件及外推边界，并判断这项结果能支持读者怎样理解或使用无定形碳的热输运结论。

## 材料范围

| 材料 | 标识 | 状态 |
| --- | --- | --- |
| 主文 PDF（用户上传附件，实际可读取路径 `D:\Downloads\s41524-025-01625-2.pdf`） | SHA-256 = A2C5F62D0A618CFA460B0DA0E404520123A5B184AC84CE9490CB38E1250F1E72，2,860,002 字节，8 页 | 已读全文；重点第 3–6 页（图 3、图 4、Methods） |
| 补充材料（SI） | https://static-content.springer.com/esm/art%3A10.1038%2Fs41524-025-01625-2/MediaObjects/41524_2025_1625_MOESM1_ESM.pdf，2026-10-27 取得 | 已读（经 web_fetch 提取文本，部分字符乱码已标注） |
| nature.com 文章页 HTML | https://www.nature.com/articles/s41524-025-01625-2，2026-10-27 取得 | 用于核对网页版与 PDF 一致性及 SI 链接 |
| Skill：paper-evidence-reader | `C:\Users\Administrator\.bohrium\skills\paper-evidence-reader\`，SKILL.md SHA-256 = 028228B1CC60EB66D3D0EFEE99DD3070BF0C80F26172785425A7791F3F892394（版本标识无法取得，ATTRIBUTION.md 见 skill/ 副本） | 已加载并遵循；附 4 个 references（哈希见 records/hashes.md） |

论文版本标识：PDF 页脚 “npj Computational Materials | (2025)11:137”，DOI 10.1038/s41524-025-01625-2，Received 9 January 2025 / Accepted 26 April 2025；未检出更正或更新标记（“Check for updates” 链接未显示更新内容）。许可：CC BY-NC-ND 4.0（© The Author(s) 2025）。

## 验收标准

1. **关键解读可定位**：每条关键结论附 PDF 页码、章节、图号/子图或公式号。
2. **关键分析的解释完整**：热导计算、频谱分解、量子修正、传播/扩散判据、色散分析，各自说明实际输入 → 操作 → 输出 → 用途，不只列工具名。
3. **定量结论限定明确**：“近乎全部”的对象（热导贡献比例，非模式数量比例）、分母、频率范围、温度、结构/密度条件写清；图中读数为估读并标注。
4. **三类陈述分开**：论文原述（连续准确引句或标转述）、AI 推断、未知/未决。
5. **过程留痕**：真实首次输出存 `outputs/ai_raw.md`；核查记录存 `verification.md`；修订版存 `outputs/ai_revised.md`，不覆盖首次输出。
6. **提取预算**：分享材料中提取文本总量 ≤ 240 KiB，目标 < 200 KiB。

## 不做的事（本轮边界）

不创建/发布 GitHub 仓库，不提交比赛，不虚构链接/Release/commit；不宣称优于无 Skill 的对照（本次无公平对照）；不以 AI 摘要替代原文材料。
