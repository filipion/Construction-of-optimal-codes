# (to be completed) GSoC 2018 project presentation
The following is an overview of my collaboration with GSoC and Sagemath on the databases/bounds of codes project.

# Summary
The parameter known as Hamming weight or minimum distance of a linear code is important from both a theoretical and an applied standpoint. A main concern of coding theorists is the search for codes with large Hamming weights under the constraint of fixing the other code parameters, usually length and dimension.

The Sagemath coding theory library provides an extensive toolkit for working with linear codes. Some of these constructions already give information about codes and their minimal distances which can be used to attack this problem. This summer I have worked with Sage developers to add more helpful algorithms of this kind to the package. These enhancements have been rebased over the latest sage version. In addition, I have described an approach to the main problem using a Codetable class that applies several relevant methods to construct optimal linear codes for many choices of length and dimension.

# Merged code
Before attacking the main problem I decided to focus on smaller enhancements. These modifications have been rebased over the developer's latest work. My additions have focused on the two files that you can find at https://github.com/filipion/Construction-of-optimal-linear-codes/tree/master/code_constructions: linear_code.py and goppa_code.py

# linear_code.py
This is a modified version of the Sage source file with the same name in src/sage/coding. The latest commit shows 4 added methods for the AbstractLinearCode class: juxtaposition, u_u_plus_v_construction, product_code and construction_x. I have added these because they all give good constraints on the minimum distance of codes made using them. My Codetables implementation currently depends on the first two of these methods.

With the exception of these four methods the rest of the code in linear_code.py was already present in sage and represents the work of other developers.

# goppa_code.py
This implements a class for Goppa codes, a particular class of linear codes. They are present on the Sagemath future roadmap for coding theory.
Moreover, some best Hamming weight known codes are Goppa codes (e.g. [55,19]). It inherits from the class for AbstractLinearCodes in sage/coding. The Sage notebook does not see it automatically so you need to use python's import to test this code.


# Code not yet ready to be merged
See https://github.com/filipion/Construction-of-optimal-linear-codes/tree/master/codetables

## remarks, useful resources, challenges
