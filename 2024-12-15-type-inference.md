# Type Inference
## Barry Jay
### 2024-12-15

Now that we can type a self-evaluator by $\forall X.\forall Y. (X \to Y) \to (X \to Y)$
it's time to consider *type inference*. That is, given a term $t$ in some type context $\Gamma$ find a type $T$ such that $\Gamma \vdash t : T$.
This is problematic because out types extend the quantified types of Girard's System F (with tree types and subtyping) but System F does not support full type inference. So let us revert to a simple type system (with subtyping) and build from there. 





