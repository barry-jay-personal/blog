# It's Too Soon to Tell
## Barry Jay
### 2025-01-17

Some years ago, while dating another scholar, she introduced me to her mentor, who also happened to be a big cheese at my uni, one of the hyphenated. 
So, in the way of fathers everywhere, he asked me about my prospects, my research, which I explained as best I could to a scholar of culture. 
He then asked me why my work mattered, so I generalised some more, "But why does that matter?" came the reply. 
After a couple more rounds of this, I found myself aiming to streamline all computing, to which he replied "So what?" 
Frustrated, but determined not to back down, I answered "This changes everything!"

There was a pause, our eyes locked, then he answered "You're quite arrogant, aren't you." 

Well, that burst my bubble. Going home I was so angry, which is unusual, but it happens when I don't know who is at fault. 
Was it his for goading me, my boss's boss's boss, or was I making ridiculous claims?
I think of myself as a numbers guy, but words are also tools of trade, so I looked up "arrogant" in the dictionary, which was then a big fat book. 
Did I have "an unwarranted belief in my own abilities"? Slamming the book shut, I yelled "It's too soon to tell!" 

That was a few years ago, and it's still too soon to tell, but I'd like to share my current thoughts on how tree calculus might change everything. 
Now is a good time, since I'm about to jump in a plane to Denver, to attend POPL and present at PEPM, my first long-haul flight since before COVID. 
And long flights are a good time to think higher thoughts. So here goes. 

Tree calculus supports both the extensional computation that is central to functional programming, and the intensional computation that is central to program analysis. 
This heals many of the splits in our current thinking about computing, between: 

- function-oriented, data-oriented and object-oriented programming
- static analysis and dynamic analysis
- terms and types
- syntax and semantics
- high-level languages and low-level languages 
- correctness and efficiency 

Wait up, I'm being that guy again. Let's try again but this time expressed as a plan. 

Let's build a strongly-typed programming language based on tree calculus that supports 
- higher-order functions
- database queries
- generalised algebraic data types
- dependent types, suitable for theorem-proving, etc
- dynamic program analysis, including execution time estimates
- memory management
- efficient, high-level array operations, suitable for machine learning

The calculus already supports higher-order functions and generic queries for, say filtering. 
Database queries can be viewed as generic queries that work with named fields. 
In theory, this is just tagging, which has been done, but row-polymorphism (more subtyping!) has not been addressed yet. 
More generally, there is the challenge of object-orientation, which I touched on in my first book, *Pattern Calculus*. 

Generic accounts of mapping and folding require a uniform account of algebraic data types and their constructors. 
Again, this should be done by tagging each constructor with its name (fields again!) and information about the types of its arguments. 
For example, the list constructors Cons should be tagged by the string "Cons" and the information that its 
first argument is data (the head) and its second argument is structured data (the tail). 

Although terms and types share many features, they are usually considered separately. From my point of view, this is because type analysis is intensional, which traditional terms cannot support.   For example, to apply a function of type $A\to B$ to an argument of type $C$ one must decide if $A$ and $C$ are equal (or unifiable) but this question is intensional. 
Nevertheless, types and terms become mixed when polymorphic terms are applied to types, or when an array type is tagged by a term for its length. Such dependent types are hard to work with since their equality now depends on that of terms, which is not decidable, leading to spiralling layers of meta-theoretic equivalence. 
Here, since the term language is intensional, we can collapse the hierarchy, and represent types as terms, so that the typed language is represented within an untyped substrate.
Then theorem-proving, which is so well represented in dependent types, could be performed dynamically. 

Since the size of values can be computed, the calculus already has the ingredients required for complexity theory, which could be performed statically or dynamically. Again, no details have been worked out. 

The memory hierarchy of stacks, caches, and heaps can all be represented as paths through trees that have dependent types, so let us do this within the core language. 

Operations on large arrays must be done in parallel, but the appropriate division depends on their size (or more generally, the problem shape), the hardware (including its shape), and the complexity of the low-level operations to be performed. 
Since all of this intensional information can be supported, there is no barrier to redeveloping all the existing meta-theory on co-ordination within the core language.

WELL, if this all works out then it will streamline computing. Further, if a single language supports machine-learning and theorem-proving then it will change everything.  Am I arrogant? 
Only time will tell!  But I promise that if you join me you will have fun. If you are at POPL, I'd love to chat.

