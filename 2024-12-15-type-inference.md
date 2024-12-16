# Type Inference
## Barry Jay
### 2024-12-15

Now that we can type a self-evaluator by $\forall X.\forall Y. (X \to Y) \to (X \to Y)$
let's consider *type inference*. That is, given a term $t$ in some type context $\Gamma$ find a type $T$ such that $\Gamma \vdash t : T$.
For $\lambda$-calculus, the sweet spot is the Hindly-Milner type system. The types are split into monotypes $ T ::= X | T \to T | Nat | Bool | ...$ and *type schemes* $\tau ::= T | \forall X. \tau$. These are related by *let-terms* which are typed by 

$\frac{\Gamma \vdash u:U \quad \Gamma, x: \forall \vec X. U \vdash t:T}{\Gamma \vdash let\ x=u\ in\ t : T}$

where $\forall\vec X$ denotes the quantification of a sequence $\vec X$ of type variables. 

given by 
I don't yet have the answers but am determined to keep blogging, so here are my initial thoughts. 

The basic challenge is to type an application $f z$ where $f:P$ and $z:Z$. If $P$ is a function type $U\to V$ then it is enough to solve $Z < U$. The other interesting case is when $P$ is a fork type $Fork\ U\ V$. That is, we must solve $Fork\ U\ V < Z \to T$ for $T$ or perhaps show that there is no solution. In the absence of special subtyping rules, this is relatively straightforward. If $U$ is a leaf type then let $T$ be $V$. If $U$ is a stem type $Stem\ U_1$ then solve $V < Z\to V_1$ for some $V_1$ and solve $U < Z \to V_1 \to T$ for $T$. If $U$ is a fork type $Fork\{U_1}\ {U_2}$ then, assuming that $Z$ is a variable, we require that $T$ be covariant in $Z$ and we must solve 
-  $U_1 < Leaf \to [Leaf/Z]T$
- $U_2 < \forall Z_1. Z_1 \to [Stem\ Z_1/Z]T$
- $V_1 < \forall Z_1. \forall Z_2. Z_1\to Z_2\to [Fork\ Z_1\ Z_2/Z]T$. 

Now consider recursion. In the simplest case, we required $f: (U\to V) \to (U\to V)$ to type $Z [f] : U\to V$. This is enough to type arithmetic recursion, where $U$ and $V$ are both Nat but generic queries require a more polymorphic approach, where $U\to V$ becomes $\forall X_1,...X_n. U\to V$ also written $\forall\vec X. U\to V$. Now the type of $f$ has quantifiers on the argument type of a function type. In general, this would make type inference undecidable but we can adapt the Hindly-Milner type system, where all quantifiers appear on the outside as follows. 

Consider a function $f = \lambda x.t$ whose intended type is $\tau \to T$ where $\tau$ is a quantified type. In general, this type cannot be inferred.  However, the most important case is when the argument $u$ of $f$ is already known.  So replace the application with $let\ x=u\ in\ t$ then infer the type $U$ of $u$ then infer the type $T$ of $t$ in a context where the type scheme $\tau$ of $x$ is the maximally allowed quantification of $U$. 


That is, we introduce a new term form, the let-term for which we are able to infer a type. The same approach works for fixpoints by the rule

$\frac{\Gamma, x : \forall \vec X. U\to V \vdash t : U\to V}
{\Gamma \vdash fix\ x = t: U\to V}$

where $fix\ x = t$ represents $Z[\lambda x. t]$. 
It is not yet clear how much extra work (if any) will be needed to handle the special rules used to type the self-evaluator. 

So the plan is as follows. The source language must support let-terms and fixpoints; these can be desugared after inference. The type system must separate the monotypes (no quantifiers) from the type schemes (quantified monotypes), with new type constants such as Nat added as required. 
General solutions for  inequalities $U<V$ and $U< V \to ?$ must be found (by mutual recursion?). Type inference adapts the usual algorithms for  typing let-polymorphism. 

