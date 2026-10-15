
## The Algorithm

Let’s separate out the algorithm behind RIP-1 from the protocol itself for a moment. RIP-1 uses a distance vector algorithm to determine where to send packets, and a number of newer routing protocols have followed suit. To be specific, RIP-1 uses the Bellman-Ford algorithm to make its computations. This algorithm begins with the source location, which is a single point when we ignore the routing aspect. It assigns the distance from the source point to itself as zero. The distance to all other points is assumed to be infinite.

The major assumption applied is that there is at least one way to get from any point in the system to the source point; no points are completely isolated from the source. Furthermore, the path to the source point ends when it reaches the source point. It does not travel through it, around some more, and then back. It also cannot travel the same path twice.

The goal of this algorithm is to find the shortest total travel distance from any single point to the source point. Bellman-Ford works in iterations. To start, take a look at the graph points in Figure 1.5 (you should recognize these from Figure 1.4).

![](img/5f0cc5444dfa57f5c5cc6a7830396eaa_28_0.png)

Figure 1.5 Graph points for Bellman-Ford algorithm demonstration.

The algorithm maps the path from the remote points to the source points for each iteration using a specific number of jumps and the distance for each jump. Iteration one results in Figure 1.6.

![](img/5f0cc5444dfa57f5c5cc6a7830396eaa_29_0.png)

### Figure 1.6 First Bellman-Ford iteration for the specified graph.

The moment you get past just one jump, you have to start looking for more than just the correct number of iterations. In each case, the total distance must be as short as possible from the destination point to the source point. As you get into two jumps (Figure 1.7), three jumps (Figure 1.8), and more, you refine the determination of what exactly is the fastest way to get from any point to the source point.

![](img/5f0cc5444dfa57f5c5cc6a7830396eaa_29_1.png)

### Figure 1.7 Second Bellman-Ford iteration for the specified graph.

![](img/5f0cc5444dfa57f5c5cc6a7830396eaa_30_0.png)

### Figure 1.8 Third Bellman-Ford iteration for the specified graph.

Examine these first three iterations only for now. Table 1.2 outlines the total distance it takes to get from each point to the source per iteration, using the point labels shown in Figure 1.5.

### Table 1.2 Breakdown of Travel Distances for Three Bellman-Ford Iterations

| Point | Iteration 1 (m) | Iteration 2 (m) | Iteration 3 (m) |
|---|---|---|---|
| Ag | 21 | 95 | 147.5 |
| Eng | 59 | 56.5 | 147.5 |
| Phys | 108 | 106.5 | 106.5 |
| Hum | 134 | 133.5 | 137.5 |
| Arts | 74 | 87 | 97.5 |
| Chem | 112 | 106 | 146 |
| Math | 55 | 108.5 | 121.5 |

Notice the wildly varying results in this table. In some cases, the shortest distance is one jump. In others, it's two. None in this example benefit from three iterations, although Phys comes close. This is not always the case, however. It really depends on the spread of the points. Completing the example would require four more iterations, a total of seven, just as there are seven points not counting the source point.

Of course, RIP-1 uses this algorithm from the perspective of TCP/IP routing. When you are trying to find the fastest way to get from “here” to “there” from a routing point of view, distance is not the only factor to consider. Another important issue is that of how long it takes the data to travel from connection to connection. The shortest physical distance is not always the fastest route.

Rather than referring to a purely physical distance between points A and B, the distance in RIP-1 is a weight value defining how long it will take information to travel if it jumps between the two points in question. Originally, all distances were listed as one. This is meant as a hop count—with each router the data must pass through being one “hop.” Distances used today are more varied, with the number being slightly higher for cases where data has to travel along a very slow connection to get to the next point or other reasons that might cause delays.

Let’s return to Figure 1.8 from the example network and the data in Table 1.1. The first thing you might do is go through this table and assign the distance or cost of traveling between each of the points. One example of what you might end up with is shown in Figure 1.9.

![](img/5f0cc5444dfa57f5c5cc6a7830396eaa_31_0.png)

### Figure 1.9 RIP-1 speed factors applied to the example network.

There are two things to notice here. First, there is not a path from every point to every point as there would be in the raw Bellman-Ford algorithm. The only valid paths are the ones where there are physical connections in place. Second, notice that distances are not assigned exactly according to speed. Anything at least the speed of a T1 line received a one, and from there down the costs increased. A number of approaches can be taken when assigning distances. This is just one of them.
