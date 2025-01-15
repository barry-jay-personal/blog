# Hack the Types not the Terms
## Barry Jay
### 2025-01-16

Now that we can type a self-evaluator by $\forall X.\forall Y. (X \to Y) \to (X \to Y)$
let's consider *type inference*. That is, given a term $t$ in some type context $\Gamma$ find a type $T$ such that $\Gamma \vdash t : T$.
 What follows are my latest
thoughts on the problem, not a solution. I'm a bit reluctant to post
ideas that are half-baked, if not wrong, but that approach led to
years of radio silence so here 'tis. 

Traditionally, type inference has
required us to hack the term language in some way, e.g. by adding
type decorations or let-terms, but my goal is to leave the term
language unchanged, and merely hack the type system.  To appreciate
this, let us consider the self-application of the identity program $I$
in four variants of $\lambda$-calculus.

In pure $\lambda$-calculus, $I$ is given by $\lambda x .x$.

In simply-typed $\lambda$-calculus, each
term has an explicit type, i.e. the type is part of the structure of
the term. Thus, there is an identity function for each type $U$,
namely
$$I^U = (\lambda x^U. x^U)^{U\to U} .$$
The self-application of $I$ becomes $I^{U\to V}\ I^U$.

In System F, the types $T$ also form a sort of $\lambda$-calculus

$T ::= X \ | \ T\to T \ | \ \forall X. T$

where $\forall X. T$ binds the type variable $X$ in $T$. Now there is
a parametrically-polymorphic identity function

$I = \Lambda X. \lambda x^X. x^X$

but self-application requires that I be applied to its own type in

$I\ (\forall X. X \to X)\ I$

which hacks the term language in new ways. Further, type inference for
this must discover the type $\forall X. X \to X$ used in the type
application. Unfortunately, as is well known, even type-checking for
System F is undecidable, so that type inference is hopeless.

Between simply-typed $\lambda$-calculus and System F lies the
Hindley-Milner type system with its let-polymorphism. It limits type quantification by separating the *monotypes* $T$ which are like the simple types, from the *type schemes* which apply quantifiers to the monotypes, so that all quantifiers are on the outside. Now the
self-application of $I$ becomes 

$let\ f = \lambda x. x\ in\ f\ f .$

This could be de-sugared to the application $(\lambda
f. f\ f)(\lambda x.x)$ but then it is hard to determine the type of
$f$ in $\lambda f. f f$. By providing its value $\lambda x. x$ first,
we can infer the type of $f$ to be the principal type of $\lambda x.x$
namely $\forall X. X \to X$ and all is well.

Still, each variant of $\lambda$-calculus requires its own hacks to
the term-language, and these grow more elaborate as the subtlety of
typing increases.

The challenges are a little different in tree calculus. The
application $(\lambda f. f\ f)(\lambda x.x)$ corresponds to 
$(SII)I$. Now $I$ has principal type 

$Id = Fork (Stem (Stem\ Leaf))(Stem\ Leaf))$

and the value of $SII$ has a principal type $Fork (Stem\ Id) Id$. So far, there is no need for quantifiers. Rather, the
challenge is to handle the supertyping of the tree type to a function
type. That is, find a type $V$ such that $$Fork (Stem Id) Id <
Id \to V$$. More generally, for given types $T$ and $U$, find the most
general $V$ such that $T<U\to V$.

Note that there is no need to hack the term language with type
decorations or let-terms. Further, it is clear how to solve $T < U\to
?$ with respect to the basic subtyping rules.

However, everything becomes heavy when considering the additional
rules needed to type queries, self-evaluators, etc. Queries seem to
need need quantified types (triage must be universal). Self-evaluators
need AsFunction types. If these can be typed using type schemes then type inference should be possible. 
