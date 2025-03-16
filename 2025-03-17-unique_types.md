# Unique Types for Combinators
## Barry Jay
### 2025-03-17

I have found a simple type system for a Turing-complete system of combinators in which every combinator has a unique type! 
Hence, there is a type inference algorithm which will find types if they exist, but may fail to terminate. 
These results are inspired by the goal of supporting type inference for tree calculus but may be of independent interest. 

Traditionally, one allows rules such as $K : U\to V \to U$ for all types $U$ and $V$ but then $K$ does not have a most general, or principal type. 
Introducing quantified types allows $K : \forall X.\forall Y. X \to Y \to X$ but these types are not simple. 
Annotating the operators to get $K^{U,V} : U\to V\to U$ gives each combinator a unique type, but now the operators have internal structure, which is against the spirit of combinatory thinking. 
Third, we could replace $K^{U,V}$ with $K U V$ in which types are also terms but this is not really simple either. 

The solution adopted here is to admit a unique type for each program (i.e. normal form) and use subtyping to convert program types to function types. 
For example, given a program of the form $Ku$ where $u:U$ then $Ku : K_1 U$. Now consider the application of this to some $v$ to get $Kuv$. 
Now $Kuv$ is a redex, not a program, so does *not* have a type of the form $K_2 UV$ (such type forms do not exist). 
Rather, $K_1 U < V \to U$ yields $Kuv : U$. More generally, the rule for typing applications is: 

if $M : T$ and $N:U$ and $T< U \to V$ then $MN : V$. 

There are various ways to develop this approach but most of them make type inference quite difficult. 
The solution adopted here is to insist that if $T< U \to V_1$ and $T< U\to V_2$ then $V_1 = V_2$ so that every term has a unique type.   
Now it is easy to prove that reduction preserves typing, and to define type inference. Less clear is that the approach is expressive enough. 
To show this, I have proved that the calculus is Turing-complete and supports lambda-abstraction. 

The terms are given by 

$$ t,u ::= x | S | K | Z | Zero | Succ | t u . $$

The types are given by 

$$ T,U,V ::= S_0 | S_1 T | S_2 U V | K_0 | K_1 T | Z_0 | Z_1 T | Nat | U \to V . $$ 

$Z$ is used to define fixpoints by the rule $Z f u \to f (Z f) u$. Since $Z$ is a binary operator, the application $Z f$ is a program if $f$ is. 
The natural numbers are inspired by the Scott encoding, and so have reduction rules $Zero\ u\ f \to u$ and $Succ\ n\ u\ f \to f\ n$. 
The subtyping rules are inspired by the need to type programs and the reduction rules. For example $Z_0 < U \to Z_1 U$ is used to type $Z f$ if $f:U$. 
Also, if $T < Z_1 T \to T_2$ and $T_2 < U\to V$ then $Z_1 T < U\to V$ is used to type fixpoints. 

The Scott encoding of natural numbers plus fixpoints is enough to show Turing-completeness. Lambda-abstraction is supported in the following sense. 
If $M:V$ in a context where $x:U$ then there is a type $T$ such that $\lambda x. M : T$ and $T< U\to V$. For example $\lambda x. x = SKK : S_2 K_0 K_0 < U\to U$. 

Since types for terms are unique, if they exist at all, type inference is easily defined. The only difficulty is that the algorithm may not terminate. For example, consider the typing of $(SII)(SII)$. 
This is a canonical example of a combinator without a normal form. In simply-typed lambda-calculus, $SII$ is equivalent to $\lambda x. xx$ which does not have a type, since $U$ is never equal to $U\to V$. 
Here $SII$ is a program of type $S_2 I_0I_0$ where $I:I_0 = S_2 K_0 K_0$. So type inference will try to find a solution $W$ for $S_2 I_0 I_0 < S_2 I_0 I_0 \to W$. 
In general, to solve $S_2 T_1 T_2 < U \to W$ is to solve $T_2 < U \to V$ for $V$ and then solve (some variant of) $T_1 < U\to V\to W$. In our particular case, the constraints reduce back to the original problem. 
The simplest solution is to impose an artifical bound on the execution time of type inference, e.g. a bound that is given by the size of the term being typed. This may be good enough in practice. 

Note that this approach will not work for pure lambda-calculus unless some combinatory thinking is introduced. First, non-trivial recursive functions do not there have normal forms, are not programs, so one would have to introduce a fixpoint operator, such as $Z$. 
Second, is the challenge of finding the principal types of programs such as $\lambda x.x$. No function type will do, so it seems that the program type $I_0$ must be supported somehow. 

Since this calculus supports a polymorphic identity function $I : I_0 < U\to U$ it is interesting to consider how much more polymorphism can be added. 
Of course, we can add data types and their constructors, so presumably all of the expressive power of the Hindley-Milner is available. But what of System F? Can we support the data types and their constructors directly? 
As for tree calculus, if there is to be only one operator the next step would be to replace the operators $Z$ and $Zero$ and $Succ$ with combinations of $S$ and $K$. This is non trivial because the combinator for Zero will have two natural types, namely its program type and Nat.
Which one should be the inferred type? Perhaps the combinator for Zero should be tagged in some way that excludes the program type. 
