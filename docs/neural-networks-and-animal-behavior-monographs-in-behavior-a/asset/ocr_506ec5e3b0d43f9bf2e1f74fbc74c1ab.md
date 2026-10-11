![](bbox=[0.28, 0.12, 0.72, 0.29])

Figure 2.4 The logistic function, equation (2.7), for several choices of parameters. Note the similarity with the curves in the right part of Figure 2.2.

The node model introduced so far is summarized in Figure 2.5 and formally by

$z_{i}=f\left(\sum_{j} w_{j} z_{j}\right)$ (2.8)

Accordingly, the operation of a whole network can be expressed symbolically as $\mathbf{z}=f(\mathbf{W} \cdot \mathbf{z})$. Obviously, this model is much simpler than neurons and synapses. Yet it has proven very useful to build models of behavior and nervous systems. In neural network studies, both simpler and more complex nodes are used, depending on the precise aim of the study. Simpler nodes sometimes are used to simplify mathematical analysis. An instance is a node having only two states, “active” and “inactive” (Amit 1989; McCulloch & Pitts 1943). More complex nodes have many uses, among which is to investigate neuron physiology. For instance, Bush & Sejnowski (1991) reconstructed from photographs the branching structure of a few neurons, and Lytton & Sejnowski (1991) simulated them as complex electrical networks, accurately reproducing the observed spiking patterns. A network with such complex nodes, however, would be very difficult to build and to understand. Moreover, we are not guaranteed to get a better model of behavior simply by including more detail. We still ignore which features of neurons are crucial for nervous system operation and which are less important (Graham & Kado 2003). Thus we will start with the basic node described earlier, and add complexity only when needed to model behavioral phenomena.

# 2.1.3 More advanced nodes

This section shows how the basic node can be developed to include additional features of neurons. It can be skipped at first reading because most of our network models will use the basic node described earlier. We start by asking how to calculate node activity in response to an input $y(t)$ that varies with time. The simplest possibility is to construe time as a succession of discrete *time steps* and to compute node activity at time $t+1$ from node input at time $t$ using equation (2.8):

$z(t+1)=f(y(t))$ (2.9)