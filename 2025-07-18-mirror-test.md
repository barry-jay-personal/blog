# The Mirror Test
## Barry Jay
### 2025-07-18

In biology, the mirror test is a test for self-awareness: can an animal recognise its own reflection in a mirror? This separates an element of consciousness from any question of general intelligence. 
Now we can apply the same test to a program, or programming language. 

A program **mirror** is  *self-aware* if **mirror mirror** is true and **mirror** p is false for any other program p. A programming language passes the mirror test if it supports a self-aware program. 

Do you know any self-aware programs? If so, let me know! Here is my solution in tree calculus. 
The heart of the matter is to have a program **equal** that decides program equality. In particular, **equal equal equal** is true, and this holds without any encodings of programs as syntax trees. 
Then it is merely a question of recursion. We will use a program constructor Q that produces fixfunctions by satisfying 

Q f x = f x (Q f)

Then tree calculus passes the mirror test by suppporting the program 

**mirror** = Q **equal** 

which is self-aware because 

**mirror** p = Q **equal** p = **equal** p **mirror** 

which decides the question. 


In recent months I have been working on typed tree calculus where the types form a combinatory calculus without quantifiers. I plan to write more on this before too long, but here is a taste. 
Corresponding to the quantified type $\forall X. X \to Bool$ is now the combinatory type **Query**[**Bool**]. 
In this setting, the type of **equal** is **Query**[**Query**[**Bool**]]. However, Q **equal** may not have a type. The solution is to replace **equal** with a variant **equal2** that has the same functional behaviour to get 

**mirror2** = Q **equal2** : **Query**[**Bool**]

which passes the mirror test and is typed as a generic query. 

