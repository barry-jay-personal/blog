# Polymorphism Without Parameters
## Barry Jay
### 2025-03-04

In lambda-calculus, polymorphism is captured by quantified function types. 
For example, the identity function $\lambda x.x$ has type $\forall X. X \to X$. 
This is a *principal type* for the identity function since all other types for it, of the form $T \to T$,
can be derived by instantiating the type parameter $X$ to be $T$. 

However, in a combinatory setting, much of this polymorphism can be supported by subtyping of *program types*. 
For example, the identity function given by $SKK$ has program type $S_2 K_0 K_0$ which is a subtype of $T\to T$ for any type $T$. 
Program types first appeared as the leaf, stem and fork type constructors for tree calculus, but they are already of interest when typing traditional combinatory logic, 
built using the operators $S$ and $K$. 

The corresponding types are given by 

$T::= K_0 | K_1 T | S_0 | S_1T | S_2 T | T \to T$.

There are three type derivation rules. 

if $S_0 < T$ then $S: T$ 

if $K_0 < T$ then $K: T$ 

if $M: U\to V$ and $N: U$ then $MN : V$ 

In turn, the subtyping relation has eleven rules. Most rules are structural, e.g. if $V_1 < V_2$ then $U\to V_1 < U\to V_2$. 
Three are used to type programs, e.g. $K_0 < U \to K_1 U$. The remaining two are inspired by the reduction rules, e.g. $K_1 U < V \to U$. 
Here are five verified results.

First, even though subtyping in the type derivation rules is limited to typing of operators (for simplifying proofs), it can be extended to arbitrary typings:    

if $M : T_1$ and $T_1 < T_2$ then $M: T_2$. 

Second, reduction preserves typing, so the system is sound. 

Third, we can derive the usual typings for $S$ and $K$ in that, for all types $U,V$ and $W$ we can derive 

$S : (U\to V\to W) \to (U\to V) \to U\to W$

$K: U\to V\to U$. 

Fourth, every *program* (i.e. normal form) is typed by its program type. For example, the identity function $SKK$ has program type $S_2 K_0 K_0$. 

Fifth, program types are *principal*: if $p$ is a program of type $T$ whose program type is $P$ then $P<T$.  

It is not yet clear how expressive this is compared to System F or even the Hindley-Milner type system. 
The canonical example of let-polymorphism is the self-application of the identity function given by 

let $f = \lambda x.x$ in $f$ $f$ 

Translated to combinatory logic, this becomes $SIII$. Now $I :I_0$ where $I_0 = S_2 K_0 K_0$ and $SII : S_2 I_0 I_0 < I_0 \to I_0$ impliers that $SIII : I_0$ as required. 
It seems that many of the usual examples can be typed in the same manner. 

Concerning System F, any type derivation corresponds to a type derivation for a combinator in an empty context. 
Further, this combinator reduces to a normal form (as do all terms in System F) which is thus a program, which has principal type, its program type! 
However, exploiting the strong normalisation of System F seems like cheating, and will not work if fixpoints are introduced. 

Backing up, the search for principal types reduces to the search for *result types*. 
Given a function of type $T$ and an argument of type $U$, find the smallest type $V$ such that $T < U \to V$. This $V$ is the result type from applying $T$ to $U$. 
In System~F typing, $T$ is usually a quantified function type $\forall X_1 ... X_m. U_1 \to V$ and $U$ is a quantified type $\forall Y_1 ... Y_n . U_2$. 
However, there is no single algorithm that will find all solutions: type inference in System F is undecidable. 
By contrast, type inference is supported by the Hindley-Milner type system as the use of quantifiers is constrained. 

Therefore, it is not clear if type inference is decidable using program types, or that there is an algorithm for finding result types.
The negative result for System~F is discouraging. On the other hand, perhaps the cheating approach outlined above can be reworked to avoid reducing terms. 
Even if there is no general algorithm, it would be interesting to find a partial solution, analogous to the Hindley-Milner approach. 
So this is my next concern. 

