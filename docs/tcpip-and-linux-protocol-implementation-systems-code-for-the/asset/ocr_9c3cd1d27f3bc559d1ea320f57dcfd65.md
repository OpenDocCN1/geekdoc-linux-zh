# Forward 789

71 At the moment CSZ is the only scheduler that provides

72 true guaranteed service. Other schemes (including CBQ)

73 do not provide guaranteed delay and randomize jitter.

74

75 There is a proof (Sally Floyd), that delay

76 can be estimated by a IntServ compliant formula.

77 This result is true formally, but it is wrong in principle.

78 It takes into account only round-robin delays,

79 ignoring delays introduced by link sharing i.e. overlimiting.

80 Note that temporary overlimits are inevitable because

81 real links are not ideal, and the real algorithms must take this

82 into account.

# Figure 9.196 CSZ notation: linux/net/sched/sch_csz.c.

86

--- Notations.

87

$$ is link bandwidth (bits/sec).

88

89

$$ is set of all flows, including flow $$$.

90 Every flow $$a$ in has associated bandwidth slice $$r\_a < 18$ and

91 $$sum(a \in I) r\_a = 18.

92

93

94

--- Flow Model.

95

96 Let $$a\_s$ is the number of backlogged flows in flow $$a\_s$.

97 The flow is \($$em active), if $$m\_a > 0$.

98 This number is a discontinuous function of time;

99

100 when packet $$s$ arrives:

\ "

101 m\_a(t+0) - m\_a(t-0) = L\_i$,

102

103 where $$l\_s$ is the length of the arrived packet.

104 The flow queue is drained continuously until $$m\_a = --$

105

106 d (m\_a \over dt) = { B r\_a \over \sum(b \in I) r\_b \},

107 I.e. flow rates are allocated rates proportionally

108 scaled to take all available link bandwidth. Apparently,

109 it is not the only possible policy. F.e. CBQ classes

110 without borrowing would be modelled by:

111

\ "

112 d (m\_a \over dt) = B r\_a

113 }

114

115 More complicated hierarchical bandwidth allocation

116 policies are possible, but unfortunately, the basic

117 flow equations have a simple solution for proportional

118 scaling.