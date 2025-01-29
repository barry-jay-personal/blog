# Engineering or Science
## Barry Jay
### 2025-01-25

Engineering builds useful things out of components that are imperfectly understood.

Science pulls apart interesting things, the better to understand them.

Engineering is synthetic.

Science is analytic.

Engineering composes.

Science analyses.

Now, category theory is a mathematical theory in which everything is built in just one way, by composing arrows, as a generalisation of function composition.
It is remarkably successful as a uniform way of building all sorts of things. It could claim to be a mathematical foundation for engineering.
However, it cannot, almost by definition, be a foundation for science, since there is no way to analyse anything. One cannot distinguish things that have the same uses.
This fact is captured by the Yoneda Lemma (if you know what that is).

Similar remarks apply to formal logic. Its rules deduce new propositions from old premises without ever analysing the structure of the premises. It is compositional, or synthetic, just like engineering.

Again, in computing, the $\lambda$-calculus is a great way to define
and compute functions. You can compose them but, once built, you can
never analyse them within the calculus. It supports software
engineering but not computer science.

Thus, the Curry-Howard-Lambek Isomorphism between logic, $\lambda$-calculus and category theory is a deep correspondence between three different ways of thinking about engineering. It is deeply moving. It inspires new ideas in every direction. But it isn't analytic; it isn't science. 


For computer science, you need to break the
abstractions by encoding $\lambda$-terms  as syntax trees to be analysed. These analyses may infer types, or apply optimisations using computations that are not representable without encoding. 

The simpler way would be to take the syntax trees as fundamental, except that the choice of syntax is artificial, driven by human choices.
However, all syntax is built on some finite alphabet, which can be encoded using small, unlabeled trees, or natural trees. So each label in a syntax tree can be replaced by a small tree, and the resulting tree of trees can be flattened to a single natural tree. So let's base computing on natural trees and work up from there, to build tree-based calculi. 
