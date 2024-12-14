# Type Inference
## Barry Jay
### 2024-12-15

Now that we can type a self-evaluator by $\forall X.\forall Y. (X \to Y) \to (X \to Y)$
it's time to consider *type inference*. That is, given a term $t$ in some type context $\Gamma$ find a type $T$ such that $\Gamma \vdash t : T$. 
