
*q*; (4) implication (a binary operation symbolized by ⊃ or by the = sign, for example, *p* ⊃ *q* or *p* = *q*), and (5) equidensical (a binary operation denoted by =, for example, *p* = *q*. Read “*p* is equivalent to *q*,” means that each proposition implies the other). The proposition *p* ⊂ *q* asserts that both *p* and *q* are true. It is important to note that the disjunctive “or” is always used in the inclusive sense; that is, *p* ∨ *q* asserts that at least one, possibly both, of the propositions *p* and *q* are true. In addition, the meaning of “implication” in logic differs markedly from the ordinary sense of that term. The proposition *p* ⊃ *q* asserts merely that it is not the case that *p* is true and *q* is false; that is, in classical logic *p* ⊃ *q* means that either *p* is false or *q* is true. The logical connectives introduced above are examples of logical constants. They are not independent notions. Implication may be defined in terms of negation and conjunction, and this is true for all of the connectives. In fact, all the connectives can be defined in terms of one binary operation, the so-called Schffer stroke function *p* | *q*, which may be read: “*p* is false or *q* is false.”

The logical connectives, the letters *p*, *q*, *r*, and so on that stand for propositions (propositional variables), and the parentheses, brackets, and braces needed for punctuation are formal concepts. A propositional function is a combination of concepts, formal or nonformal, containing at least one variable, which is not a proposition but becomes one when all the variables are given specified values. Examples are (1) *p* and *q*, (2) *x*² + *y*² = 1, and (3) *x* is president of the United States. Unlike a formula, a propositional function can have no truth value. On the other hand, the statement “For every integer *x*, *x*² + 1 = 0” is a proposition (not a propositional function) even though it contains a (bound) variable. A formal function is a propositional function that contains only formal concepts—for example [(*p* ∨ *q*) ⊃ *r*] ⊃ *s*. A truth function is a propositional function in which only propositional variables occur, and such that the truth value of each proposition obtained from the function by substituting specific propositions for the variables depends only on the truth values of those propositions. Examples are (1) (*p* ⊃ *q*) ⊃ *r*, (2) Napoléon was a great general and *p* (where *p* is a propositional variable). On the other hand, “Jones stated that *p* is not a truth function.

Tautologies are formal truth functions such that every proposition obtained from them by substituting specific propositions for the variables they contain has the truth value *T* (true). A truth function is contingent provided it assumes both truth values *T* and *F* (false)—here only the classical two-valued (aristotelian) truth functions are considered—and self-inconsistent provided it has only the value *F*. The character of a truth function is determined when it is shown to be self-inconsistent, contingent, or a tautology.

A truth function may be analyzed by means of a truth table, or matrix. Such tables are most first for the elementary truth functions *p* ∨ *q*, *p* ⊃ *q*, *p* ⊃ *q* as follows:

| | (I) | (II) | (III) | (IV) |
| :--- | :--- | :--- | :--- | :--- |
| *p* | *p*’ | *p* | *q* | *p* ∨ *q* | *p* | *q* | *p* ⊃ *q* | *p* | *q* | *p* ⊃ *q* |
| *T* | *F* | *T* | *T* | *T* | *T* | *T* | *F* | *T* | *T* | *T* |
| *T* | *F* | *T* | *T* | *T* | *F* | *F* | *T* | *T* | *F* | *F* |
| *T* | *T* | *F* | *T* | *T* | *T* | *T* | *T* | *T* | *F* | *F* |
| *F* | *T* | *T* | *F* | *T* | *F* | *T* | *F* | *F* | *F* | *T* |

In every table each row of the last column gives that truth value of the function that is determined by those truth values (assigned to the variables that are entered in the preceding columns of that row.

All tautologies can be deduced from a set just four of them:

- P1  ( *p* ∨ *p* ) ⊃ *p*
- P2  *q* ⊃ ( *p* ∨ *q* )
- P3  ( *p* ∨ *q* ) ⊃ ( *q* ∨ *p* )
- P4  ( *q* ⊃ *r* ) ⊃ [ ( *p* ∨ *q* ) ⊃ ( *p* ∨ *r* ) ]

These simple tautologies were selected by Alfred North Whitehead and Bertrand Russell in their monumental work *Principia Mathematica* as the basic set from which all tautologies can be derived. This is analogous to what is done in an axiomatic geometry in which all the theorems of the geometry are deduced from a selected set of axioms or postulates that are assumed to be true.

It was proved by E. L. Post that postulates P1–P4 are consistent; that is, it is impossible to deduce from truth functions *X* and *X*. He also proved that the four postulates form an independent set; that is, no one of the postulates can be deduced from the others.

In nonaxiomatic logics the principle of the excluded middle (that is, each proposition is either true or false) is not valid. There are, then, at least three truth values possible for a proposition, and for this reason such logics are known as many-valued. If “true” be interpreted in mathematics to mean “provable,” then a proposition can be called false provided its negation is provable, then the law of excluded middle is demonstrably false, since it has been shown that mathematics contains proposition *p* such that neither *p* nor its negation *p*’ is provable. See BOOLEAN ALGEBRA; EUCLIDEAN GEOMETRY; MATHEMATICS, SCIENCE.

## Mathematical logic

*Mathematical logic* is an area of research that has emerged from the study of formal systems. It has its roots in work on the foundations of mathematics in the nineteenth and early twentieth centuries, showing that the customary forms of mathematical reasoning can be adequately expressed in formal (purely symbolic) systems. Mathematical logic contains four areas of research: proof theory, set theory, model theory, and recursion theory.

The original objective of work in the foundations of mathematics was the analysis and precise formulation of mathematical concepts, such as “limit,” “function,” and “differential manifold,” as well as a complete and explicit determination of the valid forms of mathematical argument. This goal was achieved by the formalization of mathematics.

A formal system consists of a symbolic notation (or language) with rules for constructing expressions using the specified notation, axioms (expressions taken as given), and rules of inference used to derive additional expressions from a given set of expressions. To formalize an area of mathematics means to give a procedure for representing proofs in the specified area within a definite formal system. One formal system that is adequate for the formalization of all existing mathematics is theory of set theory, which can be set up in a variety of ways. There are various standard systems of axioms for set theory, notably the axiom system ZFC, consisting of axioms proposed by E. Zermelo and A. Fraenkel, with the addition of the axiom of choice.

Proof theoretic research continues the study of formal systems that are adequate for the formalization of various parts of mathematics. Two basic results, due to K. Gödel, relate to the adequacy of formal systems in general: the so-called completeness and incompleteness theorems. The completeness theorem essentially states that the laws of inference are adequately mirrored in the usual formal systems in the sense that any law of inference that is in fact valid in all mathematical contexts is derivable in any of these systems. The incompleteness theorem, on the other hand, can be interpreted as stating that it is impossible to give a completely satisfactory axiom system for any theory that can serve as a formal foundation for mathematics. See GÖDEL’S THEOREM.

Axiomatic set theory was developed in part as a way of obtaining a formalism adequate for all of mathematics, and also for concrete mathematical reasons connected with the development of general topology and measure theory around 1900. Set theory is probably the most active research area within mathematical logic. It has been shown that a variety of problems in analysis, general topology, and algebra (especially homological algebra) cannot be settled within the framework of any of the standard set theoretic systems like ZFC. See SET THEORY.
