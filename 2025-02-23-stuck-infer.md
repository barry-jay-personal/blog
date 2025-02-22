# Stuck on Type Inference
## Barry Jay
### 2025-02-23

Little progress to date on type inference, but I'm going to share anyway; maybe something will shake loose. 
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
