# Tweets on Trees
## Barry Jay
### 2024-12-23

Here are some tweets about tree calculus that I wrote in September, 2020. My goals was to summarise each chapter of the book in one tweet but I ended up with almost double that number. The text was illustrated with some cartoons and diagrams of trees from the book, but they aren't replicated here. 

I've just finished drafting my new book "Reflective Programs in Tree Calculus".

Good computer science needs theorems (to show that bad things don’t happen) an implementation (to show that good things do happen) and a story (that ties it all together).

At heart, computer science is the study of programs. An  implementation is an interpreter or compiler, i.e a program that acts on programs. In a good story, all these programs have equal status, so interpreters can be self-applied. This requires a theory of reflective programs.

Turing machines do reflection by encoding machines as numbers on a tape. But this computation is outside of the model, so Turing machines don't make a good theory of computation! Nor do natural numbers.

Lambda calculi do most reflection by encoding terms as syntax trees. But this computation is outside of the model, so lambda calculus doesn't make a good theory of computation! Nor does combinatory logic.

So reflective programming is hard, but no harder than operating on your own brain. 

Syntax trees support reflection but are artificial, so use natural trees, i.e. without labels, as in the frontispiece shown before.

Let parsing convert syntax to natural trees. Meet Fir (a tree made of blank tape).

In tree calculus, the programs, functions and data structures are exactly the binary trees, which are leaves, stems or forks. Other trees are computations. All these can be written as combinations of a single operator called Node, drawn as a small triangle.

The rules (K) and (S) delete or copy the third argument, so tree calculus: supports all combinators; has macros for lambda-abstraction; and is Turing-complete. The rule (F) adds factorisation, as in SF-calculus.

When recursion is expressed by fixpoints, the functions are traditionally not stable, without normal form, but in tree calculus they are. Any instability is caused by function application. Meet Shasta, the flower of recursion.

Tree calculus also supports program analysis, such as a test for program equality. 

Such program analysis is not possible in traditional models, as Fir understands.

A tree calculus program f can be tagged with a comment, type or other guidance t that can be recovered by applying a query to it, but behaves like f when it is applied: 
     $tag (t,f) =\Delta(\Delta t)(\Delta(\Delta f)(\Delta\Delta(\Delta\Delta)))$. 
Tags could support just-in-time program analysis.

Self-interpretation for branch-first (eager) evaluation and root-first (lazy) evaluation uses trees that are very small (<1000 nodes). Maybe self-awareness is not so complicated :)

Combinatory logic is incomplete since equality is not definable. Also, it has no *meaningful translation* of tree calculus.

VA-calculus supports variables and also lambda-abstractions that have environments, much as closures do. This replaces all the meta-theory, for substitution, variable renaming etc, with 7 simple equations.

Although VA-calculus is incomplete (equality is not definable) there is a *meaningful translation* to it from tree calculus. Here is the translation of Node to a combination of V and A, given as a labelled tree.

There is also a meaningful translation from VA-calculus to tree calculus. Here is the tree for A.

SF-calculus supports divide-and-conquer algorithms, such as equality or pattern-matching, using combinations built from operators S and F.

There are meaningful translations between SF-calculus and tree calculus. 
