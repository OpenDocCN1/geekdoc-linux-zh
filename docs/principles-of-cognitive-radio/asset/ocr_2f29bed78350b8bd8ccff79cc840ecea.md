![](bbox=[0.25, 0.11, 0.85, 0.32])

# Figure 2.9 Wireles network model.

message $W_{k}\in\mathcal{W}_{k} = \{1, \dots, 2^{nR_{k}}\}$ to destination $d_{k}$, at rate $R_{k}$. To do so, the source encoder maps the data sequence into a codeword $X_{k}^{n}$ consisting of $n$ symbols from the input alphabet, and sends it in $n$ time instants over the channel. All data sequences are mutually independent. Upon receiving the sequence $Y_{j}^{n}$ of length $n$, decoder $j$ maps it to its estimate of the transmitted data sequence, denoted by $\hat{W}_{j}$. The data sequence sets $\mathcal{W}_{1}, \mathcal{W}_{2}, \dots, \mathcal{W}_{K}$ along with the encoder and decoder mappings of all users define an $(R_{1}, R_{2}, \dots, R_{K}, n)$ code for this channel. The encoding function at source $s_{k}$ for data sequence $W_{k}$ at time $i$ is given by

$X_{k,i} = \mathit{f}_{k,i}(W_{k}, Y_{k}^{i-1}), \quad\quad k = 1, \dots, K. \tag{2.18}$

Note that the encoding function $\mathit{f}_{k,i}(\cdot)$ allows the source to use its receiver’s previous observations of the channel (typically obtained via feedback) to encode $W_{k}$. This allows sources to obtain information about data sequences sent by other users and potentially forward them through the network. The decoding function at destination $j$ at time $i$ is given by

$\hat{W}_{j} = g_{j}(Y_{j}^{n}), \quad\quad j = 1, \dots, K. \tag{2.19}$

A decoding error at destination $k$ occurs when $\hat{W}_{k} \neq W_{k}$. We consider that an error occurs unless all destinations decode their data sequences correctly. Thus, the error probability is given by the probability of the union of error events associated with incor-rect detection on each of the different data sequences:

$P_{e} = P \left[\bigcup_{k=1}^{K} \left[\hat{W}_{k} \neq W_{k}\right]\right]. \tag{2.20}$

If the error probability can be made arbitrarily small for a code of sufficiently large $n$, the rates $(R_{1}, \dots, R_{K})$ will be simultaneously achievable in the considered network. More precisely, rates $(R_{1}, R_{2}, \dots, R_{K})$ are achievable if, for any $\epsilon > 0$, there exists, for sufficiently large $n$, an $(R_{1}, R_{2}, \dots, R_{K}, n)$ code such that $P_{e} \leq \epsilon$. The capacity region is the closure of the set of all achievable rates $(R_{1}, R_{2}, \dots, R_{K})$, due to time-sharing between strategies associated with any set of points on the rate region.