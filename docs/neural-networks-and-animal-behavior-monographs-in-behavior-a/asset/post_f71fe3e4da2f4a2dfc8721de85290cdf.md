
...cisions rules. There are several ways to do this. One option is to use optimization theory to find neural networks that maximize fitness. We are not aware of any studies using this approach to study evolution. Alternatively, one could try to find solutions by an evolutionary simulation (see below) or some other dynamic approach. The two options may not always yield the same result. The former can locate optimal network strategies (given we can solve the optimization problem, of course), whereas the latter is sensitive to, for instance, the initial choice of network architecture, basins of attraction and local fitness maxima (Futuyma 1998). Similar options are available for frequency-dependent selection. We could use standard evolutionary game theory and search for ESS networks, but no one has done this as far as we know. The other option is simulations of evolution, which in addition to evolutionarily stable behavior may also describe behavior that emerges in scenarios with continuous change and without any stability (see below). So what insight could be gained from such analyses? We have seen in this and earlier chapters that basic features of neural network operation entail a number of biases and constraints that potentially can influence evolution. Similar biases are likely to exist in animals, and this is a cornerstone of studies of the evolution of behavior based on neural networks. Let us consider a few examples.

Neural networks show clearly that some input-output maps are more difficult (or impossible) to realize. Even when a map potentially can be implemented, biases in the behavior mechanism can still influence the direction of evolution. One example is offered by Holmgren and Getz (2000), who studied the evolution of host plant preferences in insects. The animals' recognition system was modeled with a three-layer neural network, and an evolutionary simulation was set up in which the networks had to select, by means of sensory cues, those host plants that offered better nutrition to larvae. Although many host plants had the same quality, the networks often evolved to recognize only one kind of plant. This study suggests that specialist strategies are more common because they are more easily formed by nervous systems and therefore may evolve more easily than generalist strategies.

Neural network models generalize spontaneously, responding with similar behavior to similar stimuli (Section 3.3). Generalization may also be important in many evolutionary problems; e.g., problems involving high-dimensional stimuli such as visual stimuli that are received via many receptors. Biases in behavior systems may have additional consequences for the evolution of social interactions. In this case, natural selection favors strategies that are sensitive to the behavior (or physiology or biochemistry) of others, allowing the individual to respond based on more information. However, if there are evolutionary conflicts of interests between individuals, selection would also favor social strategies that can exploit others, e.g., by taking advantage of biases in behavior mechanisms. This has consequences for the evolution of both manipulative strategies and signal form (see examples below).

Neural networks may also provide insight into how learning may affect the evolution of behavior. To analyze such problems, one may use neural networks as more realistic models of learning and memory (Chapter 4). An example is Kamo's study of how learning influences the evolution of signal form (Kamo et al. 2002). His results suggest that signals will be most exaggerated and costly when receivers learn to recognize them and when each receiver meets the signal only a few times. If learning occasions are many or recognition of the signal is genetically inherited, less costly and less exaggerated signals evolve.

Another use of neural networks could be to study directly the evolution of the behavior system, letting features of the network evolve more freely as discussed in Section 5.3.2. This could provide insight about the evolution of both behavior and the functional structure of the nervous system. For instance, one could try to understand how mechanisms (i.e., substrates) for sensory preprocessing, learning, regulatory states and decision making evolve. Simulation results could be compared with the growing literature on the neurobiology of behavior.

### 5.4.3 Simulation techniques

How can we study behavioral evolution with neural network models? Sections 2.3.3 and 2.5 provide a brief technical introduction and some examples. Most simulations are built around the following core steps:

- 1. Create an initial population of networks.
- 2. Calculate the fitness of all networks.
- 3. Based on fitness, decide which networks “reproduce” and how much.
- 4. Mutate some networks.
- 5. If a stop criterion is fulfilled, end; otherwise, go to step 2.

(We refer only to “networks,” but other traits such as morphology can be included.)

In addition to this general procedure, a number of details have to be decided before a real simulation can be carried out. One is how mutants should be produced; i.e., what variables can mutate, and how exactly do they mutate? Other relevant details are the size of populations and the mode of reproduction. The simplest choice is a population size of two and asexual reproduction. The general procedure then takes the following form:

- 1. Select an initial network (network 1).
- 2. Calculate the fitness of network 1.
- 3. Make a copy of network 1, called network 2.
- 4. Mutate network 2.
- 5. Calculate the fitness of network 2.
- 6. Compare the fitness of networks 1 and 2.
- 7. Retain the fitter network and label it network 1.
- 8. If a stop criterion is fulfilled, end; otherwise, go to step 2.

This simple algorithm can be developed along several lines to suit specific problems. One obvious extension is to use a larger network population. Using a population introduces a natural range of variability that is particularly important when simulating evolutionary games (frequency-dependent selection). In a population, mutations with higher fitness enter slowly, and adaptation to the social environment may require confronting a range of different phenotypes. It is also possible to consider sexual reproduction by defining how offspring networks are created from parent networks. The latter is not trivial because, as discussed in Section 5.3, we do not fully understand how genes code for nervous systems. Lastly, we may include individual and social learning in evolutionary simulations. This requires us to calculate fitness based on how the network behaves during a simulated life in which it can learn (e.g., Kamo et al. 2002).

### 5.4.4 Example 1: Coevolution between signal senders and receivers

This example describes how sender-receiver coevolution can be investigated with neural network models and also illustrates some of the general points discussed earlier regarding the interplay between behavior mechanisms and evolution.

An important feature of social evolution is evolutionary conflicts of interest. Such a conflict exists when the expected reproduction or fitness of one individual could increase at the expense of other individuals (Enquist et al. 2002; Parker 1979). For instance, a potential prey would benefit from the predator not attacking, a contestant from the opponent giving up or a busy female from males stopping courting her. These evolutionary conflicts may appear at first as just of theoretical interest because it is difficult to imagine how an individual can influence what others decide to do. However, many examples of successful manipulation of others' actions are known in nature. Larvae of the blue butterfly are a spectacular example, being able to persuade ants to carry them to the ant nest, where they feed on ant larvae and pupae (Hölldöbler & Wilson 1990).

How can manipulation evolve and persist? To get some insight into this problem, we will consider a simple case of evolutionary conflict called the *game of presence* (Enquist et al. 2002). We first present this game and then analyze it with both standard game theory and simulated evolution of neural networks. There are two players, an actor and a reactor. The actor is either present ($v = 1$) or absent ($v = 0$) but has no choice of actions. The reactor, based on whether or not the actor is present, decides on an effort $x$ ($x > 0$). This structure is depicted in Figure 5.6. In the presence of the actor, the reactor's payoff is first increasing and then decreasing with $x$. The payoff to the actor of the reactor's effort is ever-increasing with $x$. In the absence of the actor, providing an effort $x > 0$ returns a negative payoff to the reactor. A simple formalization of this game is as follows:

$$
\begin{aligned}
F_{A}(x) = x \\
F_{R}(x) = \begin{cases} x - x^2 & v = 1 \\ -x^2 & v = 0 \end{cases} \quad (5.2)
\end{aligned}
$$

where $F_{A}$ is the payoff (fitness) to the actor, and $F_{R}$ is the payoff to the reactor. Note the conflict between the two players concerning the amount of effort $x$ to be made by the reactor. Similar conflicts are widespread. For example, in sexual conflicts (Arnqvist & Rowe 2002; Gavrillets et al. 2001), a female (reactor) must trade off current investment in reproduction with future investment, whereas a male (actor) wants the female to invest maximally in the current reproduction (Chapman & Partridge 1996; Rice 1996). We will now present three theoretical analyses of this game given different assumptions about what strategies are available to actors and reactors.
