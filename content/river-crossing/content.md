# River Crossing Puzzles

## Introduction

> id: intro
> section: introduction

::: column.grow
River crossing puzzles are about carrying items from one river bank to another,
usually in the fewest trips and typically with restrictions that make a solution
non-obvious. 
According to [Wikipedia](https://en.wikipedia.org/wiki/River_crossing_puzzle)
the earliest known river-crossing problems occur in the manuscript 
_Propositiones ad Acuendos Juvenes_ (English: Problems to sharpen the young),
traditionally said to be written by Alcuin. The earliest copies of this 
manuscript date from the 9th century.

We use river crossing puzzles to illustrate and introduce concepts and 
principles of algorithmic problem solving, such as state-transition diagrams,
symmetry, and the importance of avoiding unnecessary naming. 


::: column(width=250)
    img(src="images/river-crossing-1.jpg" width=250)
:::


---
## The Goat, Cabbage, and Wolf Problem

> id: goat-cabbage-wolf
> section: goat-cabbage-wolf

::: column.grow
A farmer wishes to ferry a goat, a cabbage and a wolf across a river.  However,
his boat is only large enough to take one of them at a time, making several 
trips across the river
necessary.  Also, the goat should not be left alone
with the cabbage (otherwise, the goat  would eat the cabbage), 
and the wolf should not be left alone
with the goat (otherwise, the wolf  would eat the goat).  

How can the farmer achieve the task?
::: column(width=260)

    img(src="images/Vovk_koza_kapusta.png" width=260)

:::



### Introduction
Before we proceed, it is important that we understand clearly the problem
statement. Usually, with puzzles, there is a substantial amount of implicit
information in the problem statement that needs to be made explicit. 
For example, initially, [[all the four elements are at the same river 
bank | there are two elements on each river bank]].
Also, [[farmer | goat | cabbage | wolf]] has to accompany each of the other 
elements when crossing the river. 

Note that we adopt what [E. W. Dijkstra](bio:ewdijkstra) called the rule of 
_no  cancellation_, i.e. we reject any schedule in which a subsequence of 
successive moves results in no change.

#### Why is this an algorithmic puzzle?
This is an algorithmic problem because [[its solution consists of 
an algorithm|the farmer is a computer scientist|all puzzles are algorithmic 
problems]]. _{span.reveal(when="blank-2")} In other words, a solution to this puzzle consists of a sequence of instructions. A typical instruction would  be: 
"the farmer  crosses with the wolf" or "the farmer returns alone"._



---
> id: states
### Notations and states
In order to solve the problem, we need a way to represent the position of each
element. We will name one of the river banks as _left bank_ and the other one
as _right bank_. We assume that initially all elements are in the left bank.

We use the letter *L* to denote that an element is in the left
bank and the letter *R* to denote that an element is in the right bank.
For example, we write *LLRR* to denote that the farmer is in the left bank, 
the goat is in the left bank, the cabbage is in the right bank, and the wolf 
is in the right bank (exactly by that order). 
Each of these four-letter representations is called a _state_.

Using this notation, we have the following cases:

 - To represent that the farmer is in the 
   left
   bank, the goat is in the 
   left
   bank, the cabbage is in the
   left
   bank, and the wolf is in the
   right
   bank, we write [[LLLR | LRLR | RLRL]]

 - To represent that the farmer is in the 
   left
   bank, the goat is in the 
   right
   bank, the cabbage is in the
   left
   bank, and the wolf is in the
   right
   bank, we write [[LRLR | LLLL | RLRL]]

 - To represent the initial state, we write [[LLLL | RRRR | LLLR | RLLL ]]

 - To represent the final state, we write [[RRRR | LLLL | LLLR | RLLL ]]


#### How many states are there?
The _state space_ of a problem (or system) is the set of all possible
states (i.e. configurations) that the problem (or system) can have.
This information is important because it can give us a better idea of the
complexity of the problem.

In this case, since we only have 4 elements (the farmer, the goat, the cabbage,
and the wolf), we conclude that there is a total of [[16 | 10 | 8 | 64 ]]
states. _{span.reveal(when="blank-4")}Indeed, since we have 4 elements and each
element can be in one of two positions (either *L* or *R*), the total number
of states is `2 * 2 * 2 * 2` (i.e. `2^4 = 16`)._

The number of states grows [[exponentially|linearly]].
_{span.reveal(when="blank-5")}This means that it grows very quickly! The total 
number of states is `2^n`, where `n` is the number of elements. 
To see how quickly it grows, note that for 
${a}{a|4|0,20,1} elements the total number of states is ${2**a} (change
the number of elements by sliding over it)_.


Note that not all states are valid, in the sense that some violate the
constraints of the problem. For example, the state *LRLR* is invalid
because [[the goat is alone with the wolf | the cabbage is alone with the 
goat]].

---
> id: puzzlejs
### State-transition diagrams
Now that we understand in much more detail the problem, let us try
to find a solution! To use the animation below, you just need to
select the elements that you want to move. 
We suggest that you keep reading only after you found a solution.

    .puzzle-scripts
    script(src='/resources/river-crossing/bridge/js/aux.js')
    script(src='/resources/river-crossing/bridge/js/Passenger.js')
    script(src='/resources/river-crossing/bridge/js/Boat.js')
    script(src='/resources/river-crossing/bridge/js/main.js')
    

    .boat-puzzle

For the first step, there is only one possibility: the farmer has to take
the [[goat | cabbage | wolf]] to the other side. Using the notation 
introduced before, the only possibility is to move from the initial 
state *LLLL* to the state *RRLL*. Such a move is called a _state transition_.

---
Given that the total number of states is not large, one way of solving
this puzzle is to systematically try all the possible state transitions.
We can represent this in a _state-transition diagram_:

    img(src="images/state-transition-diagram.png" 
    alt="State-transition diagram")

This state transition diagram shows that there are [[two || three]] 
different solutions. In the third step, when the goat is in the right
bank and all the other elements are on the left bank, the farmer can 
either carry the wolf or the cabbage. _Try this using the interactive
animation above!_

---
> id: naming

### On avoiding unnecessary naming

To be written.


### Acknowledgements
The material above is heavily influenced by Roland Backhouse's book
[Algorithmic Problem
Solving](https://books.google.pt/books/about/Algorithmic_Problem_Solving.html?id=84VZLWMnKrQC&printsec=frontcover&source=kp_read_button&redir_esc=y#v=onepage&q&f=false).

The interactive puzzle was written by [Victor
Ribeiro](https://github.com/victorqribeiro/bridge).
