# Combinatorial Explosion
## Barry Jay
### 2025-03-30

How many different tree calculi are there? 

More precisely, let a tree calculus be a combinatory calculus with just one operator, which is ternary. How many possibilities are there? 

The original tree calculus has three rules, according to whether the first argument is a leaf, stem or fork. 
These were carefully chosen to support both the copying and deleting necessary for lambda-abstraction, and also program analysis. 
Since the rule for stems was crafted to support both copying and analysis, it is hard to understand. Perhaps a different set of three rules could achieve the same expressive power, with better clarity. 

Triage calculus has five rules. If the first argument is a leaf or stem then deleting or copying arise: if a fork then the third argument is analysed by the three rules for triage. 
These rules are easier to understand but now implementation is harder, since two arguments must be analysed. Again, perhaps there are other calculi that analyse two arguments without losing any expressive power. 

More generally still, we could analyse all three arguments! If nothing else, it might allow some shortcuts for, say, defining equality. 
However as each of its three arguments can be a leaf, stem or fork, such a calculus could have twenty-seven different reduction rules! Could we automate the search? 
Let us consider the search space. 

In general, the right-hand side of each rule will be some combination of node operators and the pattern variables of its left-hand side. 
Of course, there is no limit to the possibilities, so let us simplify the counting as follows. 
First, assume that no pattern-variable appears more than twice, and there are no more than two nodes. 
The count will be dominated by the most complex rule, where each argument is a fork, so there are six pattern-variables in play. 
Further, assume that each variable appears exactly twice, and the node operator occurs exactly twice. 
The number of possible permutations of fourteen things is 14! but this must be divided by 128 to account for repetitions. This makes 681,080,400 sequences.
Then each of these must be bracketed to show the order of applications. This number is the Catalan number of 13 which is 208,012. 
So the number of possibilities is over ten to the fourteenth power! 

Of course, most of these calculi can be rejected for being either inconsistent, or incomplete, but we cannot exclude the possibility of thousands of useful calculi hidden in the mix. 
It's like looking for intelligent life elsewhere in the galaxy. Surely, this is too much for brute force exploration but that doesn't mean we shouldn't try either. What sort of creativity is required to find them? 
