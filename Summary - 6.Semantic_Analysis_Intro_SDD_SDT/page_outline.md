# 6.Semantic_Analysis_Intro_SDD_SDT 覆盖清单

源文件：`/Users/bytedance/mywork/final/com/6.Semantic_Analysis_Intro_SDD_SDT.pdf`

提取文件：
- `6.Semantic_Analysis_Intro_SDD_SDT_full.txt`
- `6.Semantic_Analysis_Intro_SDD_SDT_pages.json`

总页数：129 页。笔记按课件原顺序组织；重复出现的 Revisit/Summary 页面在正文中合并总结，但保留其强调的知识点。

## p1-p4 标题、编译阶段和 Annotated AST

- Lecture 6：Semantic Analysis: Intro & SDD & SDT。
- 语义分析位于前端最后阶段，输入为 syntax tree，输出仍可作为后续中间代码生成的输入。
- 抽象语法树 AST 可进一步带类型、符号等标注，形成 Annotated/Decorated AST。

## p5-p8 为什么需要语义分析与实现方式

- 标识符需要上下文才能确定含义，类比 “He ate it”。
- 语义分析负责 def-use check、type check、声明先于使用、表达式类型一致等。
- CFG 只能描述语法形状，不能处理使用定义绑定等上下文约束。
- 两类实现思路：
  - Attribute grammars：一遍编译，解析过程中做语义动作。
  - AST walk：先构建语法树，再遍历检查语义规则。

## p9-p17 语法制导翻译、属性、SDD 与 SDT

- Syntax Directed Translation：由 CFG 语法结构驱动语义分析和翻译。
- 属性：附着在文法符号上的语义信息，格式 `X.a`，可表示值、类型、地址、AST 指针、代码片段等。
- SDD：CFG + attributes + semantic rules，是 CFG 的推广，语义规则不规定执行位置。
- SDT：CFG 中嵌入 semantic actions，动作位置决定执行时机。
- SDD 更像高层规则说明；SDT 是可执行的翻译方案。

## p18-p28 SDD 属性类型与基本概念

- SDD 有两类属性：Synthesized attribute 和 Inherited attribute。
- 综合属性：由节点自身和子节点属性计算，信息向上传递。
- 继承属性：由父节点、自身或兄弟节点属性计算，信息可向下或横向传递。
- 终结符可以有综合属性，通常来自词法分析；终结符没有继承属性。
- 副作用：代码生成、打印、修改符号表等非纯属性计算行为。
- Attribute grammar：无副作用的 SDD。
- Annotated parse tree：每个节点标注属性值的分析树。

## p29-p33 依赖图与属性值求值顺序

- 依赖关系：计算某属性前必须先计算它依赖的属性。
- Dependency graph：对某棵分析树中所有属性实例建图，边表示依赖。
- 属性计算顺序必须是依赖图的拓扑序。
- 若依赖图有环，则没有拓扑序，该 SDD 在这棵分析树上无法求值。
- SDD 中同时有综合属性和继承属性时，不保证总存在合法求值顺序。

## p34-p37 S-Attributed 与 L-Attributed Definitions

- S-SDD：所有属性都是综合属性，可按任意自底向上顺序求值，可与 LR/Bottom-up parsing 一起实现。
- L-SDD：允许受限制的继承属性，RHS 中依赖只能从左到右；可与 LL/Top-down parsing 结合，也可通过改写用于 LR。
- L-SDD 中 `Xi.inh` 只能依赖 `A.inh`、左侧符号属性以及 `Xi` 自身无环属性。
- 示例 `A -> BC` 中 `B.i = f(C.c,A.s)` 不是 L-SDD，因为依赖了右兄弟/左部综合属性。

## p38-p47 S-SDD 到 SDT 及 LR 实现

- SDT 可通过 parse tree/AST 遍历实现，也可在 parsing 过程中实现。
- 任意无环 SDD/SDT 可通过树遍历实现；解析过程中实现只适合特定子类。
- S-SDD 转 SDT：把动作放到产生式末尾，得到 postfix SDT。
- 若底层文法 LR 可分析，则 postfix SDT 可在 LR 规约时执行。
- LR 栈扩展：状态、文法符号、属性一起存；规约时根据栈位置计算左部属性。
- 示例：表达式 `3*5+4` 的属性计算和栈操作。

## p48-p60 L-SDD 到 SDT、消除左递归与属性传递

- L-SDD 转 SDT：
  - 计算某非终结符继承属性的动作放在它出现之前。
  - 计算左部综合属性的动作放在产生式末尾。
- 对 top-down 实现，需要先消除左递归。
- 示例：把 `E -> E + T | E - T | T` 改为 `E -> T R`，用 `R.i` 传递当前累计值，用 `R.s` 返回最终结果。
- 输入 `9 - 5 + 2` 最终得到 `E.val = 6`。
- 一般规则：左递归的累计计算可通过新非终结符 `R` 的继承属性和综合属性转移。

## p61-p73 L-SDD 在 RDP、LL 和 LR 中的实现

- 递归下降实现：继承属性作为函数参数传入，综合属性作为返回值返回；函数体中用局部变量和语义动作。
- 非递归 LL 实现：扩展分析栈，加入 action-record 和 synthesize-record；继承属性放在符号记录中，综合属性放在单独综合记录中。
- LL 表驱动分析时，展开左部可能丢失其记录，因此必须把后续动作需要的属性提前复制到动作记录。
- LR 实现 L-SDD 的问题：继承属性已在栈中，但位置可能不固定。
- Marker 非终结符：用 `M -> epsilon` 替换嵌入动作，作为占位并把动作转成可在规约时执行的 postfix 形式。
- 示例：`T -> F {T'.inh=F.val} T'` 改为 `T -> F M T'`，`M -> epsilon` 保存并传递 `F.val`。

## p74-p103 语义分析应用：绑定、作用域、符号表和类型检查

- Binding：把标识符使用与其定义匹配，是代码生成前的关键步骤。
- Scope：某个定义可绑定使用点的程序区域。
- Static scoping：由程序文本位置决定，也称 lexical scoping；绑定到最近的外层定义。
- Dynamic scoping：由运行时调用/执行路径决定；绑定到当前执行中最近定义。
- 符号表：记录标识符定义及属性，随作用域进入/退出更新。
- 符号表操作：`enter_scope`、`exit_scope`、`find_symbol`、`add_symbol`、`check_symbol`。
- 数据结构：数组、链表、二叉树、哈希表；哈希表常用，平均 O(1)，冲突用链式解决。
- 多作用域处理：每个作用域一个符号表，活动作用域用栈管理，查找从栈顶向外层搜索。
- 符号表条目：name、kind、attributes；变量、函数、结构体、类的属性不同。
- 类型信息用于语义检查、代码生成和优化。
- Type：值集合及其操作集合；Type checking：验证操作和操作数类型一致。
- 静态类型检查在编译时进行；动态类型检查在运行时通过 type tag 检查。
- Static typing 与 dynamic typing 是语言类型系统特征；static/dynamic type checking 是执行检查的方法。

## p104-p129 Exercise

- 复习第 4/5 讲练习：无二义文法最左/最右推导、LL(1) 判断、LL(1) 表大小、活前缀、短语/直接短语/句柄、LL(1) 表、LR(1) DFA/表、`y++` 分析流程。
- 新增 LR/SLR 练习：`S -> Sb | bAa; A -> aSc | aSb | a`，判断 LR(0)、LR(1)，构造 SLR(1) 表。
- 判断题：
  - L-属性定义不是所有属性都是继承属性。
  - RHS 中间有语义动作并不意味着只能用递归下降；LR 可通过 marker 等方式实现。
- SDD 输出题：`S -> (L) | a; L -> L,S | S`，输入 `(a,(a))` 输出 `2`。
- S/L 属性判断题：对 `A -> B C D` 的属性规则判断是否满足 S-SDD/L-SDD。
- 非标准二进制数值系统：用 `val` 和 `tmp` 两个属性计算交替符号权值。
