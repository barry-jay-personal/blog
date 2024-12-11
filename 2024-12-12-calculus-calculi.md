
title: Calculus or Calculi
date: 2024-12-12

According to the [Internet Encyclopedia of Philosophy]
(https://iep.utm.edu/lambda-calculi) the λ-calculus is in fact a
family of formal systems, a family of calculi that all stem from the
same root. They may support additional term forms or reduction rules,
such as $\eta$-reduction, or give different accounts of substitution,
as implicit or explicit, or be typed or not. In turn, types may be
simple, quantified, dependent, subtyped, static or dynamic, explicit
or implicit or something in between. The shared root is that
computation is about functions, expressed as $\lambda$-abstractions.

The same variability can be found in combinatory logic. There are five
or three or two basic operators, which can be combined by application
to produce functions without any need for binding.  Indeed, it seems
that any new model of computation is destined to spawn variants that
stem from a common root.  For example, pattern calculus is rooted in
pattern-matching but there is more than one way to handle mis-matches.

Most recently, I developed tree calculus on the principal that
computations are unlabelled trees, and the programs and values are the
binary trees but there is some freedom when it comes to choosing the
reduction rules. They should maximise expressive power, be compact and
be reasonable.

In my book [Reflective Programs in Tree
Calculus](https://github.com/barry-jay-personal/tree-calculus/tree_book.pdf)
I emphasised expressive power and compactness but reasoning is
hard. That is, there are only three reduction rules, according to
whether the first argument is a leaf, stem or fork, but the second
rule does double duty, to duplicate arguments like the operator $S$ of
combinatory logic, and to support program analysis.
From this can be built *triage* for case analysis, using the rules
$$
\begin{array}
T \{f_0, f_1, f_2\} \Delta &\longrightarrow& f_0 \\
T \{f_0, f_1, f_2\} (\Delta x) &\longrightarrow& f_1x \\
T \{f_0, f_1, f_2\} (\Delta x y) &\longrightarrow& f_2 x y
\end{array}
$$


Well, everything worked just fine until it came to typing. Each triage
is a large term, and the reductions above take many steps, each of
which must be well typed. I slogged my way through that, but then the
self-interpreters use triply-nested triage, which was overwhelming.

After explaining all this to Johannes Bader in one of our Zoom
meetings, he suggested that the triage reductions above should be
rules, where triage is introduced by the following mnemonic:
$$
\Delta \Delta &=& K \\
\Delta (\Delta x) &=& S x \\
\Delta (\Delta w x) y &=& T\{w,x,y}\;. 
$$

This is more reasonable, but less compact than the original. There are
five reduction rules instead of three, but each rule does a single
job, and the typing is more straightfoward. I used this *triage
calculus* in my paper [Typed Program Analysis without
Encodings](https://github.com/barry-jay-personal/typed_tree_calculus/typed_program_analysis.pdf)
and Johannes used it in his [exploration of tree
calculus](treecalcul.us).

So now we have the *original tree calculus* of the book and *triage
calculus*. Who knows what other tree calculi will emerge in the
future?
