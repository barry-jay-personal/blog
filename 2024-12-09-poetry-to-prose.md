
# Turning Poetry into Prose
## Barry Jay
### 2024-12-09

Hi everyone! I'm going to write about tree calculus and intensional
computation and overturning the standard model of computation etc. Of
course, I've written papers and books about this stuff, have been
chipping away for almost 25 years, but the dominant reaction has been
that the work is cute, or crazy, depending on how much I attack the
Church-Turing Thesis. Along the way, I've noticed that my writing
style gets strong reactions (good and bad!). At first, I couldn't
figure out why, but now think that its because I write poetry; those
expecting prose get frustated.

To illustrate, here is a concluding slide from my upcoming talk (PEPM,
January 2025, draft paper is online).

- Encodings are patches.
- Theorems trump theses. 
- Programs are normal forms. 
- Programs are trees not numbers. 
- Tree types become function types. 
- Tricky programs are typed by hacking.

Each sentence has a very simple structure, so it should be easy,
right?  But each sentence is loaded with meaning, and provocation - is
that the right word?

To digress, this blog is going to be in prose. An editor once told me
that in prose, no sentence should require a second reading. I
extrapolate that in poetry, a second reading should enrich the
experience, open up new meanings. To avoid slipping into poetic mode,
I am not going to revise anything I write here (except for spelling
mistakes, perhaps a paragraph break). If I'm not happy with it later,
I will write a new sentence.

Let's take a look at the "verse" above.

**Encodings are patches**

This summarises the argument (or observation)
that the traditional models of computation (the standard model?)
cannot analyse their own programs, cannot analyse their own normal
forms, without encodings, e.g. from lambda-calculus to the nautral
numbers (and back). This leads to a damning criticism of the
Church-Turing Thesis. Oh! No backsies! Let us rather say that it
exposes a limitation of the Church-Turing Thesis, one that was
inconsequential in 1936 but became a real limitation once compilers
were in play. Notice how I used the work "limitation" twice there? Its
a bit ugly, isn't it, but no going back!


**Theorems trump theses**

The argument for the Church-Turing Thesis, well, the original one, was
that since all these different models compute the same numbers, and we
haven't seen anything better, maybe that is all there is. My
refutation of this conjecture (thanks, Popper) is that we also want to
do program analysis.  Now tree calculus (actually, "calculi", since
there is more than one now) support program analysis in a way that
none of the traditional models do. So the original argument is blown
out of the water. The other argument I have heard is that everything
can be implemented on a Turing machine; QED. However, these
implementations require encodings, which takes us back to the previous
point. Indeed, modern compilers have many, many layers of encoding,
all of which create friction in the machinery. My hope is that tree
calculus can eliminate many of these intermediate languages.

**Programs are normal forms**

In lambda-calculus and combinatory logic it is traditional to
represent recursive functions as fixpoints that do not (in the
interesting cases) have normal forms, and so are unstable with repect
to computation.  Thus, program analysis requires encodings to freeze
the target.  Although this is unavoidable for lambda-calculus, all
function that are representable in combinatory logic can be
represented by normal forms, so that encodings can be avoided.

**Programs are trees not number**

When programs are represented by natural numbers (tapes) then the
program structure is encoded by arithmetic properties, e.g. prime
factorisation of Goedel numbers. But we want to avoid encodings!  By
contrast, binary natural trees, (no labels) can
represent program fragments by branches. One way to see this is to
build a syntax tree, and then replace each label by a small natural
tree. So the real challenge is to express the functionality of these
trees through algebra.

So far, this is the story of my book "Reflective Programs in Tree
Calculus". The latest work "Typed Program Analysis with Encodings"
shows how to type tree calculus.

**Tree types become function types**

Since program analysis can reveal all program structure, each program
must have a unique type, a tree type, that exactly captures its
structure. However, many different programs may have the same function
type, so this is captured by subtyping. For example, the reduction rule

$\Delta \Delta y z \Longrightarrow y$

yields the subtyping rule

$Fork\ Leaf\ Y   <   Z \rightarrow Y$

**Tricky programs are typed by hacking**

Traditionally, when complex behaviour threatens to break the type
system, new syntax is introduced.  For example, when a fixpoint
combinator is represented by the self-application of some combinator
omega which doesn't have a type, the solution has been to add a new
operator $Y$ for fixpoints. Its behaviour is captured by a new reduction
rule

$Y f \Longrightarrow f (Y f)$

and its type is

$(X \rightarrow X) \rightarrow X$.

However, there is no need to hack the term language. It is enough to
hack the type system, by adding a subtyping rule for the program type
of omega.

Ps. I failed to produce a blog with GitHub pages: it wouldn't display my post; 
I corrupted the files; it wouldn't let me delete them; I made them private; 
I'm not allowed to have two blogs; 
and now I can't even see the files to make them public again. 
So I'm just making a regular repository (sigh). 
You can make pull requests or write me direct on Barry.Jay8@gmail.com
