+   *   Flows are allowed to cross from level to level
+   *   Flows in a line are united not by priority and the length of the use interval flows with shorter intervals are in line with higher priority

Within all queues, except the lowest, use circular scheduling (the lowest FIFO algorithm works). The different queues correspond to different lengths of time quanta - the higher the priority, the shorter the quantum (usually the length of the quantum for adjacent queues is halved). If the flow has exhausted its time quantum, it moves to the tail of the queue with a lower priority (and with a longer quantum). As a result, flows with shorter intervals (such as limited I / O) remain with high priority, and flows with longer intervals extend their time. You can also automatically move non-managed streams from the lower tier to the tier in and out.

# Lottery Planning

Planning lottery ( lottery scheduling ) - algorithm, easy to understand and easy to implement and it has great potential. The idea of lottery planning is that:

+   *   The stream receives an insane amount of lottery tickets, each of which entitles the processor to use T for a time
+   *   The scheduler selects one lottery ticket at random over a period of time T
+   *   The winnable stream gets control to the next draw

Lottery planning allows you to:

+   *   Emulate circular scheduling, giving each stream the same number of tickets