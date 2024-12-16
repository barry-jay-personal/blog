# Type Inference
## Barry Jay
### 2024-12-15

Now that we can type a self-evaluator by $\forall X.\forall Y. (X \to Y) \to (X \to Y)$
let's consider *type inference*. That is, given a term $t$ in some type context $\Gamma$ find a type $T$ such that $\Gamma \vdash t : T$.
What follows are my latest thoughts on the problem, not a solution. I'm a bit reluctant to post ideas that are half-baked, if not wrong, but that approach led to years of radio silence so here 'tis.

For $\lambda$-calculus, the sweet spot is the Hindly-Milner type system. The types are split into monotypes $ T ::= X | T \to T | Nat | Bool | ...$ and *type schemes* $\tau ::= T | \forall X. \tau$. These are related by *let-terms* which are typed by 

$\frac{\Gamma \vdash u:U \quad \Gamma, x: \forall \vec X. U \vdash t:T}{\Gamma \vdash let\ x=u\ in\ t : T}$

where $\tau = \forall\vec X.U$ denotes the quantification of $U$ by a sequence $\vec X$ of type variables that are free in $U\to V$ but not free in $\Gamma$. 
Operationally, $let\ x = u\ in\ t$ corresponds to $(\lambda x. t)u$ but now $\lambda x. t$ would be typed by $\tau\to T$ which has a quantified argument type. In general, type inference cannot infer such types, so inference for the let-term begins by inferring the argument type (scheme) of $u$. 

My goal is to adopt the same approach for tree calculus. Where quantified argument types threaten to block inference, let us introduce new term forms that only require type schemes. 

The basic challenge for tree calculus is to type an application $f z$ where $f:P$ and $z:Z$. If $P$ is a function type $U\to V$ then it is enough to solve $Z < U$. The other interesting case is when $P$ is a fork type $Fork\ U\ V$. That is, we must solve $Fork\ U\ V < Z \to T$ for $T$. In the absence of special subtyping rules, this is relatively straightforward.  If $U$ is a function type then fail. If $U$ is a leaf type then let $T$ be $V$. If $U$ is a stem type $Stem\ U_1$ then solve $V < Z\to V_1$ for some $V_1$ and solve $U < Z \to V_1 \to T$ for $T$. If $U$ is a fork type $Fork\{U_0}\ {U_1}$ and $V$ is $U_2$ then we are typing a triage. Assuming that $Z$ is a variable, we require that $T$ be covariant in $Z$ and we must solve 
-  $U_0 < Leaf \to [Leaf/Z]T$
- $U_1 < \forall Z_1. Z_1 \to [Stem\ Z_1/Z]T$
- $U_2 < \forall Z_1. \forall Z_2. Z_1\to Z_2\to [Fork\ Z_1\ Z_2/Z]T$. 

In turn, this challenge is like that of let-terms. The sub-expressions, of types $U_0$ and $U_1$ and $U_2$ must be shown to have appropriate type schemes before typing the triage as a whole. 

Now consider recursion. In the simplest case, we required $f: (U\to V) \to (U\to V)$ to type $Z [f] : U\to V$. This is enough to type arithmetic recursion, where $U$ and $V$ are both Nat but generic queries require a more polymorphic approach, where $U\to V$ becomes $\forall X_1,...X_n. U\to V$ also written $\forall\vec X. U\to V$.  

A first attempt might use  a new term form $fix\ f = t$ to represent $Z[\lambda f. t]$. Now  a premise of the form 
$\Gamma, f : \forall \vec X. U\to V \vdash t : U\to V$ does not show how to type $f$ but we can type the size function $fix\ f = s$ by the rule 

$\frac{\Gamma, f : \forall X. X\to Nat \vdash s: X\to Nat}{\Gamma\vdash fix\ f = s : X\to Nat}$. 

The question here is whether $T = Nat$ can be inferred when trying to solve $\Gamma f : \forall X. X \to T \vdash s : X \to T$. It seems that it can be done if $X$ is not free in $T$ or if $T$ is $X$ but the general case is uncertain. 

More generally, the equality function has type $\forall X. \forall Y. X \to Y \to Bool$ so we must allow $fix$ to take many arguments, by the rule 

$\frac{\Gamma, f : \forall \vec X. \vec X\to T \vdash t: \vec X \to T}{\Gamma\vdash fix\ \vec x = t : \vec X\to T}$

Finally, it is quite unclear what adjustments must be made to infer a type $\forall X. X \to Asf X$ for a self-evaluator. Now the argument type variable $X$ is free in the result type, and the many new subtyping rules complicate things. We'll cross this bridge when we come to it. 

So the plan is as follows. The source language must support let-terms and fixpoints; these can be desugared after inference. The type system must separate the monotypes (no quantifiers) from the type schemes (quantified monotypes), with new type constants such as Nat added as required. 
General solutions for  inequalities $U<V$ and $U< V \to ?$ must be found (by mutual recursion?). Type inference adapts the usual algorithms for  typing let-polymorphism, by adding rules for the new term forms. 

