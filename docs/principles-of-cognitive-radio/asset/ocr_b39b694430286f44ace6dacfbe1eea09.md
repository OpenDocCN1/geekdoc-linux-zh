![](bbox=[0.22, 0.12, 0.93, 0.48])

Figure 5.3 Probability of detection vs. average SNR (dB) for an OFDM signal in a Rayleigh fading channel for single-user sensing and cooperative detection of ten secondary users using cyclostationarity-based local detectors [123]. Cooperative sensing improves the detection performance significantly due to spatial diversity. Moreover, using multiple cyclic frequencies further improves the performance. (SU = secondary user, cf. = cyclic frequency).

where k in the subscript denotes the kth user's local test statistic.

Figure 5.3 illustrates the single-user and collaborative detection performance of different cyclostationarity-based detectors in a Rayleigh fading channel.

# Energy-efficient sensing

In wireless networks, secondary user terminals are often battery-operated. Consequently, low power consumption is an important design goal. There are many ways to lower the power consumption both in spectrum sensing and during exploitation of the identified idle spectrum. In spectrum sensing, the power consumption depends obviously on the employed sensing algorithms and their implementation, the duty cycle used in sensing, the employed sensing policy, as well as the power used in reporting the sensing results. In addition, deciding if and how the idle spectrum is accessed plays a key role in prolonging battery life. For example, if the secondary user is experiencing poor channel quality even if the channel is detected to be idle, it may make sense not to access the channel for transmitting with low rate while using high transmit power.

Censoring is a promising method to reduce power consumption in reporting sensing results to a fusion center [23, 166]. In order to limit the amount of data transmitted and save energy, only sufficiently informative decision statistics may be communicated to the fusion center or shared with other users. A secondary user sends its test statistic to the fusion center only when its test statistic, denoted here by log Λ_i, is above a censoring threshold defined by the communication rate constraint specified by the designers:

P[log Λ_i > ψ_i | H0] ≤ κ_i, i = 1, …, N_SU. (5.28)