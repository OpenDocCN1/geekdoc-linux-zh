# Introduction to Graphs

# 9.1 GRAPHS AND PICTURES

As we remarked in Chapter 1, graphs (which comprise points—usually called $vertices$—some pairs of which are joined by arcs—usually called $edges$) occur in many practical situations, for example, in representing, constructing, and improving on road, rail, electrical, and oil-pipeline networks and in scheduling problems, to name but a few. In some situations (for example, in one-way streets on a road map) a $direction$ may also be indicated; in the theory of $directed$ graphs, also called digraphs, some, maybe all, edges have an associated direction—indicated by an arrow. (In that case there could well be an edge from vertex $a$ to vertex $b$ and a distinct edge from $b$ to $a$.) We shall, however, have no occasion to consider digraphs in this book.

Graphs also feature in recreational problems, as Problems 9A and 9B from Chapter 1 indicate. We discuss the $bridges$ of $K\ddot{o}nigsberg$ in Section 9.6 and the $utilities$ problem in Section 9.5. The $four-color$ $Problem$ is discussed in Section 9.8.

Labeling vertices with letters or numbers, which is just another form of “coloring” them, is also employed in the determination of the number of different $isomers$ of various chemical compounds, as we shall see in the next chapter.

While it is more natural, convenient, instructive, and entertaining to study graphs by using pictures, these pictures should be regarded as only informal representations. Pictures can give rise to ambiguities, even to false assumptions, since it is not always obvious to the eye that different pictures represent the same graph. Indeed, we have not yet even made precise what we mean by this. Roughly speaking, we mean that the two pictures show that the vertices are joined by edges in the same way. We make this more precise when we give the definition of an $isomorphism$ between graphs in Section 9.3.

It turns out that the pictures in Figure 9.1 all represent the same graph called the $Petersen$ $graph,^{a}$ as we (and you!) will confirm in Exercise 9.3.1B. The vertices are labeled for later convenience.

a This graph is named after Julius Peter Christian Petersen (born June 16, 1839, died August 5, 1910). He did not introduce the graph merely because it looks so pretty. Indeed it was invented to show that several plausible conjectures about certain types of graphs were actually false. Furthermore Alfred Bray Kempe seems to have beaten Petersen to it. He studied the same graph in 1886. There is more information about Kempe in a footnote in Section 9.8.