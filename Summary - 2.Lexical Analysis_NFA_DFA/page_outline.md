# 课件分段大纲：2.Lexical Analysis_NFA_DFA（共 80 页）

主线：From Specification to Implementation —— RE(规范) → NFA → DFA → 最小化DFA → 表驱动实现(实现)。
本讲覆盖蓝图的"右半部分"（实现线），第1讲已讲左半部分（RE 规范）。

## 分段（segmentation map，覆盖全部 80 页）

- **A 导论与路线图** p1–2：标题页；From Spec to Impl 全景图（NFA/DFA/Table-Driven/Minimizing/Token Partition）。
- **B 有穷自动机基础** p3–13：
  - p3–4 为何需要 FA：RE只是规范，需识别器；FA=实现；automaton/FA定义。
  - p5 转换图（Transition Diagram）：节点=状态、边=转移、start、双圈=接受态。
  - p6–7 FA 即语言识别程序；L(FA)≡L(RE)；接受/拒绝；例子"任意个1后跟一个0"。
  - p8 DFA vs NFA 概念定义（确定/非确定、ε-move、单路径/多路径）。
  - p9 FA 五元组 (Σ,S,n,F,δ)。
  - p10–11 NFA/DFA 对比：(a|b)*abb，输入aabb的成功/失败序列。
  - p12–13 转换表（Transition Table）：优缺点、O(|S|·|Σ|)空间；本讲四步流程总览。
- **C Thompson 算法 RE→NFA** p14–22：
  - p14 原子 RE 的 NFA（ε、单字符 a）。
  - p15 归纳规则：R=A|B、R=AB、R=A*。
  - p16–17 例子：(a|b)*abb 分步构造。
  - p18–22 Revisit（规范→实现的两张回顾图 + 文字小结：复合RE、消歧、FA类型、Thompson）。
- **D NFA→DFA 子集构造** p23–31：
  - p22–23 NFA≡DFA 等价定理；DFA更费内存但更快。
  - p24 子集构造思想：DFA每个状态=NFA状态集合。
  - p25–26 两个要解决的问题（消ε、消多转移）；ε-closure 定义；move(T,a)、Iₐ=ε-closure(move(I,a))记号。
  - p27–31 完整例子：从start求ε-closure，建T0..T3转移表，标记接受态，画DFA。
- **E DFA 最小化（分割法）** p32–40：
  - p33 最小DFA唯一性；等价状态两条件。
  - p34 分割算法三步。
  - p35 简单例子。
  - p36–39 复杂例子 {S,A,B,C,D,E,F} 逐步分割，画最小DFA。
  - p40 判断DFA是否最小的练习。
- **F 复杂度** p41–42：空间 O(2^N)（子集数 2^N−1）；DFA执行 O(|X|)，NFA执行 O(|X|·N²)。
- **G 表驱动实现 / Lex** p43–62：
  - p50 Lex 流程 RE→NFA→DFA→Table；以空间换速度。
  - p51–54 Lex 生成器原理；多模式合并NFA（a、abb、a*b+ 三模式 + 起始态0 + ε）；模拟run、备份找最长接受态。
  - p55 最长匹配（maximal/longest match）；同长则先列优先。
  - p56 关键字匹配两种方法（嵌RE vs 关键字表），通常方法2更优。
  - p57–62 Lex DFA 例子、二义性问题、是否最小。
- **H 正则语言的极限 + 展望 + 小结** p63–73(对应文件p63–68)：
  - p63–65 L={aⁿbaⁿ}/{aⁿbⁿ} 非正则；FA无记忆不能计数；括号/嵌套结构非RL；需更强形式 → CFG。
  - p66–67 总结两张图（转换流程 + 完整规范到实现）。
  - p68 龙书阅读建议。
- **I 练习** p69–80：判断NFA/DFA及RE(0*1+2*)；NFA可被DFA模拟(always)；补集；Thompson构造(a|b)*abb(a|b)*；从RE到最小FA完整流程 b*(a|ab)*。

## 公式/概念密集区
- ε-closure、move、子集构造（D）
- 等价状态判据、分割法（E）
- 复杂度公式（F）
- 最长匹配/消歧规则（G）
- 正则语言极限（H）

## 需要的图（用 TikZ 画）
1. From Spec to Impl 全景流水线（贯穿全讲）
2. 转换图基本元素（start态、接受态双圈）
3. Thompson 三条归纳规则（A|B、AB、A*）的 NFA 拼接
4. 子集构造例子的 NFA + 结果 DFA
5. 最小化前后 DFA 对比
6. NFA vs DFA 执行对比示意
