# 5.Syntax_Analysis_Bottom_Up 覆盖清单

源文件：`/Users/bytedance/mywork/final/com/5.Syntax_Analysis_Bottom_Up.pdf`

提取文件：
- `5.Syntax_Analysis_Bottom_Up_full.txt`
- `5.Syntax_Analysis_Bottom_Up_pages.json`

总页数：206 页。笔记按课件原顺序组织；重复出现的 Revisit 页面在正文中合并总结，但保留其新增或强调的知识点。

## p1-p3 标题与课程路线图

- Lecture 5：Syntax Analysis: Bottom-Up。
- 内容导图：Bottom-up parser、Shift-Reduce、Handle、Viable Prefix、Conflicts、LR(0)、SLR(1)、LR(1)、LALR(1)、Parser table。
- LR 系列关系：LR(0) 自动机提供状态与转移；SLR(1) 用 FOLLOW 限制规约；LR(1) 在 item 中加入 lookahead；LALR(1) 合并 LR(1) 同 core 状态。

## p4-p9 自底向上分析与移入-规约基础

- Bottom-up parsing：从输入串出发逐步规约为开始符号，是最右推导的逆过程，从叶到根构造语法树。
- 相对 Top-down 的特点：不需要左因子提取，可以处理左递归，但手写实现困难，通常依赖自动工具。
- Shift-reduce parser：栈保存文法符号，输入缓冲区保存剩余输入。
- 四类动作：Shift、Reduce、Accept、Error。
- 示例文法 `S -> aAcBe; A -> b | Ab; B -> d` 对 `abbcde` 的分析流程。
- 关键问题：何时移入/规约，以及规约时用哪条产生式。

## p10-p27 句柄、短语、直接短语与活前缀

- Right-sentential form：最右推导中出现的句型。
- Phrase：句型语法树中某个子树叶子构成的符号串。
- Simple phrase：只有父子两代的子树形成的短语。
- Handle：最左直接短语，是规约时应被替换的 RHS；一个右句型中只有一个句柄。
- 示例 `a*b+c`：短语、直接短语、句柄识别。
- 示例 `T + T*F + id`：逐步展示句柄如何被移入栈顶并规约。
- 句柄为什么总能在栈顶处理：没到栈顶就继续移入，到栈顶就立即规约。
- Viable prefix：不越过最右句柄右端的右句型前缀；LR 分析栈内容始终是活前缀。

## p28-p31 冲突与 Bottom-up 性质

- 二义文法 `E -> E*E | E+E | (E) | id` 对 `id*id+id` 产生不同分析。
- Shift-reduce conflict：既可移入也可规约。
- Reduce-reduce conflict：可用两条产生式规约。
- 冲突常来自二义文法，也可能来自不适合某类分析器的非二义文法。
- 解决方向：改写文法/分析器以编码优先级和结合性，或去除 dangling-else 等二义性。

## p32-p62 LR 分析器与 ACTION/GOTO 表

- Bottom-up parser 类型：simple precedence、operator precedence、recursive ascent、LR family 等。
- LR(k)：L 表示从左到右扫描，R 表示反向构造最右推导，k 表示向前看符号个数。
- LR 与 LL 对比：同为线性时间/空间、可自动生成；LR 更强，但冲突调试更复杂。
- LR parser 栈保存状态序列 `S0 S1 ... Sm`，每个文法符号关联一个状态。
- ACTION 表按状态和终结符索引，动作包括 shift、reduce、accept、error。
- GOTO 表按状态和非终结符索引，用于规约后压入新状态。
- 表驱动 LR 程序伪代码。
- 示例文法 `E -> E*B | E+B | B; B -> 0 | 1`，使用表分析 `1+1`。
- 构造解析表的类型概览：LR(0)、SLR(1)、LALR(1)、LR(1)、LR(k)。

## p63-p95 LR(0) item、CLOSURE/GOTO、DFA 与局限

- LR parser 通过状态追踪分析进度；状态由 item 集合表示。
- LR(0) item：在产生式 RHS 中加入点号，点号表示已经识别到的位置。
- 配置集：若 item 点后是非终结符，要把该非终结符的候选产生式也纳入当前状态。
- 增广文法：加入 `S' -> S`，用 `S' -> S .` 表示接受。
- CLOSURE(I)：对点后非终结符不断加入其点在最左的产生式。
- GOTO(I, X)：将 I 中点前移过 X 后再取闭包，形成 DFA 转移。
- Canonical LR(0) collection：所有可达 LR(0) item 集。
- 示例文法 `S' -> S; S -> BB; B -> aB | b` 的状态、DFA 和 LR(0) 表。
- LR(0) 表构造规则：点后终结符产生 shift；完成项产生 reduce；`S' -> S .` 产生 accept。
- LR(0) 冲突条件：同一状态存在完成项和移入项，或存在多个完成项。
- LR(0) 局限：没有 lookahead，完成项会无条件规约，容易冲突，尤其含 epsilon 产生式时。

## p96-p106 SLR(1)

- SLR(1) 使用同一套 LR(0) 配置集、表结构和运行算法。
- 只在下一输入符号属于被规约非终结符 FOLLOW 集时填入 reduce。
- 示例：`E -> T | E+T | V=E; T -> (E) | id | id[E]; V -> id`，用 `FOLLOW(T)` 与 `FOLLOW(V)` 区分 `id` 后的动作。
- SLR(1) 文法判定条件：
  - 移入项的终结符不能落入同状态完成项左部的 FOLLOW 集。
  - 多个完成项的 FOLLOW 集必须两两不交。
- SLR(1) 优势：相比 LR(0) 用一个 lookahead 大幅减少冲突，且状态数不变。
- SLR(1) 局限：FOLLOW 是全局集合，不能区分当前栈下方的具体上下文。
- 示例 `S -> L=R | R; L -> *R | id; R -> L` 中 `id=id` 的 SLR 冲突。

## p107-p122 LR(1)

- LR(1) 把必要的上下文加入状态：item 形如 `[A -> X1...Xi . Xi+1...Xj, a]`。
- lookahead 只对完成项的 reduce 起作用。
- reduce 精度递进：LR(0) 完成即规约；SLR(1) 看 FOLLOW；LR(1) 看 item 自带的精确 lookahead。
- LR(1) CLOSURE：对 `[A -> u . Bv, a]` 和 `B -> w`，加入 `[B -> . w, b]`，其中 `b in FIRST(va)`。
- LR(1) GOTO：点移过符号后传递 lookahead 并取闭包。
- 示例文法 `S -> XX; X -> aX | b` 的 LR(1) 项集和表。
- LR(1) 文法条件：无 shift-reduce 冲突，完成项 lookahead 两两不冲突。
- 每个 SLR(1) 文法都是 LR(1)，但 LR(1) 状态数通常更多。

## p123-p139 LALR(1)、LL vs LR 与层级

- LR(1) 状态数可能很大；LALR(1) 合并同 core 状态，折中 LR(1) 与 SLR(1)。
- Core：LR(1) item 去掉 lookahead 后的 LR(0) item。
- 示例：合并 `I3/I6`、`I4/I7`、`I8/I9` 得到更少状态。
- 合并效果：
  - 可能引入 reduce-reduce conflict。
  - 不会新引入 shift-reduce conflict。
  - 错误检测可能延迟。
- LALR 表构造：可先构造 LR(1) 再合并，也可构造时即时合并。
- 文法与状态层级：能力 `LR(1) > LALR(1) > SLR(1) > LR(0)`；状态数 `LR(1) > LALR(1)=SLR(1)=LR(0)`。
- LL 与 LR 对比：LL 在看到 RHS 前缀时就要猜产生式；LR 等完整 RHS 入栈后再规约，因而可处理更多文法。

## p140-p189 Syntax Analysis Revisit

- 复习语法分析作为编译第二阶段：输入 token 序列，输出 parse tree 或 AST。
- 文法四元组 `G=(VT,VN,S,delta)`，终结符、非终结符、开始符号、产生式。
- 正则表达能力不足以描述嵌套结构，需要 CFG。
- 推导、规约、句型、句子、语言、分析树、二义性。
- 乔姆斯基文法体系：0 型、1 型、2 型、3 型。
- Parse Tree vs AST：AST 去除不影响语义的推导细节。
- Top-down 复习：RDP、回溯、左递归消除、左因子、FIRST、FOLLOW、LL(1) 表和非递归算法。
- Bottom-up 复习：Shift-reduce、Phrase/Handle、Viable Prefix、LR(k)、ACTION/GOTO、LR(0)、SLR(1)、LR(1)、LALR(1)。

## p190-p206 Exercise 2

- 正则语言与有限集：有限语言可用正则表达式；`{x^n y z^n | n>0}` 不是正则语言。
- DFA 是否能识别 epsilon：可以，当开始状态为接受状态。
- Thompson 构造 `(a|b)*` 的状态数：8。
- 无二义文法中同一句子的最左/最右推导分析树一致。
- LL(1) 文法判定条件与 LL(1) 表行列含义。
- 活前缀题：`S => aBb => aaAb`，句柄 `aA`，活前缀为 `a, aa, aaA`。
- 短语/直接短语/句柄题：`a*b+c`。
- LL(1) 表题：`S -> A; A -> epsilon | bbA`。
- LR(1) DFA/表题：`S -> A; A -> A+A | B++; B -> y`。
- 该文法存在 `r2/s4` 冲突，不是 LR(1)；可通过改写文法或定义解析策略解决。
- 对 `y++` 的 LR 分析流程，最终 accept，说明 `y++` 是该文法句子。
