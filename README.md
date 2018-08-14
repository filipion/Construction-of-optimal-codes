# GSoC 2018 project presentation
The following is an overview of my collaboration with GSoC and Sagemath on the databases/bounds of codes project.

# Summary
The parameter known as Hamming weight or minimum distance of a linear code is important from both a theoretical and an applied standpoint. A main concern of coding theorists is the search for codes with large Hamming weights under the constraint of fixing the other code parameters, usually length and dimension.

The Sagemath coding theory library provides an extensive toolkit for working with linear codes. Some of these constructions already give information about codes and their minimal distances which can be used to attack this problem. This summer I have worked with Sage developers to add more helpful algorithms of this kind to the package. These enhancements have been rebased over the latest sage version. In addition, I have described an approach to the main problem using a Codetable class that applies several relevant methods to construct optimal linear codes for many choices of length and dimension.


# Merged code
Before attacking the main problem I decided to focus on smaller enhancements. These modifications have been rebased over the developer's latest work. My additions have focused on the two files, [linear_code.py](https://github.com/filipion/optimal-linear-codes/blob/master/code_constructions/linear_code.py) and [goppa_code.py](https://github.com/filipion/optimal-linear-codes/blob/master/code_constructions/goppa_code.py), that you can find in the [code constructions](https://github.com/filipion/Optimal-linear-codes/tree/master/code_constructions) directory.


## linear_code.py
This is a modified version of the Sage source file with the same name in src/sage/coding. The latest commit shows 4 added methods for the AbstractLinearCode class: juxtaposition, u_u_plus_v_construction, product_code and construction_x. I have added these because they all give good constraints on the minimum distance of codes made using them. My Codetables implementation currently depends on the first two of these methods. 

All of these methods are based on constructing a generator matrix from the matrices of some smaller components and then make use of LinearCode to construct a generic code with such a matrix. For their implementation, I just used Sagemath methods to manipulate matrices.

With the exception of these four methods the rest of the code in linear_code.py was already present in sage and represents the work of other developers.

The development of this part of the project is tied to [trac ticket 25982](https://trac.sagemath.org/ticket/25982).

## goppa_code.py
This implements a class for Goppa codes, a particular class of linear codes. They are present on the Sagemath future roadmap for coding theory. Moreover, some best Hamming weight known codes are Goppa codes (e.g. (55,19)). Goppa codes are defined by constructing a parity check matrix. The determinants of submatrices of this matrix are nonvanishing Vandermonde determinants. Because of this, the resulting codes have provably high minimum distance. If the generator polynomial has no double roots, 2 * (degree of g) + 1 is a lower bound for the Hamming weight.

The implementation of the construction algorithm is straightforward. One interesting detail is that the algorithm needed a way to represent elements of a q^^m finite field as column vectors over q, for q prime. This [trac ticket](https://trac.sagemath.org/ticket/20284#no1) from 2016 provides the method I needed to manage embedded finite fields. This file inherits from the class for AbstractLinearCodes in sage/coding. The Sage notebook does not see it automatically so python's import is needed to test this code.

The development of this part of the project is tied to [trac ticket 25977](https://trac.sagemath.org/ticket/25977).


# Codetables
In this part of the project I have tried to use Sage's expanded toolset to find good constructions for linear codes. The purpose was to approach results similar to the ones obtained at this online [database](www.codetables.de). Further explanation and proof of concept code can be found in the directory [here](https://github.com/filipion/Optimal-linear-codes/tree/master/codetables).

This version is my current best attempt at the problem introduced in the summary. It appears to me that codetables.de generally uses constructions based on well informed choices of generator matrices for linear codes, generator polynomials for cyclic/quasi-cyclic codes. I do not fully understand how the examples that beat my approach are found, however, I do not think they are based on a general algorithm. My mentor suggested that a method based on large sacle memorization works if the problem depends on various ad-hoc cases. This is the approach I have taken here.

### Implementation details
The codetable class has several dictionaries that memorize lower bounds and constructions for each value of length and dimension, similarly to how they are stored in the tables at the online database. You can give any codes you have constructed on your own as input. The codetable then suggests derived constructions based on the input and updates lower bounds adequately. I have organized the constructions in two stages, based on their increasing complexity (of course your own input code construcions can be as complicated as you wish):

1. First stage:
   These are trivial constructions. Generally they allow a code to be applied in more cases but give up some efficiency. My class doesn't perform these transformations on actual codes, at this stage only a human readable recipe is given. The user can find support for all these constructions in the Sage library. At this stage I have taken into account:
  * shortenings
  * punctured(or truncated) codes
  * lenghtened codes
  
2. Second stage:
   These are still simple but somewhat more involved constructions. They perform combinations of two codes. The instructions file suggests a how to use the class methods to build up good codes from simpler examples. Currently supported by the codetable class are:
  * juxtapositions
  * Plotkin sums (or (u/u+v) constructions)

When checking this out please make sure to also read [instructions.py](https://github.com/filipion/optimal-linear-codes/blob/master/codetables/instructions.py), for explanations and examples of how to use the code.

# Remarks, challenges, useful resources and acknowledgements
I have tested the codetable class in the case of binary codes with length smaller than 128. The distances I obtain are usually smaller than the best known (by about 15 at most. This increases with the length of the codes considered). Strangely, the performance is much better on odd numbers than even numbers. 


In the future the natural next step would be to add:

* extended codes

* construction_x with BCH codes

* concatenated codes (not yet in sage)


Here are the resources I have found most useful:

Helpful links:

* For the database of codes that I have compared my solutions against see [http://codetables.de/](http://codetables.de/)

* For an illustration of how some of the constructions I have implemented work towards the goal of the project see the lecture notes at [http://www.math.nus.edu.sg/~urops/Projects/BinaryCodes.pdf](http://www.math.nus.edu.sg/~urops/Projects/BinaryCodes.pdf)

* This roadmap has provided me with guidance on what problems to approach [https://wiki.sagemath.org/Coding_Theory](https://wiki.sagemath.org/Coding_Theory)

* Introduction to Coding Theory by Van Lint and the online notes at [http://www.win.tue.nl/~ruudp/lectures.html](http://www.win.tue.nl/~ruudp/lectures.html) have proved to me very useful on the theoretical front.


I would like to thank my mentor Dmitrii Pasechnik, Sagemath developers, the authors of the resources above and Google Summer of Code for the many ways they have helped me with this project.


