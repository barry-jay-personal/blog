# Stuck on Type Inference
## Barry Jay
### 2025-02-23

Little progress to date on type inference, but I'm going to share anyway; maybe something will shake loose; the only theorem is both peculiar and useless. 

The ultimate goal is a broad-spectrum typed programming language. At the front end are the higher-order programs of functional languages. 
At the back end is the memory hierarchy, with the heap, stacks and registers of computing machines.
In the middle are the intensional programs required for program analysis. 
This is enough work for an army, and I am lousy at multi-tasking, so am currently working on the front end, for which type inference seems the most pressing task. 

This throws up some fundamental questions which are already relevant to combinatory logic, so let's begin there. Indeed, this is still tough, so let's strip down to the simplest possible setting. 
Traditionally, this would a simply-typed calculus with function types built from some type constants for, say, natural numbers and booleans. 
However, as mentioned in an earlier post, we want to work with *program types*. 
In a tree calculus, these would be types for leaves, stems and forks, but in a combinatory logic built from the operators $S$ and $K$ they will be types for terms of the form $K, Ku, S, Su, Suv$. 
Further, and here is the shocking part, the most primitive calculus need not support function types! Thus, the types are of the form

$T ::= K_0 | K_1 T | S_0 | S_1 T | S_2 T T $

There are three type derivation rules. The two obvious ones are that $K:K_0$ and $S:S_0$. The rule for typing an application is 
if $M : T$ and $N:U$ then $MN {:} res {T}{ U}$ where $res{T}{U}$ is the *result type* that comes from applying a function of type $T$ to an argument of type $U$. For example, if we actually had function types and $T$ was $U\to V$ then $res{T}{U}$ would be $V$. With program types, however, we have rules like $res{K_0}{U} = K_1 U$ etc. The most complex rule is for $res{S_2 T_1 T_2}{U}$. Again, if we had function types, we might expect $res{S_2(U\to V\to W}{U\to V} = U\to W$ but the same effect can be captured by having $res{(S_2T_1T_2)}{U} = W$ if $res{T_2}U = V$ and $res{T_1}{U} = T_3$ and $res{T_3}{V} = W$. 

The resulting system is sound, in that reduction preserves typing, and supports type inference by inferring result types. 

The next big challenge is to support recursive functions. This leads to some technical challenges, but before we get to those there is a big picture problem. Since we are recursing, or looping, over functions, the program types are too rigid since, in a sense, they only type one program each. To add flexibility, we need *function types*. 

So let us put aside fixpoints for now, and consider function types. Although it is tempting to also consider the typing of lambda-abstractions, it turns out that merely adding function types is a challenge, one that I haven't solved! 

Of course, it seems silly. How can adding a new type form without changing the terms possibly cause problems? Well, it is easy enough to show that reduction preserves typing. The problem is with type inference. 

Backing up, to type recursion requires that program types be converted to function types, for which we can use subtyping. Further, the basic rules for result types can all be represented as subtyping rules to function types. For example, we could have $K_0 < U \to K_1 U$. Then the natural subtyping rules for function types is $U_1 \to V_1 < U_2 \to V_2$ if $U_2 < U_1$ and $V_1 < V_2$ which is *contravariant$ in the argument types. 


All of this works well enough for deriving types, without any mention of 



Here is a vague account. 

The difficulties arise from the interplay of result Perforce, I must be vague about this, since I don't properly understand, 


Since I haven't 

At this point, it is tempting to 



, more or less, there is only one In the typed tree calculus, this was achieved by adding subtyping rules of the form $\Omega_2 < \Omega_2 \to Fix{T}$. In our current setting, this could be converted to a new rule for result types, say $res{\Omega_2}{\Omega_2} = Fix{T}$. Actually, $T$ should be replaced by a polymorphic type, which introduces more problems, but  Ignoring the details

