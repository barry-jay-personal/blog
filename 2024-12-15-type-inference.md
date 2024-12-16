# Type Inference
## Barry Jay
### 2024-12-15

Now that we can type a self-evaluator by $\forall X.\forall Y. (X \to Y) \to (X \to Y)$
it's time to consider *type inference*. That is, given a term $t$ in some type context $\Gamma$ find a type $T$ such that $\Gamma \vdash t : T$.

The basic challenge is to type an application $f z$ where $f:P$ and $z:Z$. If $P$ is a function type $U\to V$ then it is enough to solve $Z < U$. The other interesting case is when $P$ is a fork type $\Fork U V$. That is, we must solve $Fork~U~V < Z \to T$ for $T$ or perhaps show that there is no solution. In the absence of special subtyping rules, this is relatively straightforward. If $U$ is a leaf type then let $T$ be $V$. If $U$ is a stem type $\Stem U_1$ then solve $V < $Z\to V_1$ for some $V_1$ and solve $U < Z \to V_1 \to T$ for $T$. If $U$ is a fork type $Fork\{U_1}\ {U_2}$ then, assuming that $Z$ is a variable, we require that $T$ be covariant in $Z$ and we must solve $U_1 < Leaf \to \{Leaf/Z\}T$ and $U_1 < \forall Z_1. Z_1 \to \{Stem\ {Z_1\}/Z\}T$ and $V_1 < \forall Z_1. \forall Z_2. _1\to Z_2\to \{Fork\ {Z_1}\ {Z_2}/Z\}T$. 

From memory, it is easy enough to type the basic queries, such as isFork. We could also simply-type all of the $\mu$-recursive arithmetic functions as follows. Add a type constant Nat for the natural numbers, and subtyping rules to type zero, successor and case analysis. Recursion is typed by adding another constant that types $\omega_2$ and a subtyping rule for fixpoints of numerical functions. 

The next challenge is to type fixpoints on arbitrary types. This can be done by adding a new term form $fix\ x = t$ with a type derivation rule to capture its iterative behaviour. That is, $\Gamma \vdash fix\ x\ t : \forall \vec X. U \to V$ if we can show $\Gamma, x : \forall \vec X. U\to V \vdash t : \forall \vec X. U \to V$.  

Now consider triage{f0,f1,f2}. The three cases  should be quantified by zero, one or two type variables. So make triage a new term form, and add the corresponding rule. 

Finally, consider **bf**. Perhaps this works in a similar manner. 



This is problematic because our types extend the quantified types of Girard's System F (with tree types and subtyping) but System F does not support full type inference because of ambiguities that arise when function arguments have quantified types. The traditional solution is to require all quantifiers be on the outside, except in precisely controlled circumstances, as when typing let-expressions. Let us try something similar for tree calculus. What follows is my best recollection and guesses, but is not to be relied upon. For now, these are personal notes, not for public consumption.

Before getting into details, the key challenge is to type an application
