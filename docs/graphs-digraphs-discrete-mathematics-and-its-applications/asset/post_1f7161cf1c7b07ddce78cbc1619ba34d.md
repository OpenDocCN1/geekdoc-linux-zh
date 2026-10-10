
## 16.5 Chromatic Polynomials
## 16.6 The Heawood Map-Coloring Problem
- Exercises for Chapter 16
## 17. Edge Colorings
## 17.1 The Chromatic Index of a Graph
## 17.2 Class One and Class Two Graphs
## 17.3 Tait Colorings
- Exercises for Chapter 17
## 18. Nowhere-Zero Flows, List Edge Colorings
## 18.1 Nowhere-Zero Flows
## 18.2 List Edge Colorings
## 18.3 Total Colorings
- Exercises for Chapter 18
## 19. Extremal Graph Theory
## 19.1 Turán’s Theorem
## 19.2 Extremal Subgraphs
## 19.3 Cages
- Exercises for Chapter 19
## 20. Ramsey Theory
## 20.1 Classical Ramsey Numbers
## 20.2 More General Ramsey Numbers
- Exercises for Chapter 20
## 21. The Probabilistic Method
## 21.1 The Probabilistic Method
## 21.2 Random Graphs
- Exercises for Chapter 21
## Hints and Solutions to Odd-Numbered Exercises
## References
## Supplemental References
## Index of Names
## Index of Mathematical Terms
## Index of Symbols

# Preface to the Sixth Edition

Graph theory is an area of mathematics whose origin dates back to 1736 with the solution of the famous Königsberg Bridge Problem by the eminent Swiss mathematician Leonhard Euler. During the next several decades, topics in graph theory arose primarily through recreational mathematics. The development of graph theory received a substantial boost in 1852 when the young British mathematician Francis Guthrie introduced one of the best known problems in all of mathematics: the Four Color Problem. It wasn’t until late in the 19th century, however, when graph theory became a theoretical area of mathematics through the research of the Danish mathematician Julius Petersen. Major progress in graph theory, however, didn’t occur until World War II ended. Since then, though, the subject has developed into an area with a fascinating history, numerous interesting problems and applications in many diverse fields. It is the beauty of the subject, however, that has attracted so many to this field.

The goal of this sixth edition is, as with the previous editions, to describe much of the story that is graph theory – through its concepts, its theorems, its applications and its history. The audience for the sixth edition is beginning graduate students and advanced undergraduate students. The primary prerequisite required of students using this book is a knowledge of mathematical proofs. For some topics, an elementary knowledge of linear algebra and group theory is useful. For Chapter 21, an elementary knowledge of probability is needed. Proofs of some of the results that appear in this book have not been supplied because the techniques are beyond the scope of the book or are inordinately lengthy. Nevertheless, these results have been included due to their interest and since they provide a more complete description of what is known on a particular topic.

A one-semester course in graph theory using this textbook can be designed by selecting topics of greatest interest to the instructor and students. There is more than ample material available for a two-semester sequence in graph theory. Our goal has been to prepare a book that is interesting, carefully written, student-friendly and consisting of clear proofs. The sixth edition has been divided into shorter chapters as well as more sections and subsections to make reading and locating material easier for instructors and students. The following major additions have been made to the sixth edition:

- more than 160 new exercises
- several conjectures and open problems
- many new theorems and examples
- new material on graph decompositions
- a proof of the Perfect Graph Theorem
- material on Hamiltonian extension
- a new chapter on the probabilistic method in graph theory and random graphs

At the end of the book is an index of mathematicians, an index of mathematical terms and an index of symbols. The references list research papers referred to in the book (indicating the page number(s) where the reference occurs) and some useful supplemental references. There is also a section giving hints and solutions to all odd-numbered exercises.

Over the years, there have been some changes in notation that a number of mathematicians now use. When certain notation appears to have been adopted by sufficiently many mathematicians working in graph theory so that this has become the norm, we have adhered to these changes. As with the fifth edition, the following notation is used in the sixth edition:

- a path is now expressed as $ P = (v_1, v_2, \dots, v_k) $ and a cycle as $ C = (v_1, v_2, \dots, v_k, v_1) $;
- the Cartesian product of two graphs $ G $ and $ H $ is expressed as $ G \square H $, rather than the previous $ G \times H $;
- the union of $ G $ and $ H $ is expressed by $ G + H $, rather than $ G \cup H $;
- the join of two graphs $ G $ and $ H $ is expressed as $ G \lor H $, rather than $ G + H $.

We are most grateful to Bob Ross, senior editor of CRC Press, who has been a constant source of support and assistance throughout the entire writing process.

Gary Chartrand, Linda Lesniak and Ping Zhang

# Chapter 1
# Introduction

> *The theory of graphs is one of the few fields of mathematics with a definite birth date.*

It is the subject of graph theory of course that we are about to describe. The statement above was made in 1963 by the mathematician Oystein Ore who will be encountered in Chapter 6. While graph theory was probably Ore’s major mathematical area of interest during the latter part of his career, he is also known for his work and interest in number theory (the study of integers) and the history of mathematics.

Although awareness of integers can be traced back for many centuries, geometry has an even longer history. Early geometry concerned distance, lengths, angles, areas and volumes, which were used for surveying, construction and astronomy. While geometry dealt with magnitudes, the German mathematician Gottfried Leibniz introduced another branch of geometry called the geometry of position. This branch of geometry did not deal with measurements and calculations, but rather with the determination of position and its properties. The famous mathematician Leonhard Euler said that it hadn’t been determined what kinds of problems could be studied with the aid of the geometry of position but in 1736 he believed that he had found one, which led to the origin of graph theory. It is this event to which Oystein Ore was referring in his quote above. We will visit Euler again, in Chapter 5 as well as in Chapters 10 and 11.

## 1.1 Graphs

Graphs arise in many different settings. Let’s look at three of these.

**Example 1.1** Eight students $s_1,s_2,\dots,s_8$ have been invited to a dinner. Each student knows only some of the other students. The students that each student knows are listed below.

- $s_{1}: s_{4}, s_{5}, s_{8}$
- $s_{2}: s_{3}, s_{4}, s_{6}, s_{8}$
- $s_{3}: s_{2}, s_{5}, s_{6}, s_{7}, s_{8}$
- $s_{4}: s_{1}, s_{2}, s_{5}, s_{6}, s_{7}$
- $s_{5}: s_{1}, s_{3}, s_{4}, s_{8}$
- $s_{6}: s_{2}, s_{3}, s_{4}, s_{7}$
- $s_{7}: s_{3}, s_{4}, s_{6}$
- $s_{8}: s_{1}, s_{2}, s_{3}, s_{5}$

In order to determine if these eight students can be seated at a round table where each student sits next to two students he or she knows, it is useful to represent this situation by the diagram shown in Figure 1.1. Each point or small circle in the diagram represents a student and two points are joined by a line segment if the two students know each other. This diagram is referred to as a graph.

![](img/598a6ae3fd44120830ada34717906f29_14_0.png)

Figure 1.1: The diagram in Example 1.1

A related question is whether the students could be seated at a round table so that each student sits next to two students he or she does not know.

**Example 1.2** There are six special locations in a neighborhood park. Twelve trails are to be built between certain pairs of these locations, namely all pairs of locations except $\{a_{1}, a_{2}\}, \{b_{1}, b_{2}\}, \{c_{1}, c_{2}\}$ (see Figure 1.2(a)). A trail can be straight or curved. Can this be done without any trails crossing? This situation can be represented by the diagram with six points (each point representing a location), where two points are joined by a line segment or a curve if the two points represent locations to be joined by a trail (see Figure 1.2(b)). Once again, this diagram is a graph.

**Example 1.3** A chemical company is to ship eight chemicals (denoted by $c_{1}, c_{2}, \dots, c_{8}$) to a chemistry department in a university. Because some pairs of chemicals should not be shipped in the same container, more than one container needs to be used for this shipment. Each chemical is listed below together with the chemicals that should not be placed in the same container as this chemical.

- $c_{1}: c_{2}$
- $c_{2}: c_{1}, c_{8}$
- $c_{3}: c_{5}, c_{6}, c_{7}$
- $c_{4}: c_{5}, c_{7}$
- $c_{5}: c_{3}, c_{4}, c_{8}$
- $c_{6}: c_{3}, c_{7}$
- $c_{7}: c_{3}, c_{4}, c_{6}$
- $c_{8}: c_{2}, c_{5}$

It would be useful to know the minimum number of containers needed to ship these eight chemicals. This situation can be represented by the diagram
