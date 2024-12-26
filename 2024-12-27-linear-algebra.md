# Linear Algebra is Intensional
## Barry Jay
### 2024-12-25

I want to get something off my chest. For a long time, I have been
stretching our models of computation to support program analysis, so
that we can write programs that reveal all the internal structure of
other programs (or themselves!) or, if you prefer, the intensions of
the programmer. This intensional approach goes beyond the expressive
power of merely extensional models of computation, such as lambda
calculus or combinatory logic, by supporting triage. Okay, so triage
is a bit new, a bit weird, and it takes more than a glance to appreciate.
How can we relate it to more familiar things?

Till now, I've taken a two-pronged approach. One is to develop generic
queries, to provide a natural foundation for the familar database
queries. This is clear enough but the focus is on data analysis, not
program analysis, which has already been done both in practice and in
theory by [pattern calculus]().

The other is to produce toy examples of program analyses, such as
computing the size of a program, or deciding program
equality but these theoretical advances do not impress in
practice. 

However, there is another domain in which program analysis is
central to program execution, namely the linear algebra
underpinning machine learning. Let me say straight up that this is not
my field, so there will be no discussion of practicalities. Indeed,
there are no theorems to share either. It's just an
observation.

A matrix is both a function and a data structure. It is both a
function that answers queries and a data structure to be updated
during learning. To freely interleave these activities requires an
intensional programming language.  I am curious to see how easily tree
calculus can support this. Peraps the main challenge is that trees
use one-and-a-half dimensions, between the
one-dimensional numbers and the two-dimensional matrices. How might
this affect performance?