# Principal Types for Combinators
## Barry Jay
### 2025-03-03

Typed tree calculus uses subtyping to express polymorphism but type inference requires *result types*. 
That is, given a function of type $T$ and an argument of type $U$ find the best (smallest) type $V$ for the application. 
So let's put subtyping aside for now and try to derive types using result types instead. To begin, let us consider combinatory logic, with operators $S$ and $K$ and types given by 

$T::= K_0 | K_1 T | S_0 | S_1T | S_2 T | T \to T .$

The function types may not be strictly necessary but certainly support more familar typings. The indiviudal rules for forming result types and deriving types are all simple enough, 
but there are many similar variants that are hard to work with. Since reduction preserves typing, the main goal is to show the expressive power of the system. 

First, we can derive the usual typings for $S$ and $K$ in that, for all types $U,V$ and $W$ we can derive 

$S : (U\to V\to W) \to (U\to V) \to U\to W$

$K: U\to V\to U$. 

Second, every program (normal form) is typed by its program type. For example, the identity function $SKK$ has program type $S_2 K_0 K_0$. 
The identity function also has type $T\to T$ for every type $T$. The program type will be principal

namely

$possibilities finding the right make it easier to convenient 
develop the type theory using such that the function application has type $V$. $T$ is a subtype of subtyping is hard to infer. . For example, the identity function $SKK$ 
