
## Chapter Six
### Conclusions

In this book we have explored the potential of neural networks to model behavior. The results suggest that neural networks can model behavior systems in all their parts, reproducing a wide range of behavioral phenomena. Figure 6.1 provides a summarizing sketch of a simple but complete model of an animal's behavior mechanism. The model includes reception and further processing of sensory input, central mechanisms of decision making and the control of muscles and other effectors. The figure shows only a few recurrent connections, but in principle connections between any nodes in the system can be included, *e.g.*, so that sensory information affects motor control directly. Additional flexibility can be gained by including nodes with different dynamics, although we have only touched upon this possibility. By putting together these components in suitable ways, virtually any behavior map can be implemented. In addition, the model may include networks able to convey feedback signals from the environment ("reinforcement") that can be used to modify the behavior map (i.e., learn) through weight changes (Chapter 4).

In this last chapter we make an assessment of neural networks as models of behavior and compare them with other modeling approaches, in particular, cognitive models. We recall that our aim is to understand behavior, and we use neural networks because we think that they can provide better models of behavior. Of course, behavior can be used to study what occurs inside animals, but this is not our principal aim. See Staddon (2001) for a penetrating discussion of the different aims of behavior studies, with a focus on behaviorism.

### 6.1 ARE NEURAL NETWORKS GOOD MODELS OF BEHAVIOR?

In Chapter 1 we listed some requirements that a general model of behavior should satisfy (page 7). Below we reproduce these requirements (*in italics*), and we evaluate to what extent neural network models fulfill them. We recall that we consider animals in general, ranging from the simplest to the most complex. Our interest is in how behavior systems in general operate and how they can be elaborated during evolution. Humans have very special abilities, sometimes shared with our closest relatives (Tomasello 1999), that are outside our scope. Currently we do not have good neural network models of, say, human symbolic reasoning. This has sometimes generated strong criticism of the connectionist approach (Fodor & Pylyshyn 1988; Pinker & Prince 1988). Such critiques, however, are less relevant when we consider animals in general. Starting from humans would mean starting from a very special and complex case of behavior rather than from typical or simple behavior.

![](img/4e7230a4ecf676d308ca85f3d2e65bae_218_0.png)

Figure 6.1 A behavior mechanism modeled as a neural network connected to receptors and muscles. The model includes reception of stimuli, processing of sensory input, a central decision making mechanism and a part that controls muscles and other effectors. An example with more sophisticated decision making is in Figure 3.27 on page 106.

#### 6.1.1 Versatility

> *We observe great diversity in behavior, both between species and, on a less dramatic scale, within species. The basic structure of a general model of behavior should allow for a diversity of behavior maps to be formed.*

We have shown throughout this book that neural network models seem able to implement practically any behavior system we consider. Additionally, neural networks can integrate diverse features and subsystems within a single basic architecture, allowing unified models of fields that earlier have been treated separately (e.g., reaction to stimuli, motor control, control theory, and learning).

Formally, it has been proved that a three-layer feedforward network with sufficiently many hidden nodes can approximate to any degree of accuracy any continuous map from the input to the output space (Cybenko 1989; Funahashi 1989; Hornik et al. 1989). More generally, a recurrent network can reproduce practically any *sequence* of input-output mappings (Hytöneniemi 1996; Jin et al. 1995; Šima & Opponen 2003). These theorems guarantee that networks are general enough to encompass the diversity we observe in animal behavior, although they do not show how to build a network that implements any particular map. For this, the techniques described in Chapter 2 can be used.

#### 6.1.2 Robustness

> *Regardless what explanation we seek, the mechanisms should display some robustness; otherwise, behavior would be vulnerable to any genetic or environmental disturbance. Thus small disturbances should not cause any major changes in performance.*

Robustness is a landmark of neural networks, as demonstrated by many studies. We have discussed this issue in Section 3.9. Even rather small networks (few tens of nodes) can show graceful degradation of performance as nodes or connections are eliminated. Neural networks are robust also in the sense that small changes in input patterns usually result in small changes in network output (Section 3.3).

#### 6.1.3 Learning

> *Learning from experience is a general feature of animal behavior. The model should allow learning, which should integrate realistically with the behavior map.*

Neural network models offer a concrete interpretation of learning as changes to connection weights, corresponding to synapses in nervous systems. Finding biologically realistic learning procedures for neural networks, however, has been somewhat of a struggle (in fairness, the same is also true for other models). The essential issue is that in a plausible learning algorithm weights should change based solely on information that is in principle available at biological synapses. This may not be a major problem when the goal of learning is to organize the network based on general features of incoming input, e.g., to produce receptive fields of the Hubel-Wiesel type (Sections 2.4 and 4.7; Kohonen 2001). Neural network studies show in fact that such organization can be achieved with easily available information such as the activity of the pre- and postsynaptic nodes. However, learning about definite input-output relationships (e.g., classical and instrumental conditioning) also needs feedback from the animal's behavior and its consequences. In early algorithms such as back-propagation, such feedback was poorly integrated with the functioning of the network itself (Section 4.2). So-called reinforcement learning (Sections 2.3.4 and 4.2) represents a more biologically plausible alternative and can be materialized within the network. Recently, other promising algorithms have appeared (Section 4.2.2).

#### 6.1.4 Ontogeny

> *The behavior system of an individual develops in a sequence of events in which genes, the developing individual and the environment interact. The structure of the model should allow for gradual development of a behavior map from scratch to an adult form.*

This is perhaps the weak point of neural network models today, not because we know that neural networks suffer from particular shortcomings but rather because of our unsatisfactory understanding of the interactions among genes, the environment and the developing individual. Nevertheless, we saw in Chapter 4 that neural networks allow us to make interesting speculations about ontogeny, and the whole process appears at least less mysterious. For instance, since neural networks allow to model learning, they demonstrate how genetic information controlling the development of the network can be integrated with environmental effects. Moreover, the ontogeny of sensory processing abilities has been illuminated by network studies on the development of receptive fields, as recalled in the preceding point.

#### 6.1.5 Evolution

> *For evolution to occur, genetic variation must exist that affects the development of behavior mechanisms. In a model, it should be possible to specify how genes control features of behavior maps and learning mechanisms. In addition, a model should allow the evolution of nervous systems from very simple forms to the complexities seen in, e.g., birds and mammals.*

Realistic studies of the evolution of genetically controlled features of nervous systems suffer from the same lack of knowledge just discussed for ontogeny. However, the requirement that complex systems can evolve from simpler ones seems overwhelmingly fulfilled. Already very small networks are very capable and can be improved incrementally in a variety of ways, leading from sloppy to near-perfect behavior. In addition, we have seen that neural network studies are contributing to the understanding of particular issues about the evolution of behavior (Chapter 5).

### 6.2 DO WE USE TOO SIMPLE NETWORK MODELS?

Most analyses in this book rely on simple networks operating in discrete time. Nervous systems are much more complex and operate in continuous time. Such complexities are considered often in neuroethology and neuroscience, which are based on reconstructions of nervous machinery, including the detailed description of patterns of connectivity and the dynamics of neurons and synapses. The main goal of neuroscience, however, is to understand the nervous system and not behavior. We have already stated and defended our parsimonious approach in Chapter 1. Simple models have the advantage of being easier to understand and potentially more general because they do not include details that vary between species. On the other hand, there is always the possibility that models are too simple or in other ways unrealistic. The crucial test of simple neural network models of behavior is the extent to which they capture essential features of the behavior of real animals. If they do, the fact that the model is simple and neurally inspired (rather than based on some other metaphor, such as the digital computer) should be considered bonuses rather than problems. Of course, our approach would be in trouble if nervous systems turned out to operate in a dramatically different way from the models used in this book.

### 6.3 COMPARISONS WITH OTHER MODELS

In Chapter 1 we discussed various approaches to modeling behavior. Do neural networks offer any advantages over these other approaches? And what are the disadvantages? We start with advantages. First, the neural network approach provides a material implementation of sensory reception, processing, memory, decision making and motor control that is consistent with neurobiology and can model the whole causal chain from stimulus reception to behavior. Network models also show potential for modeling behavioral ontogeny and nature-nurture issues, although these
