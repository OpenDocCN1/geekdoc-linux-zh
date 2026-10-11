with $c_1 = d_1 / (\mathbf{x}_1 \cdot \mathbf{x}_1)$. Moreover, if we add to $\mathbf{W}$ a vector $\mathbf{u}$ such that $\mathbf{u} \cdot \mathbf{x}_1 = 0$, the result is not altered. In conclusion, the general solution to the task is of the form

$$\begin{cases} \mathbf{W} = \frac{d_1}{\mathbf{x}_1 \cdot \mathbf{x}_1}\mathbf{x}_1 + \mathbf{u} \\ \mathbf{u} \cdot \mathbf{x}_1 = 0 \end{cases} \tag{2.23}$$

By extending this reasoning, it can be shown that the weight vector that realizes a number $\mu$ of input-output mappings can be written as

$$\begin{cases} \mathbf{W} = \sum_{\alpha=1}^{\mu} c_\alpha \mathbf{x}_\alpha + \mathbf{u} \\ \mathbf{u} \cdot \mathbf{x}_\alpha = 0 \quad \forall \alpha = 1, \dots, \mu \end{cases} \tag{2.24}$$

The general expression for the $c_\alpha$'s, however, is not as simple as in equation (2.23). We show how to solve this problem in the case of two input-output mappings. This simple task will be used throughout this section to illustrate and compare different weight setting techniques. It may be helpful to think of a discrimination task where $\mathbf{x}_1$ has to be mapped to a high output and $\mathbf{x}_2$ to a low one, although the procedure is the same for all desired outputs.

Following equation (2.24), we guess that $\mathbf{W}$ should be of the form $c_1 \mathbf{x}_1 + c_2 \mathbf{x}_2$, so our task is to find the values of $c_1$ and $c_2$ that satisfy the requirements $\mathbf{W} \cdot \mathbf{x}_\alpha = d_\alpha$. If we substitute $c_1 \mathbf{x}_1 + c_2 \mathbf{x}_2$ for $\mathbf{W}$, the requirements read

$$\begin{aligned} (c_1 \mathbf{x}_1 + c_2 \mathbf{x}_2) \cdot \mathbf{x}_1 = c_1 \mathbf{x}_1 \cdot \mathbf{x}_1 + c_2 \mathbf{x}_2 \cdot \mathbf{x}_1 = d_1 \\ (c_1 \mathbf{x}_1 + c_2 \mathbf{x}_2) \cdot \mathbf{x}_2 = c_1 \mathbf{x}_1 \cdot \mathbf{x}_2 + c_2 \mathbf{x}_2 \cdot \mathbf{x}_2 = d_2 \end{aligned} \tag{2.25}$$

For brevity, we write $\mathbf{x}_\alpha \cdot \mathbf{x}_\beta = X_{\alpha\beta}$:

$$\begin{aligned} X_{11}c_1 + X_{12}c_2 = d_1 \\ X_{12}c_1 + X_{22}c_2 = d_2 \end{aligned} \tag{2.26}$$

(note that $X_{12} = X_{21}$). The preceding is a system of two linear equations in the unknowns $c_1$ and $c_2$. It can be solved by a variety of methods, yielding

$$\begin{aligned} c_1 &= \frac{d_1 X_{22} - d_2 X_{12}}{X_{11} X_{22} - X_{12}^2} \quad \quad c_2 &= \frac{d_2 X_{11} - d_1 X_{12}}{X_{11} X_{22} - X_{12}^2} \end{aligned} \tag{2.27}$$

As an exercise, the reader can check that these expressions are really such that $\mathbf{W} \cdot \mathbf{x}_1 = d_1$ and $\mathbf{W} \cdot \mathbf{x}_2 = d_2$. If the network has to satisfy many input-output mappings, the same techniques apply, but the calculations get boring. Software for numeric or formal mathematics will come in handy, whereas textbooks on linear algebra will provide the theoretical foundation.

Note that equation (2.24) expresses the weight vector $\mathbf{W}$ in terms of the vectors $\mathbf{x}_\alpha$. This gives a concrete interpretation to the intuitive statement that the $\mathbf{x}_\alpha$'s have been "stored in memory." Moreover, it allows one to understand the output to a