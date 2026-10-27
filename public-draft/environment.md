# environment.md — 实际模型、环境、工具与投入

记录时间：2026-10-27。只记录真实可见信息；无法取得处如实标注。

## 平台与运行环境

- 平台：玻尔（Bohrium）科学空间，SciMaster 代理会话。
- 工作目录：`E:\bor\gzkj`（会话临时目录；案例目录为其下 `amorphous-carbon-reading/`）。
- 操作系统：Windows 10.0.22631 x64；Shell：PowerShell（pwsh）；时区 Asia/Shanghai。
- 文件策略：workspace-write；审批策略：ask。本轮所有文件写入均在会话工作区内，未触发额外审批。
- Skill 发现与调用：用户在提示词中指定 `paper-evidence-reader`；会话以 skill_content 形式注入该 Skill 说明，并给出基目录 `C:\Users\Administrator\.bohrium\skills\paper-evidence-reader`；SKILL.md 与 4 个 references 经文件读取完整加载（哈希见 `records/hashes.md`）。Skill 无显式版本号字段，**版本无法取得**（只有 ATTRIBUTION.md，见 skill/ 副本）。Skill 未做任何修改。
- PDF 提供方式：用户本机路径 `D:\Downloads\s41524-025-01625-2.pdf` 在当前空间实际可读取（2,860,002 字节，SHA-256 A2C5F6…F1E72），已复制入 `materials/` 并二次校验哈希一致。

## 工具（真实使用）

| 工具 | 用途 | 备注 |
| --- | --- | --- |
| pdftotext（-layout） | PDF 全文提取 | 63,599 字节；双栏行内公式乱码若干 |
| pdftoppm（-png, 150/200/300 dpi） | 第 3、4 页整页渲染与局部放大 | 用于核对图 3/图 4 与乱码公式 |
| pdfinfo | 拟用于元数据 | **不可用**（未安装），改用换页符计数与页脚核对页数 |
| web_fetch | 抓取 nature.com 文章页与 SI PDF | 2026-10-27 取得；SI 提取有字符损失 |
| PowerShell Get-FileHash | SHA-256 校验 | 全部材料与输出 |

## 模型与投入

- 底层语言模型精确版本：**无法取得**（会话未暴露模型标识；不填 0，不推测）。
- 会话日志、token 用量与费用：**无法取得**（平台未向会话提供）。
- 网络：仅访问 nature.com 文章页与其静态 SI 地址，均成功；未访问其他站点用于正文结论。
- 人工投入：用户提供论文附件、阅读问题与验收标准；其余阅读、核查、整理为 AI 完成；**未经人类复核**。

## 已知限制

- SI 提取文本存在系统性字符替换（如 ~ →“⇠”），SI 引句按语义使用。
- 图内数值均为估读；无原始绘图数据（论文 Data availability：“available within the article and its Supplementary Information … from the corresponding author upon request”，第 6 页）。
