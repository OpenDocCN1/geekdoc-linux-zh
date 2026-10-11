growth (Roche suter et al. 1956) and also limits what can be learned. For example, a stimulus can become more potent in eliciting a response, but not less. A global signal could be used to make \( \eta \) zero or even negative, allowing weights to decrease. We are not aware of any implementation of this idea, but several modifications of equation (4.2) have been proposed in a similar spirit (see also the next section). One such development is expressed as

```
\( \Delta W = \eta zx - \gamma z^2 W \)
```

where \( \gamma \) is a positive constant (Oja 1982). The first part of this equation is the same as equation (4.2). The second part limits the increase of \( W \) because it subtracts an increasing amount as \( W \) gets larger. The multiplication by \( z^2 \) has further interesting effects, detailed in Oja (1982) or Dayan and Abbott (2001). In short, equation (4.3) results in a weight vector that matches the "principal component" of the input patterns, i.e., the dimension of the input space along which the input patterns show larger variation. Thus Oja's work is one example of how simple update rules can produce weights that capture statistical features of the input patterns. This has been linked to the ontogeny of receptive fields in nervous systems (Section 4.7). Equation (4.3) is also an example of how additional local factors (here the value of the connection) may enter an update rule. In Section 2.4 we have seen another Hebbike rule of the form

```
\( \Delta W = \eta (x - a)(z - b) \)
```

The addition of the parameters \( a \) and \( b \) means that \( W \) can decrease as well as increase (Linsker 1986). A simple assumption is that \( a \) and \( b \) are constants. This can lead to the development of receptive fields of the kind shown in Figure 2.15 on page 59. Further possibilities are gained if \( a \) and \( b \) are made to depend on past activities (see, e.g., Dayan and Abbott 2001).

We refer to Shouval and Perrone (1995), Haykin (1999) and Dayan and Abbott (2001) for a more complete discussion of update rules that develop Hebb's original suggestion. We stress again that the hallmark of these rules is that global signals play a limited role. This means that such rules can yield "automatic" learning such as the organization of perception (see Figure 2.15 on page 59; Section 4.4.2) but cannot model learning that relies on feedback from the environment (O'Reilly and Munakata 2000).

# 4.2.2.2 Reinforcement learning

Instrumental conditioning, as we discussed earlier, requires a global signal that delivers information about the consequences of an animal's actions. So-called reinforcement learning algorithms are based on a similar idea, whereby learning is driven by a global signal about whether a network response has been "good" or "bad" (Section 2.3.4). The global signal is usually the same for many or all weights in the network. A biological example of such a signal may be the nociceptive system, which assigns to stimuli a value along the dimension of pain (Toates 2001). We have already discussed such "value systems" as part of motivational processes in Chapter 3. Figure 4.4 shows a network endowed with a simple value system. The