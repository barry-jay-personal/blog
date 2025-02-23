# Stuck on Type Inference
## Barry Jay
### 2025-02-23

Little progress to date on type inference, but I'm going to share anyway; maybe something will shake loose; the only theorem is both peculiar and useless. 

The ultimate goal is a broad-spectrum typed programming language. At the front end are the higher-order programs of functional languages. 
At the back end is the memory hierarchy, with the heap, stacks and registers of computing machines, to be expressed as trees.
In the middle are the intensional programs required for program analysis. 
This is enough work for an army, and I am lousy at multi-tasking, so am currently working on the front end, for which type inference seems the most pressing task. 

This throws up some fundamental questions which are already relevant to combinatory logic, so let's begin there. Indeed, this is still tough, so let's strip down to the simplest possible setting. 
Traditionally, this would a simply-typed calculus with function types built from some type constants for, say, natural numbers and booleans. 
However, as mentioned in an earlier post, we want to work with *program types*. 
In a tree calculus, these would be types for leaves, stems and forks, but in a combinatory logic built from the operators $S$ and $K$ they will be types for terms of the form $K, Ku, S, Su, Suv$. 
Further, and here is the shocking part, the most primitive calculus need not support function types! Thus, the types are of the form

$T ::= K_0 | K_1 T | S_0 | S_1 T | S_2 T T $

There are three type derivation rules. The two obvious ones are that $K:K_0$ and $S:S_0$. The rule for typing an application is 
if $M : T$ and $N:U$ then $MN {:} res {T}{ U}$ where $res{T}{U}$ is the *result type* that comes from applying a function of type $T$ to an argument of type $U$. For example, if we actually had function types and $T$ was $U\to V$ then $res{T}{U}$ would be $V$. With program types, however, we have rules like $res{K_0}{U} = K_1 U$ etc. The most complex rule is for $res{(S_2 T_1 T_2)}{U}$. Again, if we had function types, we might expect $res{S_2(U\to V\to W)(U\to V)}{U}= W$ but the same effect can be captured by having $res{(S_2T_1T_2)}{U} = W$ if $res{T_2}U = V$ and $res{T_1}{U} = T_3$ and $res{T_3}{V} = W$. 

The resulting system is sound, in that reduction preserves typing, and supports type inference by inferring result types. So it is peculiar, for lack of function types, and pathetic for its lack of expressive power.

The next big challenge is to support recursive functions. This leads to some technical challenges, but before we get to those there is a big-picture problem. Since we are recursing, or looping, over functions, the program types are too rigid since, in a sense, they only type one program each. To add flexibility, we need *function types*. 

So let us put aside fixpoints for now, and consider function types. Although it is tempting to also consider the typing of lambda-abstractions, it turns out that merely adding function types is a challenge. Of course, this seems silly. How can adding a new type form without changing the terms possibly cause problems? Well, it is easy enough to show that reduction preserves typing. The problem is with type inference.

In more detail, to check a subtyping relation $S_2 T_1 T_2 < U \to W$ must infer the result type $V_2$ of $T_2$ and $U$. Conversely, to infer a result type from $U_1 \to V_1$ and $U_2$ we must check that $U_2 < U_1$.  So checking subtyping and inferring result types must be defined by mutual recursion. The complexity of the proofs grows rapidly, and I have not found my way through yet. Various side-issues arise, which I won't try to explain here, but the fundamental challenges seem to arise from the interplay  of subtyping, result typing and contravariance. 

Zooming out, there should be a solution, and it shouldn't be so complicated, since we haven't even bound any variables. So what am I missing? 



