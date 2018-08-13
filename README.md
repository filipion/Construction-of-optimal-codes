# GSoC 2018 project presentation
The following is an overview of my collaboration with GSoC and Sagemath on the databases/bounds of codes project.

# Summary
The parameter known as Hamming weight or minimum distance of a linear code is important from both a theoretical and an applied standpoint. A main concern of coding theorists is the search for codes with large Hamming weights under the constraint of fixing the other code parameters, usually length and dimension.

The Sagemath coding theory library provides an extensive toolkit for working with linear codes. Some of these constructions already give information about codes and their minimal distances which can be used to attack this problem. This summer I have worked with Sage developers to add more helpful algorithms of this kind to the package. These enhancements have been rebased over the latest sage version. In addition, I have described an approach to the main problem using a Codetable class that applies several relevant methods to construct optimal linear codes for many choices of length and dimension.


# Merged code
Before attacking the main problem I decided to focus on smaller enhancements. These modifications have been rebased over the developer's latest work. My additions have focused on the two files, linear_code.py and goppa_code.py, that you can find at 

https://github.com/filipion/optimal-linear-codes/tree/master/code_constructions


## linear_code.py
This is a modified version of the Sage source file with the same name in src/sage/coding. The latest commit shows 4 added methods for the AbstractLinearCode class: juxtaposition, u_u_plus_v_construction, product_code and construction_x. I have added these because they all give good constraints on the minimum distance of codes made using them. My Codetables implementation currently depends on the first two of these methods.

With the exception of these four methods the rest of the code in linear_code.py was already present in sage and represents the work of other developers.

## goppa_code.py
This implements a class for Goppa codes, a particular class of linear codes. They are present on the Sagemath future roadmap for coding theory.
Moreover, some best Hamming weight known codes are Goppa codes (e.g. [55,19]). It inherits from the class for AbstractLinearCodes in sage/coding. The Sage notebook does not see it automatically so python's import is needed to test this code.


# Codetables
In this part of the project I have tried to use Sage's expanded toolset to find good constructions for linear codes. The purpose was to approach results similar to the ones obtained at www.codetables.de . Explanation and proof of concept code can be found in the directory

https://github.com/filipion/optimal-linear-codes/tree/master/codetables

This version is my current best attempt at the problem introduced in the summary. It appears to me that codetables.de generally uses constructions based on well informed choices of generator matrices for linear codes, generator polynomials for cyclic/quasi-cyclic codes. I do not fully understand how the examples that beat my approach are found, however, I do not think they are based on a general algorithm. My mentor suggested that a method based on large sacle memorization works if the problem depends on various ad-hoc cases. This is the approach I have taken here.


# Remarks, challenges, useful resources and acknowledgements
I have tested the codetable class in the case of binary codes with length smaller than 128. The distances I obtain are usually smaller than the best known (by about 15 at most. This increases with the length of the codes considered). Strangely, the performance is much better on odd numbers than even numbers. 


In the future the natural next step would be to add:

-extended codes

-construction_x with BCH codes

-concatenated codes (not yet in sage)


Here are the resources I have found most useful:

Helpful links:

For the database of codes that I have compared my solutions against see
http://codetables.de/

For an illustration of how some of the constructions I have implemented work towards the goal of the project see the lecture notes at
http://www.math.nus.edu.sg/~urops/Projects/BinaryCodes.pdf

This roadmap has provided me with guidance on what problems to approach
https://wiki.sagemath.org/Coding_Theory

Introduction to Coding Theory by Van Lint and the online notes at http://www.win.tue.nl/~ruudp/lectures.html have proved to me very useful on the theoretical front.


I would like to thank my mentor, Sagemath developers, the authors of the resources above and Google Summer of Code for the many ways they have helped me with this project.


