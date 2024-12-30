# Identify Syntax and Semantics!
## Barry Jay
### 2025-01-02

The semantics of tree calculus is its syntax!

At a glance, this seems to be a nonsense.  If language is to describe
the world then we must understand the relation between a word and its
meaning, between its syntax and its semantics. For programming
languages, the world is mathematical.  Traditionally, programs
describe functions as understood by their input-out relation. Two
programs are equivalent if they have the same semantics. In this
manner, an understanding of semantics can free us from the accidents
of syntax. As well as programs, we can compare programming languages,
by using translations of syntax that preserve semantics.

However, this separation of syntax and semantics is a form of dualism,
a separation of mind and matter. It breaks down when programs are used
to analyse other programs, when programs are the things being
described or computed, as in tree calculus. This requires a form of
materialism.

So the natural binary trees (those without labels) are both the syntax
and the semantics of tree calculus! Certainly the natural trees are
mathematical objects, no matter what foundation your mathematics
adopts.  Their identification with syntax is a bit of a stretch, since
we must choose a symbol to represent a node, we still have brackets and
we still read from left to right. The key point, however, is that
equivalence of programs is decidable, indeed, trivial. No matter the
syntactic details, two programs have the same semantics if and only if
they are equal.  By contrast, in all traditional models of
computation, equivalence of programs is undecidable, because of the
Halting Problem.

These thoughts have rescued me from the temptation to build a
categorical model of tree calculus. For the untyped calculus, the
objects would be the natural numbers (representing tuples of binary
trees), and the arrows from m to n would be n-tuples of binary trees.
The resulting category should be cartesian-closed, in the traditional
way. However, what would be the point of this dualism? The binary
trees are easily understood, without adding a layer of formalism on
top.  Well, let me back up a little. There may well be some
interesting theorem about tree calculus that is best expressed in the
language of category theory, but until I know what it is, I won't have
a target to aim for, in the way that self-evaluation has been a target
until now.

Having touched on dualism, let me share a thought about Richard
Dawkin's selfish gene. The titular claim of his book is that evolution
is driven by copying of genes, not organisms. He also says that a gene
is a recipe not a blueprint. In more detail, DNA is a recipe for
building another organism, not a blueprint that outlines the organism.
However, **a genome is both recipe and a blueprint**. It is a recipe
for making copies of itself. Perhaps this serves as a definition of
life itself.  Something is alive if, in the right environment, it is
both a recipe and a blueprint.  In this sense, Conway's Game of Life
supports living things. Perhaps tree calculus does, too.