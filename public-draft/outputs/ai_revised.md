# outputs/ai_revised.md — 核查后修订版

- 修订时间：2026-10-27。基线：`ai_raw.md`（首次输出，原样保留）；核查依据：`../verification.md`（AI 自检，未经人类复核）。
- 相对首版的实质变化：(a) 纵/横向交叉频率归属改为“原文内部不一致，只引用区间”；(b) “~100%”改为“作者表述；按图 3C 估读 30 THz 以上残余约占百分之几到 ~10%”；(c) 补充横向清晰色散范围的正文/SI 口径差异；(d) λ 构造维持未知；(e) 修正一处行文缺陷并补入两处自验估算（QC 降幅、盒长截断）。

---

## 0. 回答：论文如何支持“传播振动贡献近乎全部热导”

判断链由**一条测量主线 + 一组交叉频率判据**闭合而成（全部为 300 K、NEP 机器学习势、110,592 原子熔淬结构、密度 3.0–3.5 g cm⁻³ 的模拟）：

1. HNEMD 直接从 MD 轨迹得到**频谱热导** κ(ω)（式 4），经量子修正（式 5）后得到总热导与累积函数 κ(<ω)。图 3C 显示累积在 ~30 THz 以上基本饱和。
2. 用三个物理模型把“传播→扩散”交叉频率 ω_c 定在 ~30–35 THz：ω⁻² 幂律失效（~32 THz，SI 自述仅为 ball park 估计）、传播波扩散率下限 $D_a=\frac13 v_D a$ 与扩散振动扩散率上限 $D_{RW}=\frac{\omega}{3\pi n^{2/3}}$ 的交点（~35 THz）（图 3D）。
3. 独立的色散分析（式 6–8 + 每波矢 DHO 拟合）显示清晰色散与远大于原子间距的平均自由程持续到同一频率区间（图 4）。
4. 闭合：ω_c 以下的振动是传播的，ω_c 以上几乎不贡献热导，故传播振动≈全部热导。【原述】“propagating vibrations below 30–35 THz dictate thermal transport (~100 % of thermal conductivity) in amorphous carbon at 300 K as demonstrated in Fig. 3C where thermal conductivity accumulation saturates at ~ 30 THz”（第 4 页 Discussion）。

注意：这是**热导量（W m⁻¹ K⁻¹）的份额**，不是振动模式数目的份额；按图 2 的 DOS（主峰 ~35–40 THz、延伸至 ~52 THz，估读），30 THz 以上的模式数目占相当份额，按模式计数传播模式占比远小于 100%。且按图 3C 估读，30→50 THz 间累积曲线仍有小幅爬升，残余贡献约占百分之几到 ~10%，故“~100%”应理解为“≥约九成”的近似表述而非精确值。

## 1. 证据重建（输入 → 操作 → 输出 → 用途）

### 1.1 热导计算与频谱分解（图 3A–C；式 1–4）

- **输入**：NEP 机器学习势（GPUMD）MD 轨迹。结构：110,592 原子金刚石 15,000 K 熔化 30 ps → 100 K ps⁻¹ 淬至 1000 K → 退火 1 ns → 100 K ps⁻¹ 冷至 300 K（NVT）；1 ns 平衡 + 2 ns 采样，步长 1 fs，每组 3 个初速重复（Methods，第 5 页）。
- **操作**：加均匀外力 $F_i^{ext}=F_e\cdot W_i$（式 1，$W_i$=原子维里张量；$F_e=2\times10^{-4}\ \AA^{-1}$ 保证线性响应），测热流 $J(t)=\sum_i W_i\cdot v_i$（式 2），由线性响应 $\langle J_\alpha\rangle=TV\sum_\beta\kappa_{\alpha\beta}F^e_\beta$（式 3）得 κ；频谱分解 $\kappa(\omega)=\frac{2}{VTF_e}\int Q(t)e^{i\omega t}dt$（式 4），$Q(t)=\sum_i\langle W_i(0)\cdot v_i(t)\rangle$。
- **输出**：总 κ（图 3A）、κ(ω)（图 3B）、累积 κ(<ω)（图 3C）。图 3C 中实线=量子、虚线=经典（由图 3B 图例约定与图 3A 终值对应确认）。
- **独立校验**：Green–Kubo 公式另算 κ，【原述】“Classical thermal conductivity from HNEMD and GK thermal conductivity are within the error bars of each other.”（第 3 页）。
- **为何此法**：GKMA/NMD 需对角化动力学矩阵，10⁵ 原子不可行（第 3–4 页）；代价是无法直接给简正模分类，传播/扩散判据只能借助物理模型——这决定了后文判据链条的形态。

### 1.2 量子修正（式 5）

- **操作**：$\kappa_Q(\omega)=\kappa(\omega)\frac{x^2e^x}{(e^x-1)^2}$，$x=\hbar\omega/k_BT$——经典热容换量子热容，只改频谱权重，不改轨迹。
- **效果**：【原述】“At 300 K, the quantum correction to the heat capacity reduces the classical thermal conductivities by as much as 30 to 40 %”；“becomes prominent above ~7 THz … $k_BT$ ~ 25 meV or 6 THz”（第 3 页）。自验（估读图 3A）：3.5 g cm⁻³ 处经典 ≈9.5–10、量子 ≈6–6.5 W m⁻¹ K⁻¹，降幅 ≈35%，吻合。
- **约束后果**：【推断】因子 $x^2e^x/(e^x-1)^2\le1$，方向确定——遗漏 QC 会使总 κ 高估 30–40%，并把份额推向高频，使“热导集中于 30 THz 以下”的闭合变差；对碳（Debye 温度 ~2300 K，第 2 页）在室温不可省略。

### 1.3 传播/扩散判据：三个物理模型（图 3D）

- **共同输入**：$D(\omega)=\kappa(\omega)/[C(\omega)\mathrm{DOS}(\omega)]$（第 4 页；κ 是否取量子修正版，正文未明示——未知）。DOS 来自速度自相关频谱分解（图 2）；Debye 拟合（<5 THz）得 v_D = 12.97 / 14.60 / 15.21 km s⁻¹（3.0 / 3.3 / 3.5 g cm⁻³）。
- **模型一**：传播波寿命/扩散率的 ω⁻² 幂律失效处即转变频率 → ~32 THz（第 4 页；SI 图 S1，SI 自述“not exact … ball park estimation”，有损提取、语义核对）。
- **模型二**（传播波下限）：$D_a=\frac13 v_D a$，统一取 v_D≈14 km s⁻¹ 平均、a=原子间距；图 3D 水平点线，量级 ~10⁻⁶ m² s⁻¹（估读；按 v_D=14 km s⁻¹、a≈1.5 Å 算得 ≈7×10⁻⁷，同量级）。
- **模型三**（扩散振动上限）：随机行走理论 $D_{RW}=\frac{\omega}{3\pi n^{2/3}}$（公式经 300 dpi 原页放大确认，量纲自洽），随频率线性上升；图 3D 黑色实线。
- **判据**：【原述】“If physically realistic, these two independent models should ideally merge at a certain frequency”；“Applying these two physical models leads to nearly identical crossover frequencies at ~35 THz in amorphous carbon as shown in Fig. 3D.”（第 4 页）。
- **图 3D 实际比较**：模拟 D(ω)（三种密度空心圆）对照 ω⁻² 虚线（纯视觉参考）、$D_a$ 水平线、$D_{RW}$ 上升线；D(ω) 在 ~30–40 THz（估读）跌向 $D_a$ 并穿越 $D_{RW}$。

### 1.4 色散分析（图 4；式 6–8）

- **操作**：$C_{L,T}(q,\omega)=\frac{q^2}{2\pi\omega^2 N}\int dt\langle j_{L,T}(q,t)\cdot j_{L,T}(-q,0)\rangle e^{i\omega t}$（式 6–8，纵/横投影），再对每个 q 拟合单阻尼谐振子模型（SI 图 S2 给拟合示例；公式疑为 $C(q,t)=C(q,0)e^{-t/2\tau}\cos\omega t$，SI 提取有损，未最终确认）得寿命 τ；平均自由程 λ 报于图 4C（λ 的构造公式材料中未给出——未知）。
- **输出**：清晰色散纵向至 ~30 THz、横向至 ~20 THz【原述，第 4 页】；**注意**：SI 图 S2 说明称“Clear dispersions are demonstrated up to ~30 THz in both longitudinal and transverse directions”（有损提取）——正文与 SI 对横向范围口径不一（~20 vs ~30 THz），引用需注明。
- **交叉频率**：正文【原述】“propagating to diffusive crossover frequencies for longitudinal and transverse excitations are in a similar range as the other physical models at ~30 and 35 THz, respectively”（第 4 页）。**核查发现**：图 4A/B 箭头估读 ω_L,c≈33、ω_T,c≈28 THz，图 4C 中 λ=a 交叉估读横向 ≈33–35、纵向 ≈36–38 THz（估读精度 ±2 THz），均显示纵向不低于横向，与正文“respectively”的归属（纵 30 / 横 35）相反——疑为正文数字次序颠倒或估读误差，属**原文内部不一致**；引用时只宜用区间 30–35 THz。
- 【原述】“the mean free paths vary by nearly four orders of magnitude from ~1 THz to the crossover frequencies, similar to spectral thermal diffusivity calculated by HNEMD as shown in Fig. 3D.”（第 4 页）。

### 1.5 合链

分母 = 300 K 量子修正总热导；分子 = ω_c（30–35 THz）以下传播振动的贡献；闭合依据 = 图 3C 累积在 ~30 THz 饱和 + 图 3D/图 4 把 ω_c 定在同一区间。“~100%”由此而来，是半定量闭合，不是直接测量的百分比。

## 2. 证据的共享输入与排除力

- 图 3B/3C/3D 全部由同一条 κ(ω) 派生（同轨迹、同势、同 QC 规则），互为**自洽性**校验而非独立证据；图 4 用不同观测量（速度流相关）并引入独立的 DHO 模型假设，独立性较强。模型二、三共享 Debye 声速平均值与数密度。
- **能排除**：ω_c 远低于 30 THz 的情形——若 ω_c 很低，ω_c 以上扩散振动应贡献可观热导，累积曲线不会在 ~30 THz 饱和（与图 3C 矛盾）。【推断】
- **不能排除**：20–40 THz 过渡带的判据模糊性（模型一自述 ball park；横向清晰色散范围正文/SI 口径不一）；$D(\omega)$ 定义中 κ 是否量子修正未明示；NEP 势的系统性偏差（论文以 DOS 对照 DFT、sp³ 对照实验缓解，图 1B/图 2，但未消除）。

## 3. 约束位置与遗漏后果（小结）

| 约束 | 所在环节 | 遗漏/误用改变的量 | 方向 |
| --- | --- | --- | --- |
| 经典 MD + 式 5 后验 QC | 频谱权重 | 总 κ 与累积曲线形状 | 方向确定：高估 30–40%（论文数值 + 因子 ≤1） |
| 判据用物理模型替代模态分类 | ω_c 估计 | ω_c 的不确定度直接传给“~100%” | 不定；SI 自述 ball park |
| $D_a$ 用平均 v_D≈14 km s⁻¹（实际 12.97–15.21） | 图 3D 水平线 | 交叉点位置 | 几何上可判方向（水平线上移→交点左移→ω_c 降低），幅度论文未给 |
| 有限盒长截断 ≲1 THz（估盒长 ~86 Å → 频率截断 ~1–2 THz，我的估算） | κ(ω) 低频端 | 低温外推时 Rayleigh/TLS 等机制缺失 | 300 K 影响小（κ(ω) 峰在 ~3 THz，估读）；低温重要 |
| NEP 势保真 | 全部频谱 | 系统性风险 | 不定 |

## 4. 适用边界与使用建议

- **可用**：作为“高密度（3.0–3.5 g cm⁻³）、高 sp³（58–90%）无定形碳在 300 K 的热导可由传播振动主导”的**机制性模拟证据与基准**；佐证“传播子主导 ↔ 高热导无定形固体”的跨材料图景（图 5，约 30 种无定形固体调查，第 5 页）。
- **不可用**：作为精确实验百分比；外推到低密度、含氢、薄膜几何或低温（<1 THz 截断 + QC 权重增大）需要各自重新验证；与文献最高实验值 ~37 W m⁻¹ K⁻¹ 存在差距，作者推测高值样品或为纳米晶（第 3 页）。
- **已完成的验证**（本次阅读内）：公式与原页核对、QC 降幅自验、盒长截断自洽估算、SI 判据 caveat 确认、图 3C 线型归属确认。**建议的进一步阅读**（未执行）：NEP 势原文（GPUMD，文献 64）核对势版本；Seyf & Henry（文献 51）模态分类法以了解本文未走路线的判别力；Agne et al.（文献 57）核对 $D_{RW}$ 推导前提；Treacy & Borisenko（文献 50）评估“纳米晶”假说。

## 5. 引用与定位速查

- ~100% 结论句：第 4 页 Discussion（亦见摘要、第 2 页末段）。
- HNEMD 式 1–4、QC 式 5：第 5 页 Methods“Thermal conductivity calculations”。
- 色散式 6–8：第 6 页 Methods“Dispersion analysis”。
- 图 3（A–D）及图注：第 3 页；图 4（A–C）及图注：第 4 页；图 5：第 5 页。
- 三模型与交叉频率：第 4 页 Discussion。SI 图 S1（幂律失效）、S2（DHO 拟合）、S3（温度依赖）、S4（线宽比）。
- 结构/势/模拟细节：第 2 页（sp³、DOS、Debye 速度）、第 5 页 Methods“Molecular dynamics simulations”。
