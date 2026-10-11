
can use equation (2.11), with $y(t) = \sum_j W_{ji} y_j(t)$ (see Section 2.1.3 for details). The latter is in fact a discrete-time approximation of a simple continuous time model (since digital computers operate in time steps, such an approximation is always necessary in computer simulations). Another possibility is as follows. At each time step we choose a random ordering of the nodes. We then update the first chosen node. When we update the second node, we use the updated activity of the first node, and so on for all nodes. Since the random order is different at each time step, the procedure mimics the uncoordinated dynamics in real nervous systems and thus is called *asynchronous dynamics* (Amit 1989). Any result obtained in this way obviously is resistant to changes in the order of update operations.

## 2.3 ACHIEVING SPECIFIC INPUT-OUTPUT MAPPINGS

The input-output map realized by a network depends, of course, on the values of the weights. In practice, much of the work with neural networks is concerned with setting weights. Up to now we have considered problems in which suitable weights could be found either by intuition or by using simple mathematics. In this section we describe some powerful weight-setting methods that can deal with more complex problems. In the next section we describe procedures that organize network weights in response to incoming input rather than seeking to achieve a particular input-output map.

Weight-setting methods can be viewed either as models of real-world phenomena, i.e., how synapses change in nervous systems, or simply as a tool to build networks that handle a given task, without any additional claim. Here the focus is on the latter view, whereas Chapter 4 covers biological learning. Our goal is to build a network that produces a number $\mu$ of assigned input-output mappings:

$$
m(\mathbf{x}_\alpha, \mathbf{W}) = \mathbf{d}_\alpha \quad \forall \alpha = 1, \dots, \mu \tag{2.21}
$$

where $m$ is the input-output map realized by the network, $\mathbf{W}$ denotes all network weights, and $\mathbf{d}_\alpha$ is the desired output pattern to input $\mathbf{x}_\alpha$. Equation (2.21) is a system of $\mu$ equations where the unknowns are network weights. The direct analysis of these equations is typically very challenging or plainly infeasible. The only case that can be treated thoroughly with simple mathematics is linear networks, i.e., networks in which all nodes have a linear transfer function, such as equation (2.6). We discuss this case (with a final note on networks with nonlinear output nodes) before presenting more general weight setting techniques.

### 2.3.1 Setting weights in linear networks

If the transfer function of all nodes is linear, weights satisfying equation (2.21) can be found by formal methods, or it can be proved that they do not exist. We start with a linear perceptron, equation (2.19), and with a single input-output mapping. This corresponds to equation (2.21) with $\mu = 1$ and $m(\mathbf{x}_1, \mathbf{W}) = \mathbf{W} \cdot \mathbf{x}_1$. In this case it is easy to check that the single requirement $\mathbf{W} \cdot \mathbf{x}_1 = d_1$ is satisfied by a weight vector of the form

$$
\mathbf{W} = c_1 \mathbf{x}_1 \tag{2.22}
$$

with $c_1 = d_1 / (\mathbf{x}_1 \cdot \mathbf{x}_1)$. Moreover, if we add to $\mathbf{W}$ a vector $\mathbf{u}$ such that $\mathbf{u} \cdot \mathbf{x}_1 = 0$, the result is not altered. In conclusion, the general solution to the task is of the form

$$
\begin{cases} \mathbf{W} = \frac{d_1}{\mathbf{x}_1 \cdot \mathbf{x}_1}\mathbf{x}_1 + \mathbf{u} \\ \mathbf{u} \cdot \mathbf{x}_1 = 0 \end{cases} \tag{2.23}
$$

By extending this reasoning, it can be shown that the weight vector that realizes a number $\mu$ of input-output mappings can be written as

$$
\begin{cases} \mathbf{W} = \sum_{\alpha=1}^{\mu} c_\alpha \mathbf{x}_\alpha + \mathbf{u} \\ \mathbf{u} \cdot \mathbf{x}_\alpha = 0 \quad \forall \alpha = 1, \dots, \mu \end{cases} \tag{2.24}
$$

The general expression for the $c_\alpha$'s, however, is not as simple as in equation (2.23). We show how to solve this problem in the case of two input-output mappings. This simple task will be used throughout this section to illustrate and compare different weight setting techniques. It may be helpful to think of a discrimination task where $\mathbf{x}_1$ has to be mapped to a high output and $\mathbf{x}_2$ to a low one, although the procedure is the same for all desired outputs.

Following equation (2.24), we guess that $\mathbf{W}$ should be of the form $c_1 \mathbf{x}_1 + c_2 \mathbf{x}_2$, so our task is to find the values of $c_1$ and $c_2$ that satisfy the requirements $\mathbf{W} \cdot \mathbf{x}_\alpha = d_\alpha$. If we substitute $c_1 \mathbf{x}_1 + c_2 \mathbf{x}_2$ for $\mathbf{W}$, the requirements read

$$
\begin{aligned} (c_1 \mathbf{x}_1 + c_2 \mathbf{x}_2) \cdot \mathbf{x}_1 &= c_1 \mathbf{x}_1 \cdot \mathbf{x}_1 + c_2 \mathbf{x}_2 \cdot \mathbf{x}_1 = d_1 \\ (c_1 \mathbf{x}_1 + c_2 \mathbf{x}_2) \cdot \mathbf{x}_2 &= c_1 \mathbf{x}_1 \cdot \mathbf{x}_2 + c_2 \mathbf{x}_2 \cdot \mathbf{x}_2 = d_2 \end{aligned} \tag{2.25}
$$

For brevity, we write $\mathbf{x}_\alpha \cdot \mathbf{x}_\beta = X_{\alpha\beta}$:

$$
\begin{aligned} X_{11}c_1 + X_{12}c_2 &= d_1 \\ X_{12}c_1 + X_{22}c_2 &= d_2 \end{aligned} \tag{2.26}
$$

(note that $X_{12} = X_{21}$). The preceding is a system of two linear equations in the unknowns $c_1$ and $c_2$. It can be solved by a variety of methods, yielding

$$
\begin{aligned} c_1 &= \frac{d_1 X_{22} - d_2 X_{12}}{X_{11} X_{22} - X_{12}^2} \quad \quad c_2 &= \frac{d_2 X_{11} - d_1 X_{12}}{X_{11} X_{22} - X_{12}^2} \end{aligned} \tag{2.27}
$$

As an exercise, the reader can check that these expressions are really such that $\mathbf{W} \cdot \mathbf{x}_1 = d_1$ and $\mathbf{W} \cdot \mathbf{x}_2 = d_2$. If the network has to satisfy many input-output mappings, the same techniques apply, but the calculations get boring. Software for numeric or formal mathematics will come in handy, whereas textbooks on linear algebra will provide the theoretical foundation.

Note that equation (2.24) expresses the weight vector $\mathbf{W}$ in terms of the vectors $\mathbf{x}_\alpha$. This gives a concrete interpretation to the intuitive statement that the $\mathbf{x}_\alpha$'s have been "stored in memory." Moreover, it allows one to understand the output to a generic input $\mathbf{x}$ in terms of how $\mathbf{x}$ relates to the $\mathbf{x}_\alpha$'s (and to the vector $\mathbf{u}$). This will be discussed in Chapter 3.

Equation (2.24) also holds if the output node is not linear. Such a network can be written as $\mathbf{r} = f(\mathbf{W} \cdot \mathbf{x})$. We mention this case because a nonlinear output node is used often to limit network output between 0 and 1 and interpret it as probability of responding. The proof follows from noting that the requirement $d_\alpha = f(\mathbf{W} \cdot \mathbf{x}_\alpha)$ can be written $d_\alpha = \mathbf{W} \cdot \tilde{d}_\alpha$, where $\tilde{d}_\alpha = f^{-1}(d_\alpha)$ and $f^{-1}$ is the inverse function of $f$. Thus we are back to a linear problem, albeit with different $d_\alpha$'s. This means that different choices of $f$ result in different values of the $c_\alpha$'s but do not alter the structure of the weight vector.

### 2.3.1.1 Limits and abilities of linear networks

We expand here our remarks about the perceptron's limitations (page 40) by asking when the task in equation (2.21) can be solved by a perceptron. We then extend the reasoning to general linear networks. It is easy to determine when the task cannot be solved. Note, in fact, that the definition of a linear network $\mathbf{r} = \mathbf{W} \cdot \mathbf{x}$ implies

$$
\mathbf{r}(\mathbf{x}_\alpha + \mathbf{x}_\beta) = \mathbf{r}(\mathbf{x}_\alpha) + \mathbf{r}(\mathbf{x}_\beta) \tag{2.28}
$$

because $\mathbf{W} \cdot (\mathbf{x}_\alpha + \mathbf{x}_\beta) = \mathbf{W} \cdot \mathbf{x}_\alpha + \mathbf{W} \cdot \mathbf{x}_\beta$ (from equation 2.8). In words, the output to a sum of inputs equals the sum of the outputs to each input (indeed, this is the technical meaning of linear). It is then clear that an input-output map where, say, $\mathbf{x}_\gamma = \mathbf{x}_\alpha + \mathbf{x}_\beta$ but $\mathbf{d}_\gamma \neq \mathbf{d}_\alpha + \mathbf{d}_\beta$ cannot be realized by a linear network. In general, if among the inputs $\mathbf{x}_1, \dots, \mathbf{x}_n$ there is one, say, $\mathbf{x}_\beta$, that can be written as a weighted sum of the others, e.g.,

$$
\mathbf{x}_\beta = \sum_{a \neq \beta} b_a \mathbf{x}_a \tag{2.29}
$$

(for some choice of the $b_a$'s), then a weight vector $\mathbf{W}$ realizing the input-output map in equation (2.21) does not exist unless

$$
\mathbf{d}_\beta = \sum_{a \neq \beta} b_a \mathbf{d}_a \tag{2.30}
$$

That is, the same relationship must hold among outputs that holds among inputs. Conversely, if it is impossible to write any of the $\mathbf{x}_a$'s in the form of equation (2.29), the input-output map in equation (2.21) can be realized by a linear network for any choice of the $\mathbf{d}_a$'s. Indeed, the reader may have noted that equation (2.27) is meaningless if $X_{11}X_{22} = X_{12}^2$ (fraction denominators vanish). This happens precisely when $\mathbf{x}_1 = b\mathbf{x}_2$, a special case of equation (2.29). In fact, in this case we have

$$
\begin{align*} X_{11} &= \mathbf{x}_1 \cdot \mathbf{x}_1 \\ X_{22} &= b^2 \mathbf{x}_1 \cdot \mathbf{x}_1 \\ X_{12} &= b \mathbf{x}_1 \cdot \mathbf{x}_1 \end{align*} \tag{2.31}
$$

so that $X_{11}X_{22} = X_{12}^2 = b^2(\mathbf{x}_1 \cdot \mathbf{x}_1)^2$. Further information on this topic can be sought in linear algebra textbooks (sections on systems of linear equations).
