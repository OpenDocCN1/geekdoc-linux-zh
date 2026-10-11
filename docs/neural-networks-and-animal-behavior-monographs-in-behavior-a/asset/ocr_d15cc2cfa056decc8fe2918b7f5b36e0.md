![](bbox=[0.28, 0.13, 0.73, 0.31])

Figure 2.3 Responses of dark-adapted photoreceptors to a flash of light of 500 ms. Left: A cranefly (Tipula) photoreceptor approaches a steady-state activity rather slowly (activity is expressed as proportion of peak activity). Right: A fleshly (Sarcophaga) photoreceptor reacts with a fast activity peak followed by lower steady-state activity (activity is expressed as proportion of maximum activity). Data from Laughlin (1981).

# 2.1.2 The basic node model

We now define mathematically network nodes and connections. Nodes in a network are indexed by integer numbers; a generic node is indicated by a lowercase letter such as $i$ or $j$. The activity of node $i$ is a (nonnegative) number written $z_{i}$. Its biological counterpart is the short-term average spiking frequency of a neuron or, for nonspiking neurons, the difference in electrical potential between the outside and inside of the neuron (see also Dayan & Abbott 2001; §1.2). The activities of all network nodes can be collected in an activity vector **z**:

```
$$\mathbf{z} = \begin{pmatrix} z_1 \\ z_2 \\ \dots \\ z_N \end{pmatrix} \tag{2.1}$$
```

where $N$ is the number of nodes. Nodes are connected to each other via weights, continuous numbers that correspond to the strength of biological synapses. The weight that connects node $j$ to node $i$ is written $W_{ij}$. To indicate compactly all weights in the network, we introduce the *weight matrix* **W**, which can be represented as an array with $N$ rows and $N$ columns:

```
$$\mathbf{W} = \begin{pmatrix} W_{11} & W_{12} & \dots & W_{1N} \\ W_{21} & W_{22} & \dots & W_{2N} \\ \dots & \dots & \dots & \dots \\ W_{N1} & W_{N2} & \dots & W_{NN} \end{pmatrix} \tag{2.2}$$
```

A first key assumption of neural network models is that node $j$ conveys to node $i$ an input equal to the product $W_{ij}z_{j}$. This models the biological fact that a presynaptic