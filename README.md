# (to be completed) GSoC 2018 project presentation
The following is an overview of my collaboration with GSoC and Sagemath on the databases/bounds of codes project.

## Summary
The parameter known as Hamming weight or minimum distance of a linear code is important from both a theoretical and an applied standpoint. A main concern of coding theorists is the search for codes with large Hamming weights under the constraint of fixing the other code parameters, usually length and dimension.
The Sagemath coding theory library provides an extensive toolkit for working with linear codes. Some of these constructions already give information about codes and their minimal distances which can be used to attack this problem. This summer I have worked with Sage developers to add more helpful algorithms of this kind to the package. These enhancements have been rebased over the latest sage version. In addition, I have described an approach to the main problem using a Codetable class that applies several relevant methods to construct optimal linear codes for many choices of length and dimension.

## Merged code

See https://github.com/filipion/Construction-of-optimal-linear-codes/tree/master/code_constructions

## Code not ready to be merged
See https://github.com/filipion/Construction-of-optimal-linear-codes/tree/master/codetables

## remarks, useful resources, challenges
