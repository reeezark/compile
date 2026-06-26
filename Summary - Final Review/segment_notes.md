# Segment notes for compiler final review

## Segment map

- L0: `0.Introduction.pdf`, pages 1-34. Course intro and compiler pipeline.
- L1: `1.Lexical Analysis_Intro_RE.pdf`, pages 1-43. Lexical analysis, tokens, languages, regular expressions.
- L2: `2.Lexical Analysis_NFA_DFA.pdf`, pages 1-80. FA, NFA/DFA, subset construction, minimization, table-driven scanner.
- L3: `3.Syntax Analysis_Intro_Parser_CFG.pdf`, pages 1-55. CFG, derivation, parse tree, ambiguity, Chomsky hierarchy, AST.
- L4: `4.Syntax_Analysis_Top_Down.pdf`, pages 1-89. Top-down parsing, FIRST/FOLLOW, LL(1), predictive parsing.
- L5: `5.Syntax_Analysis_Bottom_Up.pdf`, pages 1-206. Shift-reduce, LR(0), SLR(1), LR(1), LALR(1), conflicts.
- L6: `6.Semantic_Analysis_Intro_SDD_SDT.pdf`, pages 1-129. Semantic analysis, SDD/SDT, attributes, symbol table, type checking.
- L7: `7.Intermediate_Code_Intro_IR.pdf`, pages 1-73. IR, TAC, SSA, storage layout, translation, backpatching.
- L8: `8.Code_Optimization.pdf`, pages 1-50. Basic blocks, CFG, DAG, local/global optimization, dataflow.
- L9: `9.Target_Code_Generation.pdf`, pages 1-50. Backend tasks, MIPS-style target generation, activation records, register allocation.

## L0 - Introduction

- Main exam points: compilation vs interpretation vs JIT; compiler frontend/middle/backend phases; role of lexical, syntax, semantic analysis, IR generation, optimization, target generation. Sources: L0 p12-p33.
- Core formulas: none. Important pipeline: character stream -> token stream -> syntax tree/AST -> annotated tree/symbol table -> IR -> optimized IR -> target code. Sources: L0 p19-p33.
- Key concepts: compilation, interpretation, Just-In-Time Compiler (JIT), Lexical Analysis, Syntax Analysis, Semantic Analysis, Intermediate Representation (IR), Code Optimization, Target Code Generation.
- Examples/patterns: C `Hello World` compilation phases: preprocessing, compiling, assembly, linking. Sources: L0 p16-p17.
- Pitfalls: do not confuse parser input with source characters; parser input is token stream. Sources: L0 p20-p24.

## L1 - Lexical analysis and regular expressions

- Main exam points: lexeme/token/token class distinction; lexical analyzer task; alphabet, string, language; language operators union, concatenation, Kleene closure; regular expression construction, precedence, shorthand; longest match and keyword priority. Sources: L1 p4-p39.
- Core formulas: token = (class, lexeme); `A+ = AA*`; `A? = A | epsilon`; `[a1...an] = a1 | ... | an`; identifier pattern `letter(letter|digit)*`. Sources: L1 p8, p22-p33, p35-p36.
- Key concepts: Lexical Analysis/Scanner, token, lexeme, alphabet, string, language, Regular Expression (RE), union, concatenation, Kleene closure.
- Examples/patterns: tokenize `if i == 0` as `<keyword,'if'>, <id,'i'>, <op,'=='>, <num,'0'>`. Sources: L1 p39.
- Pitfalls: regex ambiguity is resolved by language rules, usually longest match first and then priority such as keyword over identifier. Sources: L1 p14-p15, p35-p36.

## L2 - NFA, DFA, and scanner implementation

- Main exam points: FA is implementation of RE specification; DFA vs NFA; formal components; Thompson construction; subset construction with epsilon-closure and move; DFA minimization by partition refinement; table-driven lexical analyzer; regular language limits. Sources: L2 p3-p68.
- Core formulas: FA components `(Sigma, S, n, F, delta)`; subset construction uses `epsilon-closure(move(I, x))`; DFA execution is `O(|X|)`. Sources: L2 p4-p12, p22-p31, p42.
- Key concepts: Finite Automata (FA), Deterministic Finite Automata (DFA), Non-deterministic Finite Automata (NFA), epsilon-closure, subset construction, DFA minimization, transition table, Lex.
- Examples/patterns: convert `(a|b)*abb` to NFA, then DFA; combine token NFAs with a new start state and epsilon transitions; choose longest accepted prefix. Sources: L2 p14-p18, p52-p59, p72-p80.
- Pitfalls: NFA accepts if at least one path reaches final state; DFA has exactly one transition per state/input and no epsilon moves. Regular languages cannot count unbounded matching like `a^n b a^n`. Sources: L2 p8-p11, p63-p65.

## L3 - CFG and parser basics

- Main exam points: syntax analysis input/output; CFG definition; terminal/nonterminal/start/productions; derivation, sentential form, sentence, language; leftmost/rightmost derivation; parse tree vs AST; ambiguity and removal; Chomsky grammar hierarchy. Sources: L3 p6-p55.
- Core formulas: CFG `G=(V_T,V_N,S,delta)`; type-2 production form `A -> alpha`; type-3 production form `A -> aB | a`. Sources: L3 p14-p20, p43-p49.
- Key concepts: Syntax Analysis/Parser, Context-Free Grammar (CFG), derivation, sentential form, sentence, parse tree, ambiguity, Abstract Syntax Tree (AST), Chomsky hierarchy.
- Examples/patterns: expression grammar and parse tree for arithmetic expressions; ambiguity from `E -> i | E+E | E*E | (E)`. Sources: L3 p30-p40, p52.
- Pitfalls: ambiguity of arbitrary CFG is undecidable; parser-friendly grammar often encodes precedence/associativity. Sources: L3 p36-p40.

## L4 - Top-down parsing and LL(1)

- Main exam points: recursive-descent parsing, backtracking, left recursion removal, left factoring, FIRST/FOLLOW computation, LL(1) conditions, predictive parse table construction, non-recursive LL parser algorithm. Sources: L4 p5-p89.
- Core formulas: immediate left recursion `A -> A alpha | beta` becomes `A -> beta A'`, `A' -> alpha A' | epsilon`; LL(1) alternatives need disjoint FIRST sets and FOLLOW checks for epsilon; parse table `M[A,a]`. Sources: L4 p13-p22, p30-p52, p78-p83.
- Key concepts: Top-Down Parsing, Recursive-Descent Parsing (RDP), backtracking, left recursion, left factoring, FIRST, FOLLOW, LL(1), predictive parsing table.
- Examples/patterns: expression grammar `E -> T E'`, `E' -> + T E' | epsilon`, `T -> F T'`, `T' -> * F T' | epsilon`, `F -> (E) | id`; parse `id + id * id` using stack/table. Sources: L4 p35-p50, p56-p81.
- Pitfalls: left recursion causes top-down nontermination; common prefixes prevent choosing alternatives from one lookahead; LL(1) table entries with multiple productions indicate conflict. Sources: L4 p13-p29, p82-p83.

## L5 - Bottom-up parsing and LR family

- Main exam points: shift-reduce parsing actions; handle, phrase, simple phrase, viable prefix; LR parser stack and ACTION/GOTO; LR(0) items, closure, goto, augmented grammar, canonical item collection; conflict types; SLR(1), LR(1), LALR(1), parser power hierarchy. Sources: L5 p4-p139.
- Core formulas: augmented grammar `S' -> S`; LR(0) item `A -> alpha . beta`; closure adds `B -> . gamma` for `A -> alpha . B beta`; LR(1) item `[A -> alpha . beta, a]`; LR(1) closure adds `[B -> . gamma, b]` for `b in FIRST(beta a)`. Sources: L5 p64-p82, p98-p122.
- Key concepts: Bottom-Up Parsing, Shift-Reduce Parsing, handle, viable prefix, LR(k), ACTION table, GOTO table, LR(0), SLR(1), LR(1), LALR(1), shift-reduce conflict, reduce-reduce conflict.
- Examples/patterns: construct LR(0) automaton/table for `S -> BB`, `B -> aB | b`; use FOLLOW to limit SLR reductions; merge LR(1) states with same core for LALR. Sources: L5 p69-p80, p91-p104, p124-p137.
- Pitfalls: LR(0) reduces immediately on completed items, causing many conflicts; SLR uses coarse FOLLOW sets; LALR merging can introduce reduce-reduce conflicts but not shift-reduce conflicts. Sources: L5 p81-p95, p108-p137.

## L6 - Semantic analysis, SDD, SDT

- Main exam points: semantic analysis purpose; SDD vs SDT; synthesized/inherited attributes; dependency graph and topological evaluation; S-attributed and L-attributed definitions; S-SDD with LR reductions; L-SDD with LL/RDP or marker nonterminals; binding, scope, symbol table, type checking. Sources: L6 p5-p103.
- Core formulas: SDD = CFG + attributes + semantic rules; SDT = CFG + embedded semantic actions; inherited attribute in production body may depend on head inherited attributes and left siblings for L-attributed definitions. Sources: L6 p13-p17, p19-p37, p41-p73.
- Key concepts: Semantic Analysis, Syntax-Directed Definition (SDD), Syntax-Directed Translation (SDT), Attribute Grammar, synthesized attribute, inherited attribute, dependency graph, S-attributed, L-attributed, binding, scope, symbol table, static/dynamic typing.
- Examples/patterns: arithmetic expression value as synthesized attribute; inherited attribute for variable declarations; stack manipulation for S-SDD in bottom-up parsing; RDP function arguments for inherited attributes and returns for synthesized attributes. Sources: L6 p24-p25, p41-p67.
- Pitfalls: attribute dependency cycles are illegal; not every L-attributed definition is S-attributed; dynamic scoping differs from dynamic typing. Sources: L6 p29-p37, p56-p71, p76-p99.

## L7 - Intermediate representation and code generation

- Main exam points: why multiple IR levels; TAC forms and representations; quadruples/triples/indirect triples; SSA; variable layout and alignment; array address calculation; TAC translation for assignment, boolean expressions, control statements; labels and backpatching. Sources: L7 p4-p73.
- Core formulas: TAC has at most one operator on RHS; generic `x = y op z`; row-major array offset uses dimension sizes and element width; boolean control emits conditional and unconditional gotos; backpatching uses `truelist`, `falselist`, `nextlist`, `makelist`, `merge`, `backpatch`. Sources: L7 p12-p31, p37-p52, p54-p70.
- Key concepts: Intermediate Representation (IR), Three-Address Code (TAC), quadruple, triple, indirect triple, Single Static Assignment (SSA), storage layout, alignment, backpatching.
- Examples/patterns: translate `a*b+a*b` into temporaries; represent `a=b*(-c)+b*(-c)` in quadruples/triples; translate arrays and `if/while` using labels/lists. Sources: L7 p13, p20-p30, p48-p70.
- Pitfalls: triples are fragile under code motion; indirect triples solve movement by reordering pointers; one-pass code generation needs backpatching when targets are unknown. Sources: L7 p25-p30, p64-p70.

## L8 - Code optimization

- Main exam points: optimization goals and transformation types; code/data layout; basic block and CFG construction; local vs global optimization; DAG for basic blocks; CSE, algebraic identities, constant folding/propagation, dead code elimination; conservative global dataflow reasoning; LLVM pass idea and optimization levels. Sources: L8 p4-p50.
- Core formulas: leader rules for basic block partition; CFG edges from jumps/fall-through; dataflow properties must hold along all paths for conservative global optimization. Sources: L8 p16-p23, p35-p41.
- Key concepts: Code Optimization, Basic Block, Control Flow Graph (CFG), Common Subexpression Elimination (CSE), DAG, Constant Folding, Constant Propagation, Dead Code Elimination, Dataflow Analysis, LLVM Pass.
- Examples/patterns: construct CFG from TAC; build DAG for a basic block; remove redundant expression nodes, apply algebraic simplification, fold constants, then eliminate dead assignments if not live on exit. Sources: L8 p19-p33, p48-p50.
- Pitfalls: local optimization only sees one block; global optimization must be conservative; layout transformations target locality, not semantic changes. Sources: L8 p10-p13, p23, p35-p41.

## L9 - Target code generation

- Main exam points: instruction selection, register allocation/assignment, instruction scheduling; stack-machine model and MIPS simulation; expression and conditional code generation; runtime memory areas; activation records and calling sequence; caller/callee saved registers; frame pointer; OO dispatch; machine optimizations, graph coloring and spilling, peephole optimization. Sources: L9 p3-p50.
- Core formulas: instruction cost = `1 + cost(source-mode) + cost(destination-mode)`; register allocation model uses register interference graph coloring; k-register allocation is NP-complete, so compilers use heuristics and spilling. Sources: L9 p42-p48.
- Key concepts: Target Code Generation, Instruction Selection, Register Allocation, Instruction Scheduling, Stack Machine, MIPS, Activation Record (AR), calling convention, caller-saved/callee-saved registers, Frame Pointer (FP), Dispatch Table, Register Interference Graph (RIG), spilling, peephole optimization.
- Examples/patterns: generate stack-machine/MIPS code for `7+5`; use `jal`/`jr` in function calls; access locals by offset from `$fp`; use dispatch table for virtual method call; allocate registers from live ranges. Sources: L9 p7-p20, p21-p39, p40-p50.
- Pitfalls: values not in registers require memory traffic; `$sp` moves during evaluation so stable local access uses `$fp`; LALR-style frontend concerns are separate from backend target optimizations. Sources: L9 p6-p19, p31-p32, p40-p50.
