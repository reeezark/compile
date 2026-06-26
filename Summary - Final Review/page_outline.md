## 0.Introduction.pdf (34 pages)
p1: 计算机学院 | 中山大学 | Introduction to
p2: • 年级： | u 大三年级学生、第二学期 | • 先修课程：
p3: • 教育经历： | u 2013.10 - 2018.08，硕&博，约克大学 | u 2008.09 – 2012.07，本科，西安工业大学
p4: The Instructor[关于教师] | 研究方向及成果 | 1 智能安全攸关工业软件：自动驾驶/无人机/工业机器人/手术机器人系统、实时操作系统
p5: • 常年招收硕/博士研究生（推荐大三暑假进组），也欢迎感兴趣的本科生加入 | u 研究招收方向：操作系统、CPU+GPU/NPU异构系统设计优化，无人车/无人机/机器人系统设 | 计优化、端到端时延分析技术、安全攸关编程语言/模型设计等
p6: Teaching Assistants[助教] | 26级硕士研究生 | 苟睿哲
p7: • 任课教师 | u 计算机学院，人工智能与机器人研究所，D104C | • 课程主页：
p8: • 主要教材： | u 《Compilers: Principles, Techniques, and Tools》, 第二版 | u 课程将覆盖章节1-6与附件A
p9: • 理论课 | u 排课： | p 周一：第 1-9 周
p10: Schedule[进度安排] | 周次 课程内容 周次 课程内容 | 第1周 (3.2 & 3.4) 周一：课程介绍、周三：词法分析 第10周 (5.6) 周三：中间代码
p11: • 学分与学时： | u 理论课：3学分、54学时 | u 实验课：1学分、36学时
p12: What is a Compilation[什么是编译] | • 问题：大家写程序都用过什么语言？ | u 高级语言C、C++、Java、Python、Ruby等等
p13: What is a Compilation[什么是编译] | • 不同编程语言有不同的翻译方式 | u 编译：通常针对较为“底层”的语言
p14: l 编译：翻译成机器语言后方能运行 | u 目标程序独立于源程序（修改→再编译→运行） | u 分析程序上下文，易于整体性优化
p15: l 即时编译 (Just-In-Time Compiler)： 运行时执行程序编译操作 | u 弥补解释执行的不足 | p 把翻译过的机器代码保存起来，以备下次使用
p16: #include <stdio.h> | int main( ) | printf(“Hello World!\n”);
p17: Compilation for C (Cont.) | • Preprocessing：源代码 (c code) → 展开后的代码 (c code) | • Compiling：展开后的代码 (c code) → 汇编代码 (assembly)
p18: Why Compiler [为什么学编译原理] | • 为了更好的编程？ | u 有助于产出高质量代码
p19: Overview of Compiler [编译结构总览] | Lexical Analyzer | Syntax Analyzer
p20: • 前端 (for Analysis)：对源程序，识别语法结构 | 信息，理解语义信息，反馈出错信息 | u 词法分析（Lexical Analysis）
p21: • 扫描源程序字符流，识别并分解出有词法意义的 | 单词或符号（token） | u 输入：源程序；输出：token序列
p22: Lexical Analysis[词法分析] | Language | Specification
p23: l 解析源程序对应的token序列，生成语法分 | 析结构（syntax tree, 语法分析树） | u 输入：单词流；输出：语法树
p24: Syntax Analysis[语法分析] | define | Chomsky’s Grammar Hierarchy
p25: Syntax Analysis[语法分析] | type 1 type 2 | Top-down parser
p26: • 基于语法结果进一步分析语义 | u 输入：语法树；输出：语法树+符号表 | u 收集标识符的属性信息（type, scope等）
p27: Semantic Analysis[语义分析] | Definitions (SDD) | attributes
p28: l 初步翻译，生成等价于源程序的中间表示（IR）： | u 输入：语法树；输出：IR | u 建立源和目标语言的桥梁，易于翻译过程的实现，利
p29: Intermediate Code[中间代码生成] | BackPatching | Intermediate Code
p30: l 加工变换中间代码使其更好（代码更短、性能更 | 高、内存使用更少） | u 输入：IR；输出：(优化的）IR
p31: Code Optimization[代码优化] | Layout-related | Transformations
p32: l 为特定机器产生目标代码（e.g., 汇编） | u 输入：(优化的) IR；输出：目标代码 | u 寄存器分配：放置频繁访问数据
p33: Target Code[目标代码生成] | Code | Generation
p34: Introduction | Enjoy the Journey!

## 1.Lexical Analysis_Intro_RE.pdf (43 pages)
p1: 编译原理 | Complier Principles | Lecture1
p2: The Starting Point | Lexical Analyzer | Syntax Analyzer
p3: The Starting Point | (keyword, while) | (id, y)
p4: • Lexical Analysis is the process of identifying the substrings (called | lexeme[词素]) and generating tokens[词] by identifying token class. | • Task: Reading the source program as a string of characters and diving
p5: • Example | What is Lexical Analysis[词法分析]? | w h i l e ( i < z ) \ n \ t i + + ;
p6: Lexical Analysis[词法分析] | Language | Specification
p7: Content | From Specification to Implementation | Language
p8: • Token[词法单元/词]: a “word” in language (smallest unit with meaning) | ◆ A token is a pair consisting of a token name and an optional attribute value. | ◆ A token is a tuple (class, lexeme)
p9: ⚫ Numbers: a non-empty string of consecutive digits | ⚫ Keyword: a fixed set of reserved words (“for”, “if”, “else”, …) | ⚫ Whitespace: a non-empty sequence of blanks, tabs, newlines
p10: • Which of the following names are NOT accepted by Java? | • In terms of JAVAcoding convention, which of the above is | GOOD coding practice?
p11: • Lexical analysis is also called Tokenization(or Scanner)[词法分析也称 | 为扫描器] | ◆ Partition input string into a sequence of tokens.
p12: • Define a finite set of token classes [定义词法单元的类别] | ◆Describe all items of interest | ◆keyword, identifier, whitespace…
p13: • An implementation must do two things | ◆Recognize the token class that the substring belongs to[识别分类] | ◆Return the value or lexeme.
p14: • C++: Nested template declarations | vector<vector<int>> myVector | • Ambiguity
p15: • “look ahead” may be required to resolve ambiguity[消除歧义] | ◆Extracting some tokens requires looking at the larger context or structure | ◆Structure emerges only at the parsing stage with the parse tree
p16: • Identifying token class: which set of strings belong to which | token class? | ◆ Question: How to describe string patterns? [模式]
p17: • Alphabet ∑[字母表]: A finite set of symbols. | ◆ Symbol: letter, digit, punctuation, … | ◆ Example: {0, 1}, {a, b, c}, ASCII, …
p18: • Examples: | ◆ Alphabet Σ = (set of) English characters |  Language L = (set of) English sentences
p19: • Union[并]: similar operation on sets, i.e., 𝐴 ∪ 𝐵, denoted as A | B | • Concatenation[连接]: all strings formed by taking a string from the | first language and a string from the second language in all
p20: • Language: L = {a, b}, D = {0, 1} | • L∪D = {a, b} ∪ {0, 1} = {a, b, 0, 1} | • LD = {a, b}{0, 1} = {a0, b0, a1, b1}
p21: • L = {A, B, …, Z, a, b, …, z}, D = {0, 1, …, 9} | ◆ L and D are languages whose strings happen to be of length one | ◆ Some other languages that can be constructed from L and D are:
p22: • Regular expressions [正则表达式] are to describe all languages that can be | built from the operators applied to the symbols of some alphabet. | • Regular Expression is a simple notation
p23: • The regular expressions are built recursively out of smaller regular | expressions. | • Each regular expression r denotes a language L(r)
p24: Build Regular Expressions[构建正则表达式] | • Compound Regular Expressions[复合正则表达式] | ◆ Large REs built from smaller ones
p25: • Regular expression operator precedence is | (A) | A B
p26: • One or more instances: 𝐴+ ≡ 𝐴𝐴∗ | • Zero or one instance: 𝐴? ≡ 𝐴 | 𝜀 | • Characters: [𝑎1𝑎2 … 𝑎𝑛] ≡ 𝑎1 | 𝑎2 |…| 𝑎𝑛
p27: ⚫ Excluded range: complement[补集] of [a-z] ≡ [^a-z] | ⚫ Symbol ^ is also used to match the left end of a line. Symbol $ matches the | right end of a line.
p28: Revisit | From Specification to Implementation | Language
p29: ⚫ What is lexical analysis? | ⚫ Scan the substrings and generate tokens that match the language pattern | ⚫ Token: the smallest unit in language -- (class, lexeme)
p30: ⚫ How to build machine processable languages? | ⚫ Follow certain pattern | ⚫ Regular Expression is a good way to describe computer languages
p31: RE Examples | Regular Expression Explanation | a* 0 or more a’s (ε, a, aa, aaa, aaaa, …)
p32: • (a|b)* = ? | (L(a|b))* = (L(a) ∪ L(b))* = ({a} ∪ {b})* = {a, b}* | = {a, b} 0 ∪ {a, b} 1 ∪ {a, b} 2 ∪ …
p33: • Typical regular expression for tokens, let | ◆ RE: letter = [A-Za-z] | ◆ RE: digit = [0-9]
p34: REs in Programming Language | Symbol Meaning | \d Any decimal digit, i.e. [0-9]
p35: • S0: write a regex for the lexemes of each token class | ◆ Numbers = digit+ | ◆ Keywords = ‘if’ | ‘else’ | …
p36: • Some strings can be matched by different regular expressions | • Language definition must give disambiguating rules | ◆ When a string can be either an identifier or a keyword, keyword
p37: • Concepts | • Token & Lexeme | • Alphabet & String & Language
p38: Summary | Language | Specification
p39: • lexical analysis of “if i == 0”? Write the token sequence. | • <keyword, ‘if’>, <id, ‘i’ >, <op, ‘==’>, <num, ‘0’> | • Usage of RE and FA in lexical analysis?
p40: Que. Which of the following are Lexemes? | a. Identifiers | b. Constants
p41: Que. Regular expression a|b denotes the set | a. {a} | b. {ε, a, b}
p42: • Write regular definitions for the following languages | 1. All strings of a's and b's which contains the substring aba | (a|b)*aba(a|b)*
p43: • Dragon Book | ◆ Comprehensive Reading: |  Section 1.1, 1.2, 1.6

## 2.Lexical Analysis_NFA_DFA.pdf (80 pages)
p1: 编译原理 | Complier Principles | Lecture2
p2: Content | NFA DFA Table-Driven | Implementation
p3: • REs is only a language specification[只是定义了语言] | ◆ to construct a token recognizer for languages given by regular expressions | • How do we go from specification to implementation?
p4: • Regular Expression = specification[正则表达是定义] | • Finite Automata = implementation[自动机是实现] | • Automaton (pl. automata): a machine or program
p5: • Node[节点]: state | ◆ Each state represents a condition that may occur in the process | ◆ Initial state (Start): only one, circle marked with ‘start’
p6: • An FA is a program for classifying strings (return: accept, reject) | ◆ In other words, a program for recognizing a language | ◆ For a given string ‘x’, if there is a transition sequence for ‘x’ to move from
p7: • Are the following strings acceptable? | ◆ 0 √ | ◆ 1 ×
p8: • Deterministic Finite Automata (DFA): the machine can exist in only | one state at any given time[确定的有限状态机] | ◆ One transition per input per state
p9: • 5 components ( ∑, S, n, F, δ ) | ◆ An input alphabet Σ | ◆ A set of states S
p10: • NFA: There are many possible moves: to accept a string, we only | need one sequence of moves that lead to a final state | − Input string: aabb
p11: • DFA: There is only one possible sequence of moves, either lead to | a final state and accept or the input string is rejected | − Input string: aabb
p12: • FA can also be represented using transition table | • Advantage | ◆ We can easily find the transitions on a given state and input.
p13: Content | Regular | Expression NFA Lexical
p14: Basic: processing atomic REs | • NFA for  | • NFA for single character a
p15: Inductive: processing compound Res | R=A|B | R=AB
p16: • Convert “(a|b)*abb” to NFA | (a|b) | (a|b)*
p17: • Convert “(a|b)*abb” to NFA | (a|b)*abb | a b b
p18: Revisit | From Specification to Implementation | Language
p19: Revisit | Regular | Expression NFA DFA Lexical
p20: ⚫ Specification: Regular Expression | ⚫ Compound Regular Expression | ⚫ E.g., (ab)*, (a|b)*, (a*b*)*
p21: Content | Regular | Expression NFA DFA Lexical
p22: • NFA and DFA are equivalent | From NFA to DFA | To show this we must prove every DFA can be converted into an
p23: • Theorem: L(NFA) ≡ L(DFA) | ◆ Both recognize regular languages L(RE) | ◆ 对于每个NFA M存在一个DFA M'，使得 L(M)=L(M’)
p24: • Recall DFA | ◆ Every state must have exactly one transition defined for every letter | ◆ ε-moves are not allowed
p25: • Two problem need to solve | ◆ Eliminate ε-transition | ◆ Eliminate multiple transitions from a state on a single character
p26: Notion in the algorithm | • ε-closure(s) | The set of all states reachable by a series of
p27: • Step1: Start by constructing ε-closure of the start state | ◆ 𝐼 = ε-closure(state 0) = {0, 1, 3} | ◆ {0, 1, 3} is a new state for DFA, marked T0
p28: • Step1: Start by constructing ε-closure of the start state | ◆ 𝐼 = ε-closure(state 0) = {0, 1, 3} | • Step2: Keep getting ε-closure(move(𝐼, x)) for each character x in Σ
p29: • Step1: Start by constructing ε-closure of the start state | ◆ 𝐼 = ε-closure(state 0) = {0, 1, 3} | • Step2: Keep getting ε-closure(move(𝐼, x)) for each character x in Σ
p30: • Step1: Start by constructing ε-closure of the start state | ◆ 𝐼 = ε-closure(state 0) = {0, 1, 3} | • Step2: Keep getting ε-closure(move(𝐼, x)) for each character x in Σ
p31: • Construct DFA | Example Cont. | 𝐼 𝑰𝒂 𝑰𝒃 Accept
p32: Content | Regular | Expression NFA DFA Lexical
p33: • Theory: Given any DFA, there is an equivalent DFA containing a minimum | number of states, and this minimum-state DFA is unique | • Equivalent States
p34: • The algorithm | Partitioning the states of a DFA into groups of states that cannot be | distinguished (i.e., equivalent)
p35: • Step 1：Divide the states into two sets | Initial sets: {non-accepting states}, {accepting states} | Initial: {A} , {BC, AC}
p36: ① Initial | {S, A, B} and {C, D, E, F}, {non-accepting states} and {accepting states} | ② Consider all states in each subset, check the transitions for each x∈Σ
p37: ① Initial | {S, A, B} and {C, D, E, F} | ② Consider all states in each subset, check the transitions for all x∈Σ
p38: ① Initial | {S, A, B} and {C, D, E, F} | ② Consider all states in each subset, check the transitions for all x∈Σ
p39: ③ Finally, get the subsets and draw min DFA | {C, D, E, F}, {S}, {A}, {B} | {C, D, E, F} is denoted as {C}
p40: • Is the DFA minimal? | start | a a
p41: • NFA may be in many states at any time | • How many different possible states in DFA? | ◆ If there are N states in NFA, the DFA must be in some subset of those N
p42: • DFA execution | ◆ Requires O(|X|) steps, where |X| is the input length | ◆ Each step takes constant time
p43: Revisit | Regular | Expression NFA DFA Lexical
p44: Basic: processing atomic REs | • NFA for  | • NFA for single character a
p45: Inductive: processing compound Res | R=A|B | R=AB
p46: Notion in the algorithm | • ε-closure(s) | The set of all states reachable by a series of
p47: • Step1: Start by constructing ε-closure of the start state | ◆ 𝐼 = ε-closure(state 0) = {0, 1, 3} | • Step2: Keep getting ε-closure(move(𝐼, x)) for each character x in Σ
p48: • Step 1：Divide the states into two sets | Initial sets: {non-accepting states}, {accepting states} | Initial: {A} , {BC, AC}
p49: Content | Regular | Expression NFA DFA Table-Driven
p50: • Lex[词法分析器]: RE → NFA → DFA → Table | ◆ Converts regular expressions to NFA | ◆ Converts NFA to DFA
p51: • A Lex program is turned into a transition table and actions, which are used by a | FA simulator | • Automaton need to recognize lexemes matching any of the patterns in a program
p52: • Three patterns, three NFAs | • Combine three NFAs into a single NFA | Add start state 0 and ε-transitions
p53: • Input: aaba | ◆ ε-closure(0) = {0, 1, 3, 7} | ◆ Empty states after reading the fourth input symbol
p54: • DFA’s for lexical analyzer | • Input: abba | ◆ Sequence of states entered: 0137 → 247 → 58 → 68
p55: • In general, find the longest match possible | ◆ We have seen examples | ◆ One more example: input string aabbb …
p56: • Example: to recognize the following tokens | ◆ Identifiers: letter( letter | digit )* | ◆ Keywords: if, then, else
p57: • Three patterns, three NFAs | • Combine three NFAs into a single NFA | Add start state 0 and ε-transitions
p58: • Input: abbb | ◆ ε-closure(0) = {0, 1, 3, 7} | ◆ Select aab as the lexeme, execute {action3}
p59: • The accepting states are labeled by the pattern that is identified | by that state. | ◆ {6,8} can accept abb and a*b+.
p60: • Question | ◆Is this DFA minimal? | ◆are 8, 68, 58 really equivalent?
p61: • Depends on the language and the implementation approach | ◆if abb is a keyword |  Approach 1: identify abb explicitly by FA with precedence.
p62: • Depends on the language and the implementation approach | ◆if abb is a keyword |  Approach 1: identify abb explicitly by FA
p63: • For ∑={a, b} | • The set of strings S over this alphabet consisting of a single b | surrounded by the same number of a.
p64: • L = {𝑎𝑛𝑏a𝑛| n ≥ 0} is not a Regular Language | ◆ FA does not have any memory (FA cannot count) |  The above L requires to keep count of a’s before seeing b’s
p65: • Regular languages are expressive enough for tokens | ◆ Can express identifiers, strings, comments, etc. | • However, it is the weakest (least expressive) language
p66: Summary | Regular | expressions NFA DFA Table-driven
p67: Summary | Language | Specification
p68: • Dragon Book | ◆Comprehensive Reading: |  Section Section 3.6–3.7, 3.9.6 for finite automata
p69: • The graph describes NFA or DFA? Why? | NFA. | A: ε-transition,
p70: Que. The behavior of a NFA can be simulated by a DFA | a. always | b. sometime
p71: Que. What is the complement[补集] of the language accepted by the NFA | shown below? Assume ∑ = {a} and ε is the empty string | a. 
p72: • Convert (a|b)*abb(a|b)* into NFA | • Thompson construction: RE→NFA | (a|b)→(a|b)*
p73: • Convert (a|b)*abb(a|b)* into NFA | • Thompson construction: RE→NFA | (a|b)→(a|b)*
p74: • Convert (a|b)*abb(a|b)* into NFA | • Thompson construction: RE→NFA | (a|b)→(a|b)*
p75: • Construct a DFA for a minion language with ∑ = {𝑎, 𝑏} that does | not contain “abb”: | 1. Build the regular expression for the minion’s language
p76: • Convert b*(a | ab)* into NFA | b  | a b
p77: • Convert the NFA into DFA by subset construction | 6 7 | a b
p78: I 𝑰𝒂 𝑰𝒃 Accept | {0,1,3,4,5,6,8,13} 0 {7,9,12,13,5,6,8,10} 1 {2,1,3,4,5,6,8,13} 2 Yes | {5,6,7,8,9,10,12,13} 1 {5,6,7,8,9,10,12,13} 1 {11,12,13,5,6,8} 3 Yes
p79: • Draw DFA according to the transition table | I 𝑰𝒂 𝑰𝒃 | {0,1,3,4,5,6,8,13} 0 {7,9,12,13,5,6,8,10} 1 {2,1,3,4,5,6,8,13} 2
p80: • Minimization DFA | • Initial: {0,1,2,3} | {3} have no ‘b’ transition，split

## 3.Syntax Analysis_Intro_Parser_CFG.pdf (55 pages)
p1: 编译原理 | Complier Principles | Lecture 3
p2: Revisit | Regular | expressions NFA DFA Table-driven
p3: • L = {𝑎𝑛𝑏a𝑛| n ≥ 0} is not a Regular Language | ◆ FA does not have any memory (FA cannot count) |  The above L requires to keep count of a’s before seeing b’s
p4: • Regular languages are expressive enough for tokens | ◆ Can express identifiers, strings, comments, etc. | • However, it is the weakest (least expressive) language
p5: Revisit | Language | Specification
p6: Compilation Phases[编译阶段] | Lexical Analyzer | Syntax Analyzer
p7: Compilation Phases[编译阶段] | (keyword, while) | (id, y)
p8: Mind Map[思维导图] | definition | Grammars
p9: Syntax Analysis [语法分析] | • Second phase of compilation, also called parser. | • The parser obtains a string of tokens[词法单元组成的串] from the
p10: Syntax Analysis [语法分析] | • The parser will construct a parse tree [语法分析树] and passes it to | the rest of the compiler for further processing.
p11: Parsing Example[语法分析举例] | • Example1: Input: if (x == y) stmt1 else stmt2 [源程序输入] | ◆ Parser input (Lexical output) [语法分析输入]
p12: How to Specify Syntax? [如何定义语法] | • Natural Language[自然语言]: The language spoken by human | beings and different countries have different languages.
p13: How to Specify Syntax? [如何定义语法] | • A formal language can define itself in many ways:(1) Regular | Expression; (2) some Automata(FA); (3) Grammars. [文法]
p14: Grammar[文法] | Formal definition [形式化定义] : 4 components[四元] G=(VT , VN , S, δ) | • VT : A set of terminal symbols. [终结符]
p15: Grammar[文法] | • δ : A set of productions. [产生式] | ◆ specify the manner in which the terminals and non-terminals can be
p16: Grammar[文法] | • Example Grammar: | 𝜹 ：
p17: Context Free Grammar[上下文无关文法] | • To check whether a program is well-formed requires a | specification of what is a well-formed program [语法定义]
p18: Context Free Grammar[上下文无关文法] | • Formal definition [形式化定义] : 4 components G=(VT , VN , S, δ) | ◆ VT : A set of terminal symbols. [终结符]
p19: • Usually, we can only write the δ [简写，只需写产生式] | • Sometimes, Write “G[E]/G(E)” before the production, where G is | the grammar name and E is the start symbol. [文法名和开始符号]
p20: Grammar Convention[文法的一些约定] | • Merge rules sharing the same left-hand side[规则合并] | ◆ 𝛼 → 𝛽1, 𝛼 → 𝛽2, … , 𝛼 → 𝛽𝑛
p21: Grammar Convention[文法的一些约定] | • These symbols are non-terminals: [使用这些符号表示非终结符] | ◆ Uppercase letters early in the alphabet, such as A, B, C [靠前的大写字母]
p22: Grammar Convention[文法的一些约定] | • Uppercase letters late in the alphabet, such as X, Y, Z, represent | grammar symbols; that is, either non-terminals or terminals. [字母
p23: Grammar Convention[文法的一些约定] | • Example: | • G[E]/G(E)/G:
p24: Mind Map[思维导图] | Derivation | from grammar to language
p25: Derivation[推导] | • Production rule[产生式规则]: A → α, which means that A can be | constructed (or replaced) with α.
p26: Sentential form, Sentence, Language[句型&句子&语言] | • If S ⇒ α, where S is the start symbol of a grammar G, we say that α | is a sentential form of G. [句型]
p27: Sentential form, Sentence, Language[句型&句子&语言] | • Example: | • G[A]: A→ c | Ab
p28: Grammar and Derivation [文法与推导] | • Grammar is used to derive string or construct parser | • derivation is a sequence of applications of grammar rules
p29: Grammar and Derivation [文法与推导] | • Leftmost derivations [最左推导]: | • the leftmost non-terminal in each sentential is always chosen.
p30: Leftmost/Rightmost derivations [最左/最右推导] | • G[E]: E→T|E+T ; T→F|T*F ; F→(E)|i | Leftmost Derivation: Rightmost Derivation:
p31: Mind Map[思维导图] | remove ambiguity | Derivation
p32: Parse Trees [分析树] | • Derivations can be summarized as a parse tree [语法分析 | • A parse tree is a graphical representation of a
p33: Parse Trees [分析树] | E( ) | +E T
p34: Parse Trees [分析树] | E( ) | +E T
p35: Parse Trees [分析树] | • Leftmost / rightmost derivations | • can be summarized as a parse tree [语法分析树]
p36: Ambiguity[二义性] | • Whether a sentential form corresponds to only one grammar tree? | • Consider:
p37: Ambiguity[二义性] | • Unambiguous grammars are preferred for most parsers [文法最好没有 | 二义性]
p38: Ambiguity[二义性] | • Ambiguity for grammar: A grammar that produces more than one | parse tree for a sentence.[如果一个文法存在某个句子对应两颗不同的语法树，
p39: Ambiguity[二义性] | • Ambiguity is an undecidable problem[不可判定问题], | ◆ No algorithm exists that can accurately determine whether a grammar is
p40: Remove Ambiguity[消除二义性] | • Consider the example again: | • Grammar: G(E): E → i | E+E | E*E | (E)
p41: Revisit | • Syntax analysis | • Input: takes a string of tokens
p42: Mind Map[思维导图] | Regular | class 0
p43: Chomsky Grammar System[乔姆斯基文法体系] | • Chomsky established the formal language system in 1956. He | divided grammar into four types: 0, 1, 2, 3.
p44: Type 0: Unrestricted Grammar | • A Grammar G=(VT , VN , S, δ) is Type 0 [无限制文法,短语结构文法], if each production | α → β of G:
p45: Type 1: Context Sensitive Grammar | • A Grammar G=(VT , VN , S, δ) is Type 1 [上下文有关文法], if each production | α → β of G:
p46: Type 2: Context Free Grammar | • A Grammar G=(VT , VN , S, δ) is Type 2 [上下文无关文法], if each production | A → α of G:
p47: Type 3: Regular Grammar | • A Grammar G=(VT , VN , S, δ) is Type 3 [正则文法], if each production | A→aB or A→a of G:
p48: Type 3: Regular Grammar | Source: Prof Wenjun Li @ SYSU
p49: Comparison | Type 3 Grammar | Type 2 Grammar
p50: In Practice[实际中] | • Most programming languages are not context-free language, or even context- | sensitive language.
p51: Others[其他] | • So, what exactly is parsing, or syntax analysis? | ◆ To process an input string based on a given grammar, and compose the
p52: Parse Tree VS Abstract Syntax Tree | • An abstract syntax tree (AST) is abbreviated representation[缩写表示] of a | parse tree
p53: Mind Map[思维导图] | remove ambiguity | definition
p54: • Grammar (and Chomsky Grammar System) | • Context Free Grammar, aparser uses CFG to | ◆ judge if an input str ∈ L(G)
p55: • Dragon Book | ◆Comprehensive Reading: |  Section 2.4, 4.1.1 for the introduction to

## 4.Syntax_Analysis_Top_Down.pdf (89 pages)
p1: 编译原理 | Complier Principles | Lecture 4
p2: Before we start... | So, please pay attention and keep on track!
p3: Mind Map[思维导图] | Syntax Analysis: Top-down parser | problem
p4: Mind Map[思维导图] | Syntax Analysis: Top-down parser | type 1 type 2
p5: Parser Type[语法分析类型] | • Most compilers use either Top-Down or Bottom-Up parsers. | • Bottom-up parsing [自底向上分析]
p6: Parser Type[语法分析类型] | • Top-Down parsing [自顶向下分析] | ◆Starting from the root (top) and create the leaves (down) of the parse tree in a
p7: Parser Type[语法分析类型] | • Top-Down parsing [自顶向下分析] | ◆Once a production is chosen, we try to match the terminal symbols in the
p8: Parser Type[语法分析类型] | ◆Example | ◆Grammar G(S): S → AB ; A → aA | a ; B → bB | b ;
p9: Revisit | Syntax Analysis: Top-down parser | problem
p10: Top-down Parsing[自顶向下分析] | • Recursive-descent parsing[RDP , 递归下降语法分析] | ◆A general form[通用形式] of top-down parsing.
p11: RDP with backtracking[回溯] | • RDP may require backtracking. | • Approach: for a non-terminal in the derivation, productions are tried
p12: RDP with backtracking[回溯] | • In the analysis process, when a non-terminal is successfully matched with | an alternative, the match may be temporary.
p13: Left Recursion Problem[左递归问题] | • A grammar is left recursive[左递归] if it has a | non-terminal A such that there is a derivation
p14: Left Recursion Problem[左递归问题] | • Immediate left recursion [直接/立即左递归] | ◆There is a production A → Aα.
p15: Remove Left Recursion[消除左递归] | • Immediate left recursion[直接左递归的消除] | ◆Grammar: A → A⍺ | β (⍺≠β, β doesn’t start with A)
p16: Remove Left Recursion[消除左递归] | • Immediate left recursion can be eliminated by the following | technique, which works for any number of A-productions.
p17: Remove Left Recursion[消除左递归] | • Non-Immediate left recursion[非直接左递归的消除] | ◆Grammar: S → Qc | c ; Q → Rb | b ; R → Sa | a.
p18: Remove Left Recursion[消除左递归] | • The following algorithm systematically eliminates left recursion | from a grammar[直接/间接]. It is guaranteed to work if:
p19: Remove Left Recursion[消除左递归] | ◆Step 1 : Arrange all non-terminals of grammar G in some order A1, A2,..., An; | ◆Step 2 : Execute in order obtained in Step 1:
p20: Remove Left Recursion[消除左递归] | • Example: Consider Grammar G(S): (ILR = immediate left recursion) | R → Sa | a Q → Rb | b S → Qc | c
p21: Remove Left Recursion[消除左递归] | (continue...) | (i=3,j=2) S → Sabc | abc | bc | c contains ILR.
p22: Remove Left Recursion[消除左递归] | • Question: What will happen if the order in step 1 is different | • Again, consider G(S): S → Qc | c Q → Rb | b R → Sa | a
p23: Recursive-descent parsing[递归下降语法分析] | • Recursive-descent parsing [RDP , 递归下降语法分析] | ◆ A general form of top-down parsing.
p24: Mind Map[思维导图] | Syntax Analysis: Top-down parser | type 1
p25: Predictive Parsing[预测分析] | • Predictive Parsing[预测分析法] | ◆A special case of recursive-descent parsing without backtracking[无回溯].
p26: Predictive Parsing[预测分析] | • A parser with no backtracking [无回溯]: select the correct | alternative through given next input terminal(s)[下一个输入符号/终结符]
p27: Common Prefix[共同前缀] | • G[S]: S → xAy; A → ** | *, If the current matching symbol is *, the | next step is to expand A, and A → α1 | α2 |…| αn . How to choose αi？
p28: Left factoring[提取公共左因子] | • For each non-terminal A, find the longest prefix α common to two | or more of its alternatives. If α ≠ ε, replace all of the A-
p29: Predictive Parsing[预测分析] | • Patterns in grammars that prevent predictive parsing [并非总是能预 | 测分析] :
p30: FIRST[终结首符集] | • During top-down parsing, FIRST and FOLLOW allow us to choose | which production to apply, based on the next input symbol.
p31: FOLLOW[后继终结符号集] | • Question: And then, if for an input symbol a and the non-terminal | A (A → α1 │ α2 │…│ αn) , but for any αi , a ∉ FIRST (αi), in this case,
p32: FOLLOW[后继终结符号集] | • Question: for an input symbol a and the non-terminal A (A → α1 | │ α2 │…│ αn), a ∉ FIRST(αi), in this case, how to choose αi, or draw
p33: Compute FIRST[计算FIRST集合的方法] | • To compute FIRST(X) for all grammar symbol X, apply the following | rules until no more terminals or ε can be added to any FIRST set:
p34: Compute FIRST[计算FIRST集合的方法] | • Next, we can compute FIRST for any string ⍺ = X1X2…Xn [符号串] | ◆Add all non-ε symbols of FIRST(X1) to FlRST(⍺).
p35: Compute FIRST[计算FIRST集合的方法] | • Example: G[E]: E → TE’ ; E’ → +TE’ | ε ; T → FT’ ; T’ → *FT’ | ε ; F → | (E) | id , compute the FIRST set of each non-terminal.
p36: Compute FIRST[计算FIRST集合的方法] | • Example: G[E]: E → TE’ ; E’ → +TE’ | ε ; T → FT’ ; T’ → *FT’ | ε ; F → | (E) | id , compute the FIRST set of each non-terminal.
p37: Compute FIRST[计算FIRST集合的方法] | • Example: G[E]: E → TE’ ; E’ → +TE’ | ε ; T → FT’ ; T’ → *FT’ | ε ; F → | (E) | id , compute the FIRST set of each non-terminal.
p38: Compute FIRST[计算FIRST集合的方法] | • Example: G[E]: E → TE’ ; E’ → +TE’ | ε ; T → FT’ ; T’ → *FT’ | ε ; F → | (E) | id , compute the FIRST set of each non-terminal.
p39: Compute FOLLOW[计算FOLLOW集合的方法] | • To compute FOLLOW(A) for all non-terminals A, apply the following | rules until nothing can be added to any FOLLOW set.
p40: Compute FOLLOW[计算FOLLOW集合的方法] | • Example: G[E]: E → TE’ ; E’ → +TE’ | ε ; T → FT’ ; T’ → *FT’ | ε ; F → | (E) | id , compute the FOLLOW set of each non-terminal.
p41: Compute FOLLOW[计算FOLLOW集合的方法] | • Example: G[E]: E → TE’ ; E’ → +TE’ | ε ; T → FT’ ; T’ → *FT’ | ε ; F → | (E) | id , compute the FOLLOW set of each non-terminal.
p42: Compute FOLLOW[计算FOLLOW集合的方法] | • Example: G[E]: E → TE’ ; E’ → +TE’ | ε ; T → FT’ ; T’ → *FT’ | ε ; F → | (E) | id , compute the FOLLOW set of each non-terminal.
p43: Compute FOLLOW[计算FOLLOW集合的方法] | • Example: G[E]: E → TE’ ; E’ → +TE’ | ε ; T → FT’ ; T’ → *FT’ | ε ; F → | (E) | id , compute the FOLLOW set of each non-terminal.
p44: Compute FOLLOW[计算FOLLOW集合的方法] | • Example: G[E]: E → TE’ ; E’ → +TE’ | ε ; T → FT’ ; T’ → *FT’ | ε ; F → | (E) | id , compute the FOLLOW set of each non-terminal.
p45: Revisit | • Top-down Parsing | • Recursive-descent parsing [RDP , 递归下降语法分析]
p46: Compute FIRST (Revisit) | • To compute FIRST(X) for all grammar symbol X, apply the following | rules until no more terminals or ε can be added to any FIRST set:
p47: Compute FIRST (Revisit) | • Next, we can compute FIRST for any string ⍺ = X1X2…Xn [符号串] | ◆Add all non-ε symbols of FIRST(X1) to FlRST(⍺).
p48: Compute FIRST (Revisit) | • Example: G[E]: E → TE’ ; E’ → +TE’ | ε ; T → FT’ ; T’ → *FT’ | ε ; F → | (E) | id , compute the FIRST set of each non-terminal.
p49: Compute FOLLOW (Revisit) | • To compute FOLLOW(A) for all non-terminals A, apply the following | rules until nothing can be added to any FOLLOW set.
p50: Compute FOLLOW (Revisit) | • G[E]: E → TE’ ; E’ → +TE’ | ε ; T → FT’ ; T’ → *FT’ | ε ; F → (E) | id | ◆FIRST(E):{ (, id };FIRST(T):{ (, id };FIRST(E’):{ +, ε };FIRST(T’):{ *, ε };FIRST(F):{ (, id }.
p51: LL(1) Grammar[LL(1)文法] | • Predictive parsers, that is, recursive-descent parsers needing no | backtracking, can be constructed for a class of grammars called LL(1).
p52: LL(1) Grammar[LL(1)文法] | • The first two conditions are equivalent to the statement that | FIRST(α) and FIRST(β) are disjoint sets [不相交的集合].
p53: LL(1)/LL(k) Grammar[LL(1)/LL(k)文法] | • LL (1) grammar. | ◆L: The first "L" in LL(1) stands for scanning the input from left to right.
p54: LL(1) Parser Implementation[实现] | • Recursive LL(1) parser for G[S]: S → A | B; | A → a; B → b.
p55: Non-recursive LL(1) Parser [非递归] | • Input buffer[输入串]: contains the | string to be parsed, followed by
p56: LL(1) Parse Table [预测分析表] | G[E]: | F → (E) | id
p57: LL(1) Parsing Algorithm [非递归算法] | • Initial state [初始态] | ◆Input: A string w and a parsing table M for grammar G. Input Buffer: w$.
p58: LL(1) Parsing Algorithm [非递归算法] | • Algorithm Step-by-Step based on <X, a>: | ◆X: symbol at the top of the stack
p59: Use the Parse Table [使用表进行预测分析] | • When using parse table for predictive parsers, if the grammar does | not conform to the specification of LL (1) grammar:
p60: Use the Parse Table [使用表进行预测分析] | • recognize “id + id * id” G[E]: | F → (E) | id
p61: Use the Parse Table [使用表进行预测分析] | • recognize “id + id * id” G[E]: | F → (E) | idPredictive Parsing
p62: Use the Parse Table [使用表进行预测分析] | • recognize “id + id * id” G[E]: | F → (E) | idPredictive Parsing
p63: Use the Parse Table [使用表进行预测分析] | • recognize “id + id * id” G[E]: | F → (E) | idPredictive Parsing
p64: Use the Parse Table [使用表进行预测分析] | • recognize “id + id * id” G[E]: | F → (E) | idPredictive Parsing
p65: Use the Parse Table [使用表进行预测分析] | • recognize “id + id * id” G[E]: | F → (E) | idPredictive Parsing
p66: Use the Parse Table [使用表进行预测分析] | • recognize “id + id * id” G[E]: | F → (E) | idPredictive Parsing
p67: Use the Parse Table [使用表进行预测分析] | • recognize “id + id * id” G[E]: | F → (E) | idPredictive Parsing
p68: Use the Parse Table [使用表进行预测分析] | • recognize “id + id * id” G[E]: | F → (E) | idPredictive Parsing
p69: Use the Parse Table [使用表进行预测分析] | • recognize “id + id * id” G[E]: | F → (E) | idPredictive Parsing
p70: Use the Parse Table [使用表进行预测分析] | • recognize “id + id * id” G[E]: | F → (E) | idPredictive Parsing
p71: Use the Parse Table [使用表进行预测分析] | • recognize “id + id * id” G[E]: | F → (E) | idPredictive Parsing
p72: • recognize “id + id * id” | Use the Parse Table [使用表进行预测分析] | G[E]:
p73: Use the Parse Table [使用表进行预测分析] | • recognize “id + id * id” G[E]: | F → (E) | idPredictive Parsing
p74: Use the Parse Table [使用表进行预测分析] | • recognize “id + id * id” G[E]: | F → (E) | idPredictive Parsing
p75: Use the Parse Table [使用表进行预测分析] | • recognize “id + id * id” G[E]: | F → (E) | idPredictive Parsing
p76: Use the Parse Table [使用表进行预测分析] | • recognize “id + id * id” G[E]: | F → (E) | idPredictive Parsing
p77: Matched Stack Input Action | E$ id + id * id$ E → TE’ | TE’$ id + id * id$ T → FT’
p78: Construct LL(1) Parse Table [构建预测分析表] | • Use FIRST and FOLLOW sets for a predictive parsing table M[A,a], | and the algorithm is based on the following idea:
p79: Construct LL(1) Parse Table [构建预测分析表] | • Algorithm: For each production A → α of the grammar: | ◆For each terminal a ∈ FIRST(α), add A → α to M[A, a].
p80: Construct LL(1) Parse Table [构建预测分析表] | • Algorithm: For each production A → α of the grammar: | ◆If ε ∈ FlRST(α), then for each terminal b in FOLLOW(A), add A → α to
p81: Construct LL(1) Parse Table [构建预测分析表] | Symbol FIRST FOLLOW | E (, i $, )
p82: Determine If Grammar is LL(1)[判断LL(1)文法] | • Observation [直观依据] | ◆If a grammar is LL(1), each of its LL(1) table entry contains at most one rule.
p83: Non-LL(1) Grammar [非LL(1)文法] | • Assume that a grammar is not LL(1). How to solve? | ◆Case1- the language may still be LL(1)
p84: LL(1) Time and Space Complexity[复杂度] | • Linear time and space relative to the length of input. | • Time: each input symbol is consumed within a constant number of
p85: LL(1) Time and Space Complexity[复杂度] | • Space: smaller than input (after removing X → ε) | ◆Right side of production is always longer or equal to left side of production
p86: Summary | Syntax Analysis: Top-down parser | problem
p87: Summary | • Top-down Parsing; RDP with backtracking, predictive parsing. | • (Immediate / Non-immediate) Left Recursion and how to resolve
p88: • RDP [递归下降分析] | • left recursion [左递归] | • Remove Left Recursion [消除直接/间接左递归]
p89: • Dragon Book | ◆Comprehensive Reading: |  Section 4.1.2 and 4.4.1 for the introduction to

## 5.Syntax_Analysis_Bottom_Up.pdf (206 pages)
p1: 编译原理 | Complier Principles | Lecture 5
p2: Contents | LR family parsers | Parser table
p3: Contents | Bottom-up parser | Shift-Reduce
p4: Bottom-up parsing[自下而上分析] | • Bottom-up parsing [自下而上分析] | ◆Start from the input string, and gradually reduce[规约] it (the
p5: Bottom-up parsing[自下而上分析] | • Bottom-up parsing [自下而上分析] | ◆ Parser code structure nothing like grammar
p6: Bottom-up: Shift-Reduce [移入-归约] | • Shift-reduce parsing is a form of bottom-up parsing in which a | stack[栈] holds grammar symbols and an input buffer holds the
p7: Bottom-up: Shift-Reduce [移入-归约] | • There are four actions that a shift-reduce parser can make: | ◆Shift[移入]: Shift the next input symbol onto the top of the stack.
p8: Bottom-up: Shift-Reduce [移入-归约] | Example: | • G(S): S → aAcBe;
p9: Key Issue [一个关键问题] | • The key decisions during bottom-up | parsing are about (1) when to shift
p10: Handle [句柄] | • Right-sentential form [最右句型]: a sentential form that occurs in the | rightmost derivation[规范推导].
p11: Handle [句柄] | • Simple Phrase[直接短语]: If α1Aα2 is a right sentential form of G(S), and | S ⇒ α1Aα2 ⇒ α1βα2, then β is a simple phrase of α1Aα2.
p12: • G(E): E → T | E+T; T → F | T*F; F → (E) | a | b | c | • For sentential form a * b + c | • Phrase: a*b+c, a*b, a, b, c
p13: • Gramar G(E): | E → E+T|T | T → T*F | F
p14: • Gramar G(E): E → E+T|T T → T*F | F F → (E) | id | • Sentential form: T + T*F + id | • Phrase： E1: T+T*F+id E2: T+T*F E3: T T1: T*F T2, F1: id
p15: • Gramar G(E): E → E+T|T T → T*F | F F → (E) | id | • Sentential form: T + T*F + id | • Phrase： E1: T+T*F+id E2: T+T*F E3: T T1: T*F T2, F1: id
p16: • Gramar G(E): E → E+T|T T → T*F | F F → (E) | id | • Sentential form: T + T*F + id | • Phrase： E1: T+T*F+id E2: T+T*F E3: T T1: T*F T2, F1: id
p17: • Gramar G(E): E → E+T|T T → T*F | F F → (E) | id | • Sentential form: T + T*F + id | • Phrase： E1: T+T*F+id E2: T+T*F E3: T T1: T*F T2, F1: id
p18: • Gramar G(E): E → E+T|T T → T*F | F F → (E) | id | • Sentential form: T + T*F + id | • Phrase： E1: T+T*F+id E2: T+T*F E3: T T1: T*F T2, F1: id
p19: • Gramar G(E): E → E+T|T T → T*F | F F → (E) | id | • Sentential form: T + T*F + id | • Phrase： E1: T+T*F+id E2: T+T*F E3: T T1: T*F T2, F1: id
p20: • Gramar G(E): E → E+T|T T → T*F | F F → (E) | id | • Sentential form: T + T*F + id | • Phrase： E1: T+T*F+id E2: T+T*F E3: T T1: T*F T2, F1: id
p21: • Gramar G(E): E → E+T|T T → T*F | F F → (E) | id | • Sentential form: T + T*F + id | • Phrase： E1: T+T*F+id E2: T+T*F E3: T T1: T*F T2, F1: id
p22: • Gramar G(E): E → E+T|T T → T*F | F F → (E) | id | • Sentential form: T + T*F + id | • Phrase： E1: T+T*F+id E2: T+T*F E3: T T1: T*F T2, F1: id
p23: • Gramar G(E): E → E+T|T T → T*F | F F → (E) | id | • Sentential form: T + T*F + id | • Phrase： E1: T+T*F+id E2: T+T*F E3: T T1: T*F T2, F1: id
p24: • G(S): S → aAcBe; A → b; A → Ab; B → d. | Stack Input Action | $ abbcde$ Shift
p25: Handle Always Occurs at Stack Top | • Does handle appear outside the stack? | ◆It can, but handle will eventually be shifted in, placing it at top of stack.
p26: Viable Prefix [活前缀] | • A viable prefix[活前缀/可行前缀] is a prefix of a right-sentential form that | does not pass the end of the rightmost handle of that sentential form.
p27: Viable Prefix [活前缀] | • Example 2: G(S): S → aAcBe; A → b; A → Ab; B → d. | • “aAcde” is a right sentential form, it is split between the stack and the
p28: Conflicts[冲突] | • Conflicts arise with ambiguous | grammars.
p29: Conflicts[冲突] | • Conflicts arise with ambiguous | grammars.
p30: Conflicts[冲突] | • Conflicts arise with ambiguous grammars. | • Grammar: E → E*E | E+E | (E) | id
p31: • Handles always appear at the top of the stack | ◆ Never in middle of stack | ◆ Justifies use of stack in shift–reduce parsing
p32: Contents | LR family parsers | Parser table
p33: Types of Bottom-Up Parsers | • Different types of bottom-up parsers: | ◆ Simple precedence parsers
p34: LR(k) Parser | • LR(k) : member of LR family of parsers | ◆ "L" stands for left-to-right scanning of the input.
p35: LR Parser | • The stack holds a sequence of states, S0S1…Sm (Sm is the top) | ◆ States are to track where we are in a parse.
p36: Bottom-up (Revisit) | • LR(0) Parser: | Stat
p37: Parse Table | • The LR-parsing algorithm must decide when to shift and when to | reduce (and in the latter case, by which production).
p38: Action table[动作表] | • The action table is indexed by a state of the | parser and a terminal and contains three types
p39: Possible Actions[可能的动作] | • ACTION[Sm, ai] has four possible actions: | • Shift (sx): the handle is not completed loaded in the stack
p40: Goto Table[跳转表] | • The goto table is indexed by a state of the parser and a | nonterminal
p41: Parse Table | State Action Goto | * + 0 1 $ E B
p42: Parser Actions | • If ACTION[sm, ai] = sx, then do shift: | ◆ Shift ai on stack, which is removed from the input
p43: Parser Actions | • If ACTION[sm, ai] = rx, then do reduce: | ◆Pops k (states, symbols) from stack
p44: LR Parsing Program | • Input: string ω and parse table with ACTION/GOTO | • Output: reduction steps of ω, or error
p45: Example: Parse Table | • This example of LR parsing uses the | following small grammar with goal
p46: Example: Parse Table | • Grammar: | (1) E → E * B
p47: Example: Parsing steps | • (1) E → E * B (2) E → E + B (3) E → B (4) B → 0 (5) B → 1 | Stack input ACTION GOTO
p48: Example: Parsing steps | • (1) E → E * B (2) E → E + B (3) E → B (4) B → 0 (5) B → 1 | Stack input ACTION GOTO
p49: Example: Parsing steps | • (1) E → E * B (2) E → E + B (3) E → B (4) B → 0 (5) B → 1 | Stack input ACTION GOTO
p50: Example: Parsing steps | • (1) E → E * B (2) E → E + B (3) E → B (4) B → 0 (5) B → 1 | Stack input ACTION GOTO
p51: Example: Parsing steps | • (1) E → E * B (2) E → E + B (3) E → B (4) B → 0 (5) B → 1 | Stack input ACTION GOTO
p52: Example: Parsing steps | • (1) E → E * B (2) E → E + B (3) E → B (4) B → 0 (5) B → 1 | Stack input ACTION GOTO
p53: Example: Parsing steps | • (1) E → E * B (2) E → E + B (3) E → B (4) B → 0 (5) B → 1 | Stack input ACTION GOTO
p54: Example: Parsing steps | • (1) E → E * B (2) E → E + B (3) E → B (4) B → 0 (5) B → 1 | Stack input ACTION GOTO
p55: Example: Parsing steps | • (1) E → E * B (2) E → E + B (3) E → B (4) B → 0 (5) B → 1 | Stack input ACTION GOTO
p56: Example: Parsing steps | • (1) E → E * B (2) E → E + B (3) E → B (4) B → 0 (5) B → 1 | Stack input ACTION GOTO
p57: Example: Parsing steps | • (1) E → E * B (2) E → E + B (3) E → B (4) B → 0 (5) B → 1 | Stack input ACTION GOTO
p58: Example: Parsing steps | • (1) E → E * B (2) E → E + B (3) E → B (4) B → 0 (5) B → 1 | Stack input ACTION GOTO
p59: Revisit | LR family parsers | Parser table
p60: Bottom-up (Revisit) | • Shift-Reduce parser: | • From the input to the start symbol, rightmost derivation in reverse.
p61: Bottom-up (Revisit) | • LR(0) parser: | • The stack holds a sequence of states, S0S1…Sm (Sm is the top)
p62: Construct Parse Table | • Construct parsing table: | • identify the possible states and arrange the transitions among them.
p63: • How does a shift-reduce parser know when to shift and when to | reduce? [Parser怎么知道何时移进, 何时规约] | ◆Using the figure below as an example, with stack content $T and next input
p64: Item[项目] | • The parsing table is based on the notion of LR(0) items (simply | called items here) which are grammar rules with a special dot
p65: • A → • XYZ | ◆Indicates that we hope to see a string derivable from XYZ next on the input | • A → X • YZ
p66: State[状态] | • Example: | ◆Suppose we are currently in this position: A → X • YZ
p67: Augmented Grammar[增广文法] | • We want to start with an item with a dot before the start symbol | S (•S) and move to an item with a dot after S (S•)
p68: • Each FA state corresponding to a set of items | • How to construct a state? -- closure operation | ◆Closure: the action of adding equivalent items to a set
p69: Grammar | (0) S’ -> S | (1) S -> BB
p70: Example (cont.) | “state j” refers to the state of the | set of items Ij
p71: • Closure of item sets: if I is a set of items for a grammar G, then | CLOSURE(I) is the set of items constructed from I by the two rules: | 1. Initially, add every item in I to CLOSURE(I)
p72: • GOTO(I, X): returns state (set of items) that can be reached by | advancing I by X | ◆ I is a set of items and X is a grammar symbol
p73: • Create augmented grammar G’ for G: [增广文法] | ◆ Given G: S → α | β, create G’: S’ → S , S → α | β | ◆ Creates a single rule S’ → S that when reduced, signals acceptance
p74: • Compute canonical LR(0) collection[规范LR(0)项集族, C], i.e., set of all states in DFA | [DFA中的所有状态的集合] | ◆ A collection of sets of LR(0) items that provides the basis for constructing a
p75: • The LR(0) automaton: a shift action means the transition of the current | state to a new state | ◆ State: a set of items in C
p76: [建立第一个项] | S0= Closure({S’→ · S}) | = {S’→ · S, S → · BB, B → · aB, B → · b} (I0)
p77: • ACTION [Si, a]: | ◆ If [A→α·aβ] is in Si and goto(Si, a) = Sj, where “a” is a terminal, then | ACTION[Si, a] = Sj (shift j)
p78: The example | (0) S’ → S | (1) S → BB
p79: • Construct LR(0) automaton from the Grammar | • Assumptions: | ◆ Input buffer contains ⍺
p80: • The parser must be able to determine what action to take in each | state without looking at any further input symbols | ◆ By only considering what the parsing stack contains so far
p81: • LR(0) has a reduce-reduce conflict if： | ◆ Any state has two reduce items: | ◆ X → β · and Y → ω ·
p82: • LR(0) conflicts are generally caused by reduce actions | ◆Shift-Reduce conflict | ◆Reduce-Reduce conflict
p83: • Construct LR(0) automaton from the Grammar | • Assumptions: | ◆ Input buffer contains ⍺
p84: • The parser must be able to determine what action to take in each | state without looking at any further input symbols | ◆ By only considering what the parsing stack contains so far
p85: Revisit | LR family parsers | Parser table
p86: Bottom-up (Revisit) | • Construction of LR(0) table | • Tell the parser when to shift/reduce
p87: Example (Revisit) | “state j” refers to the state of the | set of items Ij
p88: Bottom-up (Revisit) | ⚫ We want to see S • from • S | ⚫ The construction of LR(0) automaton
p89: Bottom-up (Revisit) | ⚫ We want to see S • from • S | ⚫ The construction of LR(0) automaton
p90: • Create augmented grammar G’ for G: [增广文法] | ◆ Given G: S → α | β, create G’: S’ → S , S → α | β | ◆ Creates a single rule S’ → S that when reduced, signals acceptance
p91: [建立第一个项] | S0= Closure({S’→ · S}) | = {S’→ · S, S → · BB, B → · aB, B → · b} (I0)
p92: The example (Revisit) | (0) S’ → S | (1) S → BB
p93: • LR(0) has a reduce-reduce conflict if： | ◆ Any state has two reduce items: | ◆ X → β · and Y → ω ·
p94: • LR(0) conflicts are generally caused by reduce actions | ◆Shift-Reduce conflict | ◆Reduce-Reduce conflict
p95: • LR(0) is the simplest LR parsing | ◆ Table-driven shift-reduce parser |  Action table[s, a] + Goto table[s, X]
p96: Contents | LR family parsers | Parser table
p97: LR(0) Example (revisit) | (0) S’ → S | (1) S → BB
p98: • SLR (Simple LR) | ◆ the same LR(0) configurating sets Use the same LR(0) configurating sets | and have the same table structure and parser operation
p99: • Suppose id is the first token of the input | ◆ S1: the set has a shift-reduce conflict and a reduce-reduce conflict | ◆ Follow(T) = { +, ), ], $ }, Follow(V) = { = }
p100: • A grammar is SLR(1) if the following two conditions hold for | each configurating set: | 1. For any item A → u· xvin the set, with terminal x, there is no
p101: • SLR(1) v.s. LR(0) | ◆ Adding just one token of lookahead and using the Follow set greatly expands | the class of grammars that can be parsed without conflict
p102: • When we have a complete configuration (i.e., dot at the end) such as X –> u· ,we | know that it is reducible | ◆ We allow such a reduction as long as the next symbol is in Follow(X).
p103: • For input string : id = id | ◆ Initially, at S0, push id | ◆ Move to S5, after shifting id to
p104: • Choices upon seeing = coming up in | the input: | ◆ Action[2, =] = s6 :
p105: Contents | LR family parsers | Parser table
p106: • We don’t need to see additional symbols beyond the first token in the input, | we have already seen the info that allows us to determine the correct choice | [lookahead展望信息已足够]
p107: • LR parsing adds the required extra info into the state | ◆ By redefining items to include a terminal symbol as an added component | [让项目中包含终结符]
p108: • When to reduce? | ◆ LR(0): if the configuration set has a completed item (i.e., dot at the end) | ◆ SLR(1): only if the next input token is in the Follow set
p109: LR(1) Construction | • Configuration sets | ◆Sets construction are essentially the same with SLR, but differing on
p110: LR(1) Construction (cont.) | • Goto(I, X) | ◆For item [A -> u· Xv, a] in I, Goto(I, X) = Closure ([A -> uX· v, a])
p111: Revisit | LR family parsers | Parser table
p112: • LR(0) Limitations | ◆Parses without using lookahead - weakest, not used much in practice | ◆An completed item (A → ⍺·) is reduced immediately
p113: • SLR(1): Simple LR(1) with one lookahead | ◆ Same LR(0) configurating sets, table structure, and parser operation. | ◆ Allow both shift and reduce items as well as multiple reduce items.
p114: • SLR(1) Grammar | 1. For any item A → u· xvin the set, with terminal x, there is no complete | item B → w· in that set with x in Follow(B)
p115: • LR(1): Left-to-right scan and rightmost derivation with one | lookahead | ◆ Adding a bit more information to drive the parsing.
p116: LRs Revisit | • Redefining items to include a terminal symbol as an added | component [让项目中包含终结符]
p117: LRs Revisit | • Closure(I) | ◆Given each item [A -> u·Bv, a] in I, for each production rule B -> w in G’,
p118: LRs Revisit | • Closure(I) | • For [A -> u·Bv, a], if b ∈ First(va), then [B -> · w, b]
p119: S’ → S ·,$S | S’ → ·S, $ | S → · XX, $
p120: • Shift[移进] | ◆ Same as LR(0) and SLR(1) | ◆ Don’t care the lookahead symbols
p121: (0) S’ -> S | (1) S -> XX | (2) X -> aX
p122: LR(1) Grammars | • Every SLR(1) grammar is LR(1), but the LR(1) parser may have | more states than SLR(1) parser
p123: Contents | LR family parsers | Parser table
p124: LALR(1) Parser | • What’s the drawbacks of LR(1)? | ◆ With state splitting, the LR(1) parser can have many more states than
p125: S’ → S ·,$S | S’ → ·S, $ | S → · XX, $
p126: State Merging[状态合并] | • Merge states with the same core | ◆ Core: LR(1) items minus the lookahead (i.e., LR(0) items)
p127: State Merging (cont.) | Stat | a b $ S X
p128: Merge Effects[合并效果] | 1. Merging of states can introduce conflicts[引入归约-归约冲突] | ◆ Can introduce reduce-reduce (r-r) conflicts
p129: • Shift-reduce conflicts are not introduced by merging | • Suppose: | Sij contains: [A -> ⍺· , a] reduce on input a
p130: Merge Conflict: Reduce-Reduce | • Reduce-reduce conflicts can be introduced by merging | • In this case, we say the grammar is not LALR(1)
p131: Merge Effects[合并效果] | 1. Merging of states can introduce conflicts[引入归约-归约冲突] | ◆ Can introduce reduce-reduce (r-r) conflicts
p132: Example: Error Delay | a b $ S X | 0 s3 s4 1 2
p133: Example: Error Delay(cont.) | Grammar | (0) S’ -> S (1) S -> XX (2) X -> aX (3) X -> b
p134: LALR Table Construction[解析表构建] | • LALR(1) parsing table is built from the configuration sets in the | same way as LR(1)[同样方法构建的项目集]
p135: LALR Table Construction (Cont.) | • Brute force[暴力方法] | ◆Construct LR(1) states, then merge states with same core
p136: LALR(1) Grammars | • For a grammar, if the LALR(1) parse table has no conflicts, | then we say the grammar is LALR(1)
p137: • LALR(1) provides a good balancing between LR(1) and SLR(1) | ◆ Range of grammars supported: LR > LALR > SLR | ◆ Number of states in the table: LR > LALR = SLR
p138: LL vs. LR Parsing (LL < LR) | • LL(k) parser, each expansion A -> ⍺ is decided based on | ◆Current non-terminal at the top of the stack[依赖LHS]
p139: Hierarchy of Grammars[文法层级]
p140: 编译原理 | Complier Principles | Lecture 3
p141: Compilation Phases[编译阶段] | (keyword, while) | (id, y)
p142: Mind Map[思维导图] | remove ambiguity | definition
p143: Syntax analysis | • Syntax analysis – the second phase of compilation | ◆ Input: a sequence of token provided by the Lexical Analysis
p144: Sentential form, Sentence, Language[句型&句子&语言] | • Example: | • G[A]: A→ c | Ab
p145: Overall Concepts | • Derivation | ◆ The application of the productions (from LHS to RHS)
p146: Chomsky Grammar System[乔姆斯基文法体系] | • Chomsky established the formal language system in 1956. He | divided grammar into four types: 0, 1, 2, 3.
p147: Chomsky Grammar System[乔姆斯基文法体系] | Source: Prof Wenjun Li @ SYSU
p148: Parse Tree VS Abstract Syntax Tree | • An abstract syntax tree (AST) is abbreviated representation[缩写表示] of a | parse tree
p149: Parsers | • Syntax analysis takes a sentence as the input, and outputs the | parse tree or AST of the sentence
p150: Top-down | problem | type 1
p151: Top-down Parsers | • Top-down Parsing | • Recursive-descent parsing [RDP , 递归下降语法分析]
p152: Remove Left Recursion[消除左递归] | • Immediate left recursion can be eliminated by the following | technique, which works for any number of A-productions.
p153: Compute FIRST | • To compute FIRST(X) for all grammar symbol X, apply the following | rules until no more terminals or ε can be added to any FIRST set:
p154: Compute FIRST | • Next, we can compute FIRST for any string ⍺ = X1X2…Xn [符号串] | ◆Add all non-ε symbols of FIRST(X1) to FlRST(⍺).
p155: Compute FIRST | • Example: G[E]: E → TE’ ; E’ → +TE’ | ε ; T → FT’ ; T’ → *FT’ | ε ; F → | (E) | id , compute the FIRST set of each non-terminal.
p156: Compute FOLLOW | • To compute FOLLOW(A) for all non-terminals A, apply the following | rules until nothing can be added to any FOLLOW set.
p157: Compute FOLLOW | • G[E]: E → TE’ ; E’ → +TE’ | ε ; T → FT’ ; T’ → *FT’ | ε ; F → (E) | id | ◆FIRST(E):{ (, id };FIRST(T):{ (, id };FIRST(E’):{ +, ε };FIRST(T’):{ *, ε };FIRST(F):{ (, id }.
p158: Non-recursive LL(1) Parser [非递归] | • Input buffer[输入串]: contains the | string to be parsed, followed by
p159: LL(1) Parse Table [预测分析表] | G[E]: | F → (E) | id
p160: LL(1) Parsing Algorithm [非递归算法] | • Algorithm Step-by-Step based on <X, a>: | ◆X: symbol at the top of the stack
p161: Bottom-Up | LR family parsers | Parser table
p162: Bottom-up: Shift-Reduce [移入-归约] | • Shift-reduce parsing is a form of bottom-up parsing in which a | stack[栈] holds grammar symbols and an input buffer holds the
p163: • G(E): E → T | E+T; T → F | T*F; F → (E) | a | b | c | • For sentential form a * b + c | • Phrase: a*b+c, a*b, a, b, c
p164: Viable Prefix [活前缀] | • A viable prefix[活前缀/可行前缀] is a prefix of a right-sentential form that | does not pass the end of the rightmost handle of that sentential form.
p165: LR(k) Parser | • LR(k) : member of LR family of parsers | ◆ "L" stands for left-to-right scanning of the input.
p166: LR Parser | • The stack holds a sequence of states, S0S1…Sm | ◆ States are to track where we are in a parse.
p167: Possible Actions[可能的动作] | • ACTION[Sm, ai] has four possible actions: | • Shift (sx): the handle is not completed loaded in the stack
p168: Construct Parse Table | • Construct parsing table: | • identify the possible states and arrange the transitions among them.
p169: Item[项目] | • The parsing table is based on the notion of LR(0) items (simply | called items here) which are grammar rules with a special dot
p170: • Each FA state corresponding to a set of items | • How to construct a state? -- closure operation | ◆Closure: the action of adding equivalent items to a set
p171: • Closure of item sets: if I is a set of items for a grammar G, then | CLOSURE(I) is the set of items constructed from I by the two rules: | 1. Initially, add every item in I to CLOSURE(I)
p172: • GOTO(I, X): returns state (set of items) that can be reached by | advancing I by X | ◆ I is a set of items and X is a grammar symbol
p173: [建立第一个项] | S0= Closure({S’→ · S}) | = {S’→ · S, S → · BB, B → · aB, B → · b} (I0)
p174: Example (cont.) | “state j” refers to the state of the | set of items Ij
p175: • Create augmented grammar G’ for G: [增广文法] | ◆ Given G: S → α | β, create G’: S’ → S , S → α | β | ◆ Creates a single rule S’ → S that when reduced, signals acceptance
p176: • LR(0) has a reduce-reduce conflict if： | ◆ Any state has two reduce items: | ◆ X → β · and Y → ω ·
p177: • SLR(1): Simple LR(1) with one lookahead | ◆ Same LR(0) configurating sets, table structure, and parser operation. | ◆ Allow both shift and reduce items as well as multiple reduce items.
p178: • A grammar is SLR(1) if the following two conditions hold for | each configurating set: | 1. For any item A → u· xvin the set, with terminal x, there is no
p179: • LR parsing adds the required extra info into the state | ◆ By redefining items to include a terminal symbol as an added component | [让项目中包含终结符]
p180: • When to reduce? | ◆ LR(0): if the configuration set has a completed item (i.e., dot at the end) | ◆ SLR(1): only if the next input token is in the Follow set
p181: LR(1) Construction | • Configuration sets | ◆Sets construction are essentially the same with SLR, but differing on
p182: LR(1) Construction (cont.) | • Goto(I, X) | ◆For item [A -> u· Xv, a] in I, Goto(I, X) = Closure ([A -> uX· v, a])
p183: • Shift[移进] | ◆ Same as LR(0) and SLR(1) | ◆ Don’t care the lookahead symbols
p184: (0) S’ -> S | (1) S -> XX | (2) X -> aX
p185: LALR(1) Parser | • What’s the drawbacks of LR(1)? | ◆ With state splitting, the LR(1) parser can have many more states than
p186: S’ → S ·,$S | S’ → ·S, $ | S → · XX, $
p187: State Merging[状态合并] | • Merge states with the same core | ◆ Core: LR(1) items minus the lookahead (i.e., LR(0) items)
p188: State Merging (cont.) | Stat | a b $ S X
p189: Merge Effects[合并效果] | 1. Merging of states can introduce conflicts[引入归约-归约冲突] | ◆ Can introduce reduce-reduce (r-r) conflicts
p190: • 正则表达式可以表达语言𝐿 = {𝑥𝑛𝑦𝑧𝑛, 1 ≤ 𝑛 ≤ 10}吗? | • 可以，任何有穷集都是正规集，都可以用正规表达式来描述 | • 正则表达式可以表达语言𝐿 = {𝑥𝑛𝑦𝑧𝑛, n > 0}吗?
p191: • 对于一个无二义性文法G，它的一个句子的最左与最右推导产生的分析树一 | 定是一样的吗? | • 对的，是这样的。语法树会隐去推导顺序
p192: • 找出以下文法中的句型的所有短语，直接短语，句柄 | • 文法: G(E): E → T | E+T; T → F | T*F; F → (E) | a | b | c | • 句型: a * b + c
p193: • 给定一下文法G(S), 请构建该文法的LL(1)分析表 | • S → A | • A → 
p194: • 给定一下文法G(S) , 请构建识别活前缀的DFA与LR(1)分析表 | • S → A | • A → A + A | B + +
p195: • 给定一下文法G(S) , 请构建识别活前缀的DFA与LR(1)分析表 | • (1) S → A | • (2) A → A + A
p196: • 该文法是LR(1)型文法吗? 若不是，应如何解决? (有多种选择) | Exercise 2 | S ACTOION GOTO
p197: Exercise 2 | 0 $ y++$
p198: Exercise 2 | 0 $ y++$ s1
p199: Exercise 2 | 0 $ y++$ s1 | 01 $y ++$
p200: Exercise 2 | 0 $ y++$ s1 | 01 $y ++$ r4(B → y)
p201: Exercise 2 | 0 $ y++$ s1 | 01 $y ++$ r4(B → y)
p202: Exercise 2 | 0 $ y++$ s1 | 01 $y ++$ r4(B → y)
p203: Exercise 2 | 0 $ y++$ s1 | 01 $y ++$ r4(B → y)
p204: Exercise 2 | 0 $ y++$ s1 | 01 $y ++$ r4(B → y)
p205: Exercise 2 | 0 $ y++$ s1 | 01 $y ++$ r4(B → y)
p206: Exercise 2 | 0 $ y++$ s1 | 01 $y ++$ r4(B → y)

## 6.Semantic_Analysis_Intro_SDD_SDT.pdf (129 pages)
p1: 编译原理 | Complier Principles | Lecture 6
p2: Compilation Phases[编译阶段] | Lexical Analyzer | Syntax Analyzer
p3: Content | Definitions (SDD) | attributes
p4: Compilation Phases[编译阶段] | Abstract Syntax Tree(AST) | bool
p5: • Because programs use symbols (a.k.a. identifiers) | ◆ Identifiers require context to figure out the meaning | • Consider the English sentence: “He ate it”
p6: • Semantic of a language is more difficult to describe than syntax | [语义比语法更难描述] | ◆ Syntax: describes the proper form of the programs [仅形式]
p7: • Deeper check into the source program[对程序进一步分析] | ◆ Last stage of the front end[前端最后阶段] | ◆ Compiler’s last chance to reject incorrect programs[最后拒绝机会]
p8: • Attribute grammars[属性文法] | ◆ One-pass compilation |  Semantic analysis is done along with parsing
p9: Content | Definitions (SDD) | attributes
p10: • Syntax Directed Translation[语法制导翻译] | Syntax Directed Translation | Semantic Analysis
p11: • Translate based on the program’s grammar structure[语法结构] | ◆ Syntactic structure: structure of a program given by grammar[文法] | ◆ The parsing process and parse trees are used to direct semantic analysis and
p12: • Attributes can represent anything depending on the task[属性可 | 以表示任意含义] | ◆ If computing expression: a number (value of expression)
p13: Associating semantic rules with grammar rules (productions) | involves two concepts: | • Syntax Directed Definitions (SDD) [语法制导定义]
p14: • Syntax Directed Definitions (SDD) [语法制导定义] | ◆ A syntax-directed definition (SDD) is a context-free grammar(CFG) together | with attributes and rules
p15: • Syntax Directed Translation scheme (SDT) [语法制导翻译方案] | ◆ SDT is a CFG with program fragments embedded in the right part of the | production, and these program fragments are called semantic actions.
p16: • SDD[语法制导定义]: 是CFG的推广，翻译的高层次规则说明 | ◆ A CFG grammar together with attributes and semantic rules | ◆ A subset of them are also called attribute grammars[属性文法]
p17: • Syntax: A -> ⍺ {action1} β {action2} γ … | • Actions are executed “at that point” in the RHS | ◆ action1 executes after ⍺ has been produced but before β
p18: Content | Definitions (SDD) | attributes
p19: • SDD是CFG的增广 | ◆ Grammar symbols together with semantic attributes | ◆ Productions associated with a set of semantic rules to compute the value
p20: • Synthesized attribute[综合属性] | ◆ Defined by a semantic rule associated with the production at N |  The production must have A as its head (i.e., A -> …)
p21: • Synthesized attribute for non-terminal A of parse-tree node N[非终结符 | 的综合属性] | ◆ Only defined by N’s children and N itself
p22: • Inherited attribute for non-terminal A of parse-tree node N[非终结符继 | 承属性] | ◆ Only defined by N’s parent, N’s siblings and N itself
p23: • Attribute dependencies in a production rule[产生式中的属性依赖] | • SDD has rule of the form for each grammar production | ◆ b = f(A.attrs, ⍺.attrs, β.attrs, γ.attrs)
p24: Example: Synthesized attribute | Attribute grammar for simple integer arithmetic expression | Grammar rule Semantic Rules
p25: Attribute grammar for variable | Example: Inherited Attribute | Grammar rule Semantic Rules
p26: The Concepts | • Side effect[副作用] | ◆ 一般属性值计算（基于属性值或常量进行的）之外的功能
p27: Compilation Phases[编译阶段] | Abstract Syntax Tree(AST) | bool
p28: • SDD (Syntax-directed definition) | • CFG + attributes for each symbol + semantic rules for each production | • SDT (Syntax-directed definition)
p29: • Dependence relationship[依赖关系] | ◆ Before evaluating an attribute at a node of a parse tree, we must evaluate all | attributes it depends on
p30: SDD： | Example: Dependency Graph | Productions Semantic rules
p31: • Ordering the evaluation of attributes[计算顺序] | ◆ Dependency graph characterizes possible orders in which we can evaluate the | attributes at the various nodes of a parse-tree[依赖图描述了属性计算顺序]
p32: Example: Evaluation Order | SDD： | Productions Semantic rules
p33: • Before evaluating an attribute at a node of a parse tree, we must | evaluate all attributes it depends on [依赖关系] | ◆ Synthesized: evaluate children first, then the node itself
p34: Content | Definitions (SDD) | attributes
p35: • An SDD is S-attributed if every attribute is synthesized[只具有综合属性] | S-Attributed Definitions[S-属性定义] | Productions Semantic rules
p36: • An SDD is L-attributed (L-SDD) if | ◆ Between the attributes associated with a production body, dependency graph | edges can only go from left to right [依赖图的边只能从左到右]
p37: L-Attributed Definitions (cont.) | Productions Semantic rules | A -> BC A.s = B.b
p38: Content | Definitions (SDD) | attributes
p39: • SDT (executable SDD) can be implemented in two ways | ◆Using a parse tree or AST[基于预先构建的分析树] |  First build a parse tree, and then apply rules or actions at each node while
p40: • Two important classes of SDD’s[两个关键子类] | ◆ SDD is S-attributed, the underlying grammar is LR-parsable | ◆ SDD is L-attributed, the underlying grammar is LL-parsable
p41: • Convert S-attributed SDD to SDT[SDD到SDT的转换] | ◆ Place each action at the end of the production[将每个语义动作都放在产生式的最后] | ◆ SDTs with all actions at the right ends of the production bodies are called Postfix
p42: • If the underlying grammar of S-SDD is LR parsable | ◆ Then the SDT can be implemented during LR parsing | • Implement the converted SDT by reduction[借助归约实现]
p43: • Save synthesized attributes into the stack[栈中额外存放综合属性值] | ◆ Place the attributes along with the grammar symbols (or LR states that | associated with these symbols) in records on stack
p44: • Rewrite the actions to manipulate the parser stack | ◆ The manipulation can be done automatically by the parser | Stack Manipulation[栈操作]
p45: • Rewrite the actions to manipulate the parser stack | ◆ The manipulation can be done automatically by the parser | Productions Semantic rules Semantic Actions
p46: Productions Semantic Actions | (1)L-> E | (2)E-> E1+ T
p47: Input: 3*5+4 | Productions | (1)L-> E n
p48: • We have examined S-SDD -> SDT -> implementation | ◆ S-SDD can be converted to SDT with actions at production ends | ◆ The SDT can be parsed and translated by bottom-up, as long as the
p49: • A -> B {C.inh} C {A.syn} | ◆ C的继承属性: 在C之前 | ◆ A的综合属性: 在RHS末尾
p50: Implement L-SDD | • If the underlying grammar is LL-parsable, then the SDT of L-SDD can | be implemented during LL or LR parsing [若文法是LL可解析的，则可在LL或
p51: • A motivating example: a simple case | • Trick: treating actions as terminals if they do not calculate any attributes. | Eliminating left recursion
p52: • Implementing L-SDD: top-down/bottom-up | • L-SDD -> SDT: | 1. Embed the action that computes the inherited attributes for a nonterminal A
p53: • A more complex case | Eliminating left recursion | E → E1 + T { E.val = E1.val + T.val; }
p54: Eliminating left recursion | R.i = 9T.val= 9 | num.val = 9 T.val= 5 R.i = 4–
p55: • General rules | • Only available for S-SDD (postfix translation schemes), a subset of L-SDD | Eliminating left recursion
p56: • Evaluation order -> DAG -> topological sort -> circle is NOT allowed | • SDD Subsets without circle: S-SDD and L-SDD | • S-SDD: Synthesized attributes only
p57: • Implementing S-SDD: bottom-up | • S-SDD -> SDT: Place each action at the end of the production | • Slack manuscription: enable automation
p58: • Implementing L-SDD: top-down/bottom-up | • L-SDD -> SDT: | 1. Embed the action that computes the inherited attributes for a nonterminal A
p59: • A more complex case | Eliminating left recursion | E → E1 + T { E.val = E1.val + T.val; }
p60: • General rules | • Only available for S-SDD (postfix translation schemes), a subset of L-SDD | Eliminating left recursion
p61: • A recursive-descent parser has a function A for each nonterminal A | [递归预测分析方法] | ◆ Non-terminal expansion implemented by a function call
p62: • Function arguments and return[参数和返回值] | ◆ Inherited: arguments | ◆ Synthesized: return
p63: • Extend the stack to hold actions and certain data items needed | for attribute evaluation[扩展语法分析栈] | ◆ Action-record[动作记录]: represent the actions to be executed
p64: • Table-driven LL-parser | ◆ Mimics a leftmost derivation -> stack expansion | • A-> BC, suppose nonterminal C has an inherited attr C.i
p65: • A-> BC: C.i may depend not only on the inherited attr A.I, but | on all the attrs of B | ◆ Thus, need to process B completely before C.i can be evaluated
p66: (1) T -> F {T’.inh = F.val} T’ {T.val= T’.syn} | (2) T’-> *F {T1’.inh = T’.int x F.val} T1’ {T’.syn = T1’.syn} | (3) T’-> Ɛ {T’.syn = T’.inh }
p67: Example (cont.) | Input: 3*5 | Stack top ‘digit’ matches the input ‘3’
p68: • What we already learnt | ◆ LR > LL, w.r.tparsing power |  We can do bottom-up if we can do top-down
p69: • It is not natural to evaluate inherited attributes | ◆ Example: how to get T’.inh | • Claims: inherited attributes are on the stack
p70: • Given the following SDD, where |⍺| ≠ |β| | ◆ A-> X⍺ {Y .in= X.s}Y | Xβ {Y .in= X.s}Y | ◆ Y-> γ {Y .s= f(Y .in)}
p71: • Given an L-SDD on an LL grammar, we can adapt the grammar to | compute the same SDD during an LR parse | ◆ Put a marker non-terminal[标记非终结符] in the place of each embedded action
p72: (1)T -> F {T’.inh = F.val} T’ {T.val= T’.syn} | (2) T’ -> *F {T1’ .inh = T’.int * F.val} T1’ {T’.syn = T1’ .syn} | (3) T’ -> Ɛ {T’.syn = T’.inh }
p73: Stack Manipulation[栈操作] | (1)T -> F {T’.inh = F.val} T’ {T.val= T’.syn} | (2) T’ -> *F {T1’ .inh = T’.int x F.val} T1’ {T’.syn = T1’ .syn}
p74: Content | Definitions (SDD) | attributes
p75: Content | Definitions (SDD) | attributes
p76: Binding [绑定] | • Binding: matching identifier use with definition[使用-定义] | ◆ Definition: associating an id with a memory location
p77: Scope [作用域] | • Scope: program region where a definition can be bound | ◆Uses of identifier in the scope is bound to that definition
p78: Static Scoping [静态作用域] | • Scopes formed by where definitions are in program text[声明起作用 | 的那段区域]
p79: Dynamic Scoping[动态作用域] | • Scopes formed by when definitions happen during runtime[运行时 | 决定]
p80: Static vs. Dynamic Scoping[对比] | • Most languages that started with dynamic scoping (LISP , Scheme, | Perl) added static scoping afterwards
p81: What is Symbol Table[符号表] | • Symbol: same thing as identifier (used interchangeably) | • Symbol table: a data structure that tracks info about all symbols
p82: Maintaining Symbol Table[维护] | • Basic idea: | int x=0; ... void foo() { int x=0; ... x=x+1; } ... x=x+1 ...
p83: Symbol Table Structure [结构] | • Front-end time is affected by symbol table access time[符号表访问 | 时间影响编译前端性能]
p84: Symbol Table Structure (cont.) | • Array: no space wasted, insert/delete: O(n) , search: O(n) | • Linked list: extra pointer space, insert/delete: O(1), search: O(n)
p85: • S-SDD & LR: Slack manipulation | • L-SDD: Remove Left Recursion | • L-SDD & RDP: Extend RDP Function + Slack manipulation
p86: Symbol Table Revisit | • Binding: matching identifier use with definition[使用-定义] | • Scoping:
p87: Symbol Table Structure (cont.) | • hash(id_name) → index[哈希表] | ◆ A hash function decides mapping from identifier to index
p88: • To handle multiple scopes in a program [处理多个作用域] | ◆ Conceptually, need an individual table for each scope |  In order to be able to enter and exit scopes
p89: Handle Scopes with Stack | • Organize all symbol tables into a scope stack[作用域栈] | ◆An individual symbol table for each scope
p90: Handle Scopes with Stack (cont.) | • Operations: | ◆When entering a scope
p91: Info Stored in Symbol Table | • Entry in symbol table | ◆String: the name of identifier
p92: Attribute List in Symbol Table | • Type info can be arbitrarily complicated | ◆ Type can be an array with multiple dimensions
p93: Use Type Information[类型信息] | • Each variable or function entry contains type info | • Type info is used in later code generation stage[代码生成]
p94: Type and Type Checking | • Type: a set of values and a set of operations on these values | • Type checking: verifying type consistency across program
p95: Static Type Checking[静态类型检查] | • Static type checking at compile time | ◆Infers[推断] whether the program is type consistent through code analysis
p96: Dynamic Type Checking[动态检查] | • Dynamic type checking at execution time | ◆Type consistency by checking types of runtime values
p97: Static vs. Dynamic Typing[静态-动态] | • Static typing: C/C++, Java, … | ◆Variables have static types → hold only one type of value
p98: Static vs. Dynamic Typing (cont.) | • Dynamic Typing: Python, JavaScript, PHP , ... | ◆Variables have dynamic types → can hold multiple types
p99: Type System[类型系统] | • Static/dynamic typing are type systems | ◆Type System: types and type rules of a language
p100: Summary | Definitions (SDD) | attributes
p101: • SDD & SDT | • Synthesized & inherited attribute | • Evaluation order – DAG & topological order
p102: Summary | • Static and Dynamic Scoping | ◆ Pros of static: fewer errors + more efficient
p103: • Dragon Book, 2nd Edition | ◆ Comprehensive Reading: |  Section 5.1-5.3 on introduction to syntax-directed
p104: 编译原理 | Complier Principles | Syntax and Semantic Analysis
p105: • 对于一个无二义性文法G，它的一个句子的最左与最右推导产生的分析树一 | 定是一样的吗? | • 对的，是这样的。语法树会隐去推导顺序
p106: • 找出以下文法中的句型的所有短语，直接短语，句柄 | • 文法: G(E): E → T | E+T; T → F | T*F; F → (E) | a | b | c | • 句型: a * b + c
p107: • 给定一下文法G(S), 请构建该文法的LL(1)分析表 | • S → A | • A → 
p108: • 给定一下文法G(S) , 请构建识别活前缀的DFA与LR(1)分析表 | • S → A | • A → A + A | B + +
p109: • 给定一下文法G(S) , 请构建识别活前缀的DFA与LR(1)分析表 | • (1) S → A | • (2) A → A + A
p110: • 该文法是LR(1)型文法吗? 若不是，应如何解决? (有多种选择) | S ACTOION GOTO | y + $ A B
p111: 0 $ y++$
p112: 0 $ y++$ s1
p113: 0 $ y++$ s1 | 01 $y ++$
p114: 0 $ y++$ s1 | 01 $y ++$ r4(B → y)
p115: 0 $ y++$ s1 | 01 $y ++$ r4(B → y) | 0 $B ++$ 3
p116: 0 $ y++$ s1 | 01 $y ++$ r4(B → y) | 0 $B ++$ 3
p117: 0 $ y++$ s1 | 01 $y ++$ r4(B → y) | 0 $B ++$ 3
p118: 0 $ y++$ s1 | 01 $y ++$ r4(B → y) | 0 $B ++$ 3
p119: 0 $ y++$ s1 | 01 $y ++$ r4(B → y) | 0 $B ++$ 3
p120: 0 $ y++$ s1 | 01 $y ++$ r4(B → y) | 0 $B ++$ 3
p121: 给定文法G(S): | S → Sb | bAa | A → aSc | aSb | a
p122: 给定文法G(S): | S → Sb | bAa | A → aSc | aSb | a
p123: 给定文法G(S): | S → Sb | bAa | A → aSc | aSb | a
p124: 给定文法G(S): | S → Sb | bAa | A → aSc | aSb | a
p125: 给定文法G(S): | S → Sb | bAa | A → aSc | aSb | a
p126: • 判断题 | • 在L-属性定义（L-Attributed Definition）中，每一个属性都是继承属性 | （Inherited Attribute）。
p127: 已知文法 G：S’→ S | • S → (L) | a | • L → L,S | S
p128: 假设我们有一个产生式A→BCD。A、B、C、D这四个非终结符号都有两个属性： | s是一个综合属性，而i是一个继承属性。对于下面的每组规则，请回答：这些 | 规则是否满足S属性定义的要求？这些规则是否满足L属性定义的要求？并给出
p129: 考虑一个非标准的二进制数值系统 ，其中的每个二进制数 b的值（value）被定义为从右至左 | 的非零二进制数字表示的十进制数的交替和。例如，value（ε）= 0，value（10）= 21 = 2， | value（100100）= 22 –25 =–28，value（11110）=21–22 + 23–24 = –10。已知表示非标准二进

## 7.Intermediate_Code_Intro_IR.pdf (73 pages)
p1: 编译原理 | Complier Principles | Lecture 8
p2: Revisit | Definitions (SDD) | attributes
p3: Compilation Phases[编译阶段] | Lexical Analyzer | Syntax Analyzer
p4: Intermediate Code[中间代码生成] | Intermediate Code | Representation
p5: Compilation Phases[编译阶段] | goto L1 | L2:
p6: Multiple IR Levels [不同层级的中间表示] | • IR provides advantages [中间表示的优势] | ◆ Increased abstraction and cleaner separation
p7: Multiple Level IR[不同层级的中间表示] | • Low-level IR are close to assembly [接近汇编] | ◆ E.g., three address code (TAC)[三地址码], static single assignment [静态单赋值]
p8: Multiple Level IR[不同层级的中间表示] | • Possible to have only one IR (AST) — some compilers follows this | ◆ Generate machine code from AST after semantic analysis [AST直接到机器码]
p9: Multiple Level IR[不同层级的中间表示] | • Why multiple IRs? | 2. Easier to add a new front-end (language) or back-end (ISA) [易于扩展]
p10: Intermediate Code[中间代码生成] | Intermediate Code | Representation
p11: Intermediate Representation[中间表示] | • Two Most important IR: | ◆Trees [树形结构], including parse trees and (abstract) syntax trees [语法分析
p12: Three-Address Code[三地址代码] | • At most one operator on the right side of an instruction in three- | address code, e.g., x + y *z translated into t1 = y * z t2 = x + t1
p13: Three-Address Code[三地址代码] | • Example: a * b + a * b is translated to | ◆t1, t2, t3 are temporary variables
p14: Addresses in three-address code[地址] | • An address can be one of the following: | ◆A name[名字]. For convenience, we allow source-program names to appear as
p15: Three-Address Instruction Form[三地址指令形式] | 1. Assignment instructions [二元赋值] | ◆x = y op z, op is a binary arithmetic[双目算术符] or logical operation [逻辑运算符]
p16: Three-Address Instruction Form[三地址指令形式] | 6. Procedure calls [程序调用] | ◆param x for parameters [参数传递];
p17: Three-Address Instruction Form[三地址指令形式] | 8. Indexed copy instructions [带下标的复制指令] | ◆x = y[i] x[i]=y
p18: do { | i = i + 1; | } while(a[i] < v)
p19: Implementation of Three-address Code[实现] | • Three representations. (and more) | ◆quadruples. [四元式]
p20: Quadruples[四元式] | • Quadruples. [四元式] | ◆Examples & some exceptions:
p21: Quadruples[四元式] | • Example: a = b * (-c) + b * (-c) | ◆The special operator minus is used to distinguish the unary minus operator, as in
p22: Triples[三元式] | • A triple has only three fields, which we call op, arg1, arg2. | ◆Quadruple without the result field.
p23: Triples[三元式] | • Example: a = b * (-c) + b * (-c) | ◆The copy statement a=t5 is encoded in the triple representation by placing a in
p24: More About Triples[三元式] | • How can the following statements be expressed in triple? | ◆Array location (e.g. x[i] = y)
p25: Problems About Triples[三元式] | • Problem with triples | ◆In code optimization, instructions are often moved around.
p26: Problems About Triples[三元式] | • Problem with triples | ◆In code optimization, instructions are often moved around.
p27: Three-Address Code[三地址代码] (Recap) | • Generic form is X = Y op Z [最多3个操作数] | • Three representations. (and more)
p28: Indirect Triples[间接三元式] | • The problem does not occur with indirect triples. | • Indirect triples consist of a listing of pointers to triples, rather than a
p29: Indirect Triples[间接三元式] | • After CSE, empty entries in database can be reused | ◆Code in triple database becomes non-contiguous over time
p30: Indirect Triples[间接三元式] | • Another Example: x = (a+b)*c; y = d/(a+b) | • With indirect triples, an optimizing complier can move an instruction by reordering
p31: Single Static Assignment[静态单赋值] | • Every variable is assigned exactly once statically[仅一次] | ◆Give variable a different version name on every assignment
p32: Benefits of SSA | • SSA is an IR that facilitates code optimization | ◆SSA tells you when an optimization should not happen
p33: Benefits of SSA (cont.) | • SSA is an IR that facilitates code optimizations | ◆ SSA tells you when an optimization should happen
p34: Syntax Directed Translation[语法制导翻译] | • Syntax directed translation can be used again for code generation [代码生成] | ◆ Code generation is dependent on syntax/AST
p35: Intermediate Code[中间代码生成] | Code Generation | Variable
p36: Code Generation Overview[代码生成] | • Program code is a collection of functions | ◆By now, all functions are listed in symbol table
p37: Processing Variable Definitions[变量定义] | • To lay out a variable, both location and width are needed | ◆ Location: where variable is located in memory
p38: Variable Location from Offset | • Naive method: reserve a big memory section for all data | ◆ Size data section to be large enough to contain all variables
p39: void foo() { | int a; | int b;
p40: More about Storage Layout | • Allocation alignment[对齐] | ◆ Enforce addr(x) % sizeof(x.type) == 0
p41: Code Generation[代码生成] | • We will use the syntax-directed formalisms to specify translation | ◆ Variable definitions[变量定义] -> Recall semantic analysis & symbol table
p42: Intermediate Code[中间代码生成] | Code Generation | Variable
p43: Code Generation[代码生成] | • SSA (Single Static Assignment) | • We will use the syntax-directed formalisms to specify translation
p44: CodeGen: Assignment Statement | • Translate into three-address code[赋值语句] | ◆An expression with more than one operator will be translated into
p45: SDT Translation of Assignment | • Attributes code and addr | ◆ S.code and E.code denote the TAC for S and E, respectively
p46: Incremental Translation[增量翻译] | • Generate only the new three-address instructions | ◆ gen() not only constructs a three-address inst, it appends the inst to the sequence
p47: Code Generation[代码生成] | • We will use the syntax-directed formalisms to specify translation | ◆ Variable definitions[变量定义] -> Recall semantic analysis & symbol table
p48: CodeGen: Array Reference[数组引用] | • Primary problem in generating code for array references is to | determine the address of element
p49: N-dimensional Array | • Laying out 2D array in 1D memory | int A[N1][N2]; /* int A[0..N1][0..N2] */
p50: Translation of Array References | • Type(a) = array(10, int) | ◆c = a[i];
p51: Translation of Array References (cont.) | • A[i1][i2][i3], type(a) = array(3, array(5, array(8, int))) | ◆ L.array: a pointer to the symbol-table entry for the array name
p52: Translation of Array References (cont.) | • A[i1][i2][i3], type(a) = array(3, array(5, array(8, int))) | ① S -> id = E; | L = E; { gen(L.array.base‘[’L.addr‘]’ ‘=’ E.addr); }
p53: Code Generation[代码生成] | • We will use the syntax-directed formalisms to specify translation | ◆ Variable definitions[变量定义] -> Recall semantic analysis & symbol table
p54: CodeGen: Boolean Expressions | • Boolean expression: a op b | ◆ where op can be <, <=, !=, >, >=, &&, ||, ==, …
p55: Boolean Expressions | • Computed just like any other arithmetic expression | • Then, used in control-flow statements
p56: Boolean Expressions | • Implemented via a series of jumps[利用跳转] | ◆ converted to two gotos (true and false)
p57: Boolean Expressions | • Boolean expressions are composed of | ◆Boolean operators (==, &&, ||) applied to elements that are
p58: SDT Translation of Booleans[布尔表达式] | • B -> B1 || B2 | ◆ B1.true is same as B.true, B2 must be evaluated if B1 is false[B1假才评估B2]
p59: Intermediate Code[中间代码生成] | BackPatching | Code Generation
p60: Code Generation[代码生成] | • We will use the syntax-directed formalisms to specify translation | ◆ Variable definitions[变量定义] -> Recall semantic analysis & symbol table
p61: CodeGen: Control Statement[控制语句] | • Inherited attributes[继承属性] | ◆B.true: the label to which control flows if B is true (依赖于S1)
p62: Translation of Controls | • Helper functions[辅助函数] | ◆newlabel(): creates a new label
p63: Translation of Controls (cont.) | ① S -> if ( B ) S1 | ② S -> if ( B ) S1 else S2
p64: Jumping Labels[跳转标签] | • Key of generating code for Boolean and flow-control: matching a | jump inst with the target of jump[跳转指令匹配到跳转目标]
p65: Handle Jumping Labels | • Idea: generate code using dummy labels first, then patch them with addresses | later after labels are generated
p66: One-Pass Code Generation[单遍生成] | • One Pass Generation takes less time along with LR parser | • However, given the example below, we need to know the address
p67: Backpatching[回填] | • Synthesized attributes[综合属性]. S -> if (B) S1 | ◆ B.truelist: a list of jump or conditional jump insts into which we must insert the
p68: Backpatching of Control-Flow | • Slightly modify the grammar | ① S -> if (B) M S1 { backpatch(B.truelist, M.inst)
p69: Backpatching of Control-Flow | • makelist(i): creates a new list | out of statement index i
p70: Backpatching of Control-Flow | • makelist(i): creates a new list | out of statement index i
p71: Intermediate Code[中间代码生成] | BackPatching | Intermediate Code
p72: Summary | • Three-Address Code: X = Y op Z | ◆ Three representations
p73: Further Reading | • Dragon Book, 2nd Edition | ◆ Comprehensive Reading:

## 8.Code_Optimization.pdf (50 pages)
p1: 编译原理 | Complier Principles | Lecture 9
p2: Compilation Phases[编译阶段] | Lexical Analyzer | Syntax Analyzer
p3: Compilation Phases[编译阶段] | goto L1 | L2:
p4: Optimization[代码优化] | Front End Optimization Back End | Control-Flow
p5: To Optimize: Who When Where? | • Manual: source code[人工, 源码] | ◆Select appropriate algorithms and data structures
p6: Overview of Optimizations | • Better one or more of the following (in the average case) | ◆Execution time.
p7: Code Optimization[代码优化] | Layout-related | transformations
p8: Code Optimization[代码优化] | Layout-related | transformations
p9: Types of Optimizations | • Compiler optimization is essentially a transformation[转换], | including deleting/adding/moving/modifying.
p10: Layout-Related: Code | • For example, given two ways to layout code: | ◆Which code layout is better?, assuming:
p11: Layout-Related : Data | • Example 1: Change the variable declaration order | struct S {
p12: Layout-Related : Data | • Example 2: Change AOS (array of structs) to SOA (struct of arrays) | struct S {
p13: IR Optimization Revisit | • Goal of Optimization: | ◆ Execution time / Memory usage / Energy consumption / Binary executable size...
p14: Code Optimization[代码优化] | Layout-related | transformations
p15: Code-Related Optimizations | • Modifying (e.g., strength reduction) | ◆A = 2 * a; → A = a << 1;
p16: Control-Flow Analysis | • For many imperative programming languages[命令式编程], the | control flow of a program is explicit in a program's source code.
p17: Basic Block | • A basic block[基本块] is a straight-line code sequence that | • Except the first instruction, there are no other labels[只有第一条进入]
p18: Control Flow Graph[控制流图] | • A control flow graph is a directed graph in which: | ◆ Each node represents a basic block, i.e., a straight-line piece of code
p19: L1: | a := c * 2; | w := a + b;
p20: Construct CFG | • Step 1: partition code into basic blocks[分解为基本块] | ◆ Identify the leaders instructions. An instruction is a leader if any of the
p21: Construct CFG | • Step 2 : add an edge between basic blocks B1 and | B2 if[连接基本块]
p22: 0: t0 = read_num | 1: if t0 mod 2 == 0 | 2: print t0 + " is even."
p23: Local and Global Optimizations | • Local optimizations[局部] | ◆ Optimizations performed exclusively within a basic block.
p24: Code Optimization[代码优化] | Layout-related | transformations
p25: Example: Local Optimizations | • Common subexpression elimination (CSE)[删除公共子表达式] | ◆ Two operations are common if they produce the same.
p26: DAG of Basic Blocks | • The Directed Acyclic Graph (DAG) is used to represent the | structure of a basic block
p27: Algorithm: Construction of DAG | • Create a node for each initial value of the variables appearing in | the basic block[为变量初始值创建节点 --- 叶子节点]
p28: (1) a = b + c | (2) b = a – d | (3) c = b + c
p29: Local Opt.: Elimination | • If b is not live on exit from the block | ◆ No need to keep b = a – d
p30: Local Opt.: Elimination | • When finding common subexpressions, we | really are finding expressions that are
p31: Using Algebraic Identities | • Eliminate computations by applying mathematical rules[使用数学规则] | Identities: a * 1 ≡ a, a * 0 ≡ 0, b & true ≡ b
p32: Local Opt.: Constant Folding | • Constant Folding[常量折叠] | ◆ Computing operations on constants at compile time
p33: Local Opt.: Constant Propagation | • Constant Propagation[常量传播] | ◆ Substituting values of known constants at compile time
p34: Code Optimization[代码优化] | Layout-related | transformations
p35: Global Optimizations | • Extend optimizations to flow of control, i.e., CFG | ◆ Along all paths.
p36: Global Optimizations | X = 3; | if(B>0)
p37: Global Opt.: Conservative | • Compiler must prove some property X at a particular point | ◆ Need to prove at that point property X holds along all paths.
p38: Global Opt.: Data Flow | • Most optimizations rely on a property at given point, called values | ◆ For Global Constant Propagation (GCP):
p39: Global Constant Propagation | • Let’s apply dataflow analysis to compute values for: | ◆ Emulates what human does when tracing through code
p40: • In this example, constants can be propagated to X+1, 2*X | • Statements visited in reverse post-order (predecessor first) | X = 2
p41: • Once constants have been globally propagated, we would like to | eliminate the dead code | X = 2
p42: IR Optimization of LLVM | Source url: https://www.slideserve.com/quinlan-dominguez/llvm-pass-and-code-instrumentation 41
p43: LLVM Passes | • Optimizations are implemented as Passes that traverse some portion of | a program to either collect information or transform the program
p44: General Optimization Flags | • O0: no optimization | ◆ Compiles the fastest and generates the most debuggable code
p45: Performance at Varying Flags | • Compare the performance of the benchmark when compiled | with either GCC or LLVM
p46: Summary | • Layout-related transformations[布局相关] | ◆ Goal: maximize the spatial locality [空间局部性].
p47: Further Reading | • Dragon Book, 2nd Edition | ◆ Comprehensive Reading:
p48: DAG Construction Revisit | • Three possible scenarios | 1. x = y op z
p49: • x = A + B | • y = x + 3 | • z = x * y
p50: DAG-based Optimization | • If z and b are alive | A B

## 9.Target_Code_Generation.pdf (50 pages)
p1: 编译原理Complier Principles | Lecture 9Target Code Generation赵帅计算机学院中山大学
p2: Compilation Phases[编译阶段]Lexical AnalyzerSyntax AnalyzerSemantic AnalyzerIntermediateCode Generation | token streamsyntax tree | Character Stream(Source Code)
p3: Target Code Generation[⽬标代码⽣成]•Target code generationuTransform the syntactically analyzed or optimized intermediate code into target code.•The main issues we need to consider:uHow to make the target code shorter?uHow to make full use of the registers and r...
p4: Primary Tasks [主要任务]•What we have now ?uIR of the source programuSymbol table•Three primary tasks:uInstruction selection[指令选取]pChoose appropriate target-machine instructions to implement the IR statementsuRegister allocation and assignment[寄存器分配]pdecide wha...
p5: Instruction Selection[指令选取]•Instruction selection is the stage of a compiler backend that transforms intermediate representation (IR) into a low-level IR.•contains both instruction scheduling and register allocation.•Its output IR may still be subject to pe...
p6: •Register allocation: the process of assigning local variables and expression results to processor registers[寄存器分配].uRegisters are the fastest storage unit but are of limited numberspValues not held in registers need to reside in memorypInstructions involvi...
p7: Stack Machine [栈式计算机]•A simple evaluation model:uNo variables or registersuA stack of values for intermediate results•Each instruction:uPush operands to the stack[讲操作数压⼊栈中]uTakes its operands from the top of the stack[栈顶取操作数]uRemoves those operands from the...
p8: Optimize the Stack Machine•Note that the add instruction does 3 memory operations•two reads and one write. •The top of the stack is frequently accessed.•Idea: keep the top of the stack in a register (called accumulator) [使⽤寄存器]•The “add” instruction is nowu...
p9: 3+7+5:
p10: From Stack Machine to MIPS•The compiler generates code for a stack machine with accumulator.•We want to run the resulting code on the MIPS processor•We simulate stack machine instructions using MIPS instructions and registers
p11: Simulating a Stack Machine•The ACCis kept in MIPS register $t0•The stackis kept in memory•The address of the next location on the stack is kept in MIPS register $spuThe top of the stack is at address $sp + 4 | •The stack grows towards lower addressesuStanda...
p12: MIPS Architecture•Prototypical Reduced Instruction Set Computer (RISC) architecture•Arithmetic operations use registers for operands and results•Must use load and store instructions to use operands and results in memoryuAll other instructions access only re...
p13: A Sample of MIPS Instructions•lw reg1 offset(reg2)uLoad 32-bit word from address reg2 + offset into reg1•add reg1 reg2 reg3ureg1 ← reg2 + reg3•sw reg1 offset(reg2)uStore 32-bit word in reg1 at address reg2 + offset•addiu reg1 reg2 immureg1 ← reg2 + immu“u” ...
p14: Code Generation Consideration•We used to store values in unlimited temporary variables, but registers are limited --> must reuse registers[重复使⽤寄存器] | •Must save/restore registers when reusing them[保存-恢复]ue.g.,suppose that we need tostore resultsof expressio...
p15: Code Generation Consideration(cont.)•Registers are saved on and restored from the stack•Note: $sp - stack pointer register, pointing to the top of stack uSaving a register $t0 on the stack:psw $t0, 0($sp) // store word in $t0 on the top of stackpaddiu $sp, ...
p16: • To push elements onto the stackuTo move stack pointer $sp down to make room for the new datauStore the elements into the stack•For example, to push registers $t1 and $t2 onto stack•add $sp, $sp, -8 •sw $t1, 4($sp) •sw $t2, 0($sp) | Stack Operations[栈操作]
p17: MIPS Assembly Example.•The stack-machine code for 7 + 5 in MIPS:acc ← 7push accacc ← 5acc ← acc + stack_toppop | li $t0 7 // store 7 in $t0 sw $t0 0($sp) // store $t0 in the stackaddiu $sp $sp -4 // decrement sp to make space for the valueli $t0 5 // store ...
p18: •Pop elements simply by adjusting the $sp upwardsuNote that the popped data is still present in memory, but data past the stack pointer is considered invalid | Stack Operations (cont.) | word 1word 2$sp word 1word 2$t1$t2$sp
p19: •For each expression e, we generate MIPS code that: uComputes the value of e into $t0uPreserves $sp and the contents of the stack•We define a code generation function cgen(e)uIts result is the code generated for e | Code Generation Strategy | cgen(e1 + e2):...
p20: •We need flow control instructions •New instruction: beq reg1 reg2 labeluBranch to label if reg1 ==reg2•New instruction: b labeluUnconditional jump to label | Code Generation for the Conditional | cgen(if e1 == e2 then e3 else e4):cgen(e1) # pushes $t0 on s...
p21: •Codeuthe size of the generated target code is fixed at compile time •Global/static uthe size of some program data objects, e.g., global constants, are known at compile time •Stack ustore dynamic data structures •Heap umanage long-lived data | Example Memor...
p22: •Compiler typically allocates memory in the unit of procedure.•Each execution of a procedure is called as its activation[活动].ustarts at the beginning of the procedure body uWhen completed, returns the control to the point immediately after the place where t...
p23: •Manage ARs like a stack in memory[AR栈管理] uOn function entry: AR instance allocated at top of stack uOn function return: AR instance removed from top of stack• Hardware support uStack pointer ($SP) register[栈指针] p$SP stores address of top of the stack pAllo...
p24: •Example layout of a function AR | •Registers such as $FP and $IP overwritten by callee → Must be saved to/restored from AR on call/returnuCaller’s $IP: where to execute next on function return (a.k.a. return address: instruction following function call)uCa...
p25: •Important registers should be saved across function callsuOtherwise, values might be overwritten• But, who should take the responsibility?uThe caller knows which registers are important to it and should be saveduThe callee knows exactly which registers it ...
p26: •Potential solutionsuSolution 1: caller to save any important registers that it needs before calling a func, and to restore them after (but not all will be overwritten)uSolution 2: callee saves and restores any registers it might overwrite (but not all are ...
p27: •Caller: save and restore any of the following caller-saved registers that it caresu$t0-$t9, $a0-$a3, $v0-$v1 uThe callee can modify these registers, assuming that the caller already saved them•Callee: save and restore any of the following callee-saved regi...
p28: •The caller sets up for the call via these steps[调⽤者]u Make space on stack for and save any caller-saved registersu Pass arguments by pushing them on the stack, one by one, right to leftu Jump to the function (saves the next inst in $ra)•The callee thentake...
p29: •When ready to exit, the callee does thefollowing[调⽤退出]u Assign the return value (if any) to $v0u Pop stack frame off the stack (locals/temps/saved regs)u Restore the value of $fp and $rau Jump to the address saved in $ra•When control returns to the caller,...
p30: •The calling sequence is instructions (of both caller and callee) to set up a function invocation.•New instruction: jal label.uJump to label, after saving address of next instruction in $ra. | •New instruction: jr reguJump to address in register reg | Code ...
p31: •The “variables” of a function are just its ‘parameters’uThey are all in the ARuPushed by the caller•Problem: the stack grows when intermediate results are saved, so the variables are not at a fixed offset from $spuThus, access to locations in the stack fra...
p32: •Local variables are referenced from an offset from $fp u $fp is pointing to old $ip (return address) •For a function def f(x,y) = e, the activation and frame pointer are set up as follows:u The parameters are pushed right to left by the calleru The locals ...
p33: double fun1(int p1, double p2, int p3) { int i, j;res = fun2(p1*p2, j); return res; } | double fun2(double ar, int ib) { int i, r1; double res; … return res; } | p3p2p1Old FPOld IPijibarOld FPOld IPir1res
p34: •Objects are like structures in Cu Objects are laid out in contiguous memoryu Each member variable is stored at a fixed offset in object | •Unlike structures, objects have member methods | Code Generation for OO
p35: •Two types of member methods:uNonvirtual member methods: cannot be overriddenpParent obj = new Child();pobj.nonvirtual(); // Parent::nonvirtual() calledpMethod called depends on (static) reference typepCompiler can decide call targets staticallyuVirtual mem...
p36: •Dispatch: to send to a particular place for a purposeui.e., to jump to a (particular) function •Static Dispatch: selects call target at compile time uNonvirtual methods implemented using static dispatch uImplication for code generation -- Can hard code fun...
p37: •Class tag is used for dynamic type checking •Dispatch ptr is a pointer to the dispatch table •Compiler translates member accesses to offset accesses if(...) obj = new Parent(); else obj = new Child(); obj.x = 10; // move 10, x_offset(obj) obj.f2(); // call...
p38: •Invariant: the offset of a member variable or member method is the same in a class and all of its subclassesInheritance and Subclasses | class A1 { int x; virtual void f1() { ... } virtual void f2() { ... } } class A2 inherits A1 { int y; virtual void f2()...
p39: •Member variable accessuGenerate code using offset for reference type (class)uObject may be a child type, but will still have same offset •Member method call uGenerate code to load call target from dispatch table using offset for reference type uAgain, obje...
p40: Machine Optimizations[机器相关优化]•After performing IR optimizationsuWe need to convert the optimized IR into the target language (e.g., assembly, machine code)•Specific machine features are taken into account to produce code optimized for the particular archite...
p41: Instruction Selection[指令选取]•To find an efficient mapping from the IR to a target-specific assembly listing[IR到汇编的映射]•Instruction selection is particularly important when targeting architectures with CISC (e.g., x86)uIn these architectures, there are typical...
p42: Instruction Cost[指令成本]• Instruction cost = 1 + cost (source-mode) + cost (destination-mode) | • Examples
p43: Instruction Cost (cont.)• Suppose we translate TAC x:=y+z toMOV y, R0ADD z, R0MOV R0, x• a := b + c | • a := a + 1 | MOV b, R0ADD c, R0MOV R0, aMOV b, aADD c, aMOV *R1, *R0ADD *R2, *R0
p44: Instruction Scheduling[指令调度]• Some factsuInstructions take clock cycles to execute (latency)uModern machines issue several operations per cycle (Out-of-Order Execution)uExecution time is order-dependent• Goal: reorder the operations to minimize execution ti...
p45: Register Allocation[寄存器分配]•In TAC, there are an unlimited number of variablesu On a physical machine there are a small number of registers•Register allocation is the process of assigning variables to registers and managing data transfer in and out of regist...
p46: Register Allocation (cont.)•Goals of register allocationuKeep frequently accessed variables in registersuKeep variables in registers only as long as they are live •Local register allocation[局部]uAllocate registers basic block by basic blockuMakes decisions o...
p47: Graph Coloring[图着⾊]• Register interference graph (RIG)[相交图]uEach node represents a variableuAn edge between two nodes V1 and V2 represents an interference in live ranges[活跃期/⽣存期]• Based on RIGuTwo variables can be allocated in the same register if there is ...
p48: Register Spilling[寄存器溢出]• Determining whether a graph is k-colorable is NP-completeuTherefore, problem of k-register allocation is NP-completeuIn practice: use heuristic polynomial algorithm that gives sub-optimal allocations in most of the timeuChaitin’s g...
p49: Peephole Optimization[窥孔优化]•Optimization waysuUsual: produce good code through careful instruction selection and register allocationuAlternative: generate naive target code and then improve•A simple but effective technique for locally improving the target c...
p50: Summary•Code can be optimized at different levels with various techniquesuPeephole, local, loop, globaluIR: local, global, CSE, constant folding and propagation, …uTarget: instruction, register, …•Interactions between the various optimization techniquesuSom...
