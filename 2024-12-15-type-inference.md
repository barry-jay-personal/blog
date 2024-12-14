# Type Inference
## Barry Jay
### 2024-12-15

Now that we can type a self-evaluator by $\forall X.\forall Y. (X \to Y) \to (X \to Y)$
it's time to consider *type inference*. That is, given a term $t$ in some type context $\Gamma$ find a type $T$ such that $\Gamma \vdash t : T$.
This is problematic because out types extend the quantified types of Girard's System F (with tree types and subtyping) but System F does not support full type inference. So extra guidance must be provided by the programmer by either introducing new term forms (e.g. the let-terms of Hindley and Milner) or adding type annotations. Since the generic queries required for program analysis are all given by recursive triage, let us consider how new term forms might support type inference. 

Our starting point is to consider a simple type system (with subtyping) and see where inference breaks down. 



