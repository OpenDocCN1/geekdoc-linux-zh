# 48 Chapter 3 The Architecture of Communication Systems

To solve its task, a layer N, must use only the services provided by the next lower layer (N − 1). More specifically, layer N expands the properties of layer N−1 and abstracts from its weaknesses. For this purpose, the instance of layer N communicates with the instances of the same layer on other computers. This means that the functionality of the communication system is available in the top layer. In contrast to a monolithic structure, layering a communication system means a more expensive implementation, but it offers invaluable benefits such as the independent development of partial components, easy exchange of single instances, better maintainability, and higher flexibility. Figure 3–1 shows the principles of communication in a layered system.

We can deduce two central terms for layer-oriented communication models from the current section, which will be discussed in more detail in Section 3.2:

+   * Communication between two instances of the same layer on different computers is governed by predefined rules. These rules are called protocols.
* The set of functions offered by a layer N, to its higher-order layer (N + 1), is called its service. The interface through which this service is offered is called interface.

This means that an instance is the implementation of a communication protocol and the service provided within one layer on a computer. The theoretical basis of services and protocols are discussed in Section 3.2.

![](bbox=[0.176, 0.532, 0.823, 0.883])

FIGURE 3–1
Communication in layered systems.