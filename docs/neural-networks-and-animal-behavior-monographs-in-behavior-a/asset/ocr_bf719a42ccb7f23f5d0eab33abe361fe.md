![](bbox=[0.3, 0.15, 0.78, 0.33])

Figure 3.30 Left: Simple recurrent network capable of delayed responding (equation 3.12). Right: Sample response to an input that is low before time step 5 and high afterwards. Dashed line: Network with randomly set weights. Continuous line: Network with properly set weights (the basic random search algorithm was used; Section 2.5.3).

female is present but rather goes through a series of behaviors that ultimately result in copulation.

The simple network in Figure 3.30 is capable of delayed response to stimuli. Formally, the network response is given by

```
$r(t + 1) = f\left(W_{1}x(t) + W_{2}r(t) - W_{3}\right)$ (3.12)
```

Note that the response at time $t$ sums to the input to jointly determine responding at time $t + 1$. The constant negative input $-W_{3}$ ensures that weak stimuli cannot elicit a strong response. The transfer function $f$ is a sigmoid function whose slope regulates how fast the system can go from a small to a large output. Figure 3.30 (right) demonstrates the abilities of this network.

An internal state that under suitable conditions accrues with time potentially has many uses. The basic mechanism just described can be included in larger networks to provide a diversity of behaviors. For instance, we can include a more capable recognition mechanism by replacing the single input node with a layer of $N$ input nodes. The resulting network is formalized as

```
$r(t + 1) = f\left(\sum_{i=1}^{N} W_{i}x_{i}(t) + W_{N+1}r(t) - W_{N+2}\right)$ (3.13)
```

This network can be more selective as to which stimuli are able to accrue in the internal state. For instance, males of a female's own species could be discriminated from males of other species.

Another interesting example is obtained considering the network in Figure 3.19. As we have seen, this network reacts to changes in input, but not to constant input. If a delay mechanism is added to the output node, the network reacts only when the input presents a series of consecutive changes. Such a mechanism could be