# Cantor's Second Diagonal Argument
## Barry Jay
### 2025-01-06

Can tree calculus provide a foundation for mathematics?  Since it
supports arithmetic through the Turing computable functions, 
perhaps the next step is to develop the differential and integral
calculus over the real numbers.

The real numbers themselves are easily represented as
follows. Naively, a real number between zero and one is an infinite
decimal or, in binary, an infinite sequence of bits. In turn, these
can be identified with the functions from the natural numbers to the
booleans, which can be identified with the programs, i.e. the binary
trees, as follows. Given a program $p$ then for each successive number
$0,1,2..., n, ...$ evaluate the application of $p$ to $n$ as a leaf,
stem or fork.  If a leaf, then that bit is false. If a stem or fork
then that bit is true. If the computation does not halt then this bit,
and all subsequent bits, are undefined. In this manner, standard
algorithms could be used to define all of the usual algebraic values,
such as the square root of two, the trigonometric values, such as sin
and cos and tan, and the transcendental numbers, such as $\pi$ and
$e$.  Then algorithms for computing the slopes of tangents, and areas
under curves will follow.

However, there is a mountain of work to realise these ideas (pun intended) for which I am not especially qualified.
What can I do now to get the ball rolling?

Well, there are only countably many binary trees, so there are only
countably many real numbers. On the other hand, Cantor's second
diagonal argument proves that the set of real numbers is larger than the set of natural numbers. So let's figure out what is going on.

Cantor asserts that one cannot list all of the real numbers between
zero and one. The proof is by contradiction.

- Assume that there is such a list.
- Construct a real number number $r$ whose $n$ th bit is given by flipping the $n$ th bit of the $n$ th entry in the list.
- Since $r$ is a real number, it must be in the list at, say, position $k$ but now the $k$ th bit of $r$ is both true and false.
- Contradiction!  Hence, there is no such list.

Now let us reprise the argument in tree calculus.

- There is indeed a list of all the binary trees, which lists all binary trees of depth $n$ before considering any trees of greater depth, much as in Cantor's
first diagonal argument.
- Since $r$ is a real number, it must be in the list at, say, position $k$ but now the $k$ th bit of $r$ cannot be either true or false, and so must be undefined.
- No contradiction.

The fun part is to try and compute the value of $k$ . After all, the
list of binary trees can be represented as a particular program from
the natural numbers to binary trees. Again, the program $r$ is a
particular program, so we can search the list for it, at least in
theory, but $k$ will proved to be intractably large. 

To see this, let's begin by counting the number $T(m)$ of trees whose
depth is at most $m$. If $m$ is $0$ then there exactly one tree of
this depth, namely the leaf.  If $m$ is $n+1$ then $T(n+1) = 1 + T(n) + T(n)*T(n)$ corresponding to one leaf, $T(n)$ stems and $T(n)*T(n)$
forks. This grows very quickly:

- T(0) = 1
- 𝑇(1) = 3
- T(2) = 13
- T(3) = 183
- T(4) = 33673

In fact, $T(n)$ is bigger than  $2^{2^n}$ !
Thus if $r$ has $k$ nodes then $k$ is greater than $2^{2^k}$. Since $r$ is a recursive program, we can be confident that $k$ is over one hundred, if not one thousand, so that $k$ is greater than $2^{2^{100}}$ which is incomprehensibly large! 

On consideration, there is no intensionality in this argument, so presumably it has already been made for other models of computation by listing, for example, all possible input tapes to a Universal Turing machine. Anyway, I enjoyed working things through, and preparing the ground for a more thorough development of real analysis. 
