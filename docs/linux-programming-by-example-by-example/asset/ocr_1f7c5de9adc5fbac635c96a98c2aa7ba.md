# 5—
Signals

Signals are the simplest form of interprocess communication available in Linux. Processes use them to communicate with each other, and the kernel uses them to communicate with processes. Signals are also the key facilitator of *job control*, which is the ability to run jobs in the background or temporarily to stop them. If you are writing a non-trivial application program, you will use signals. Subjects this chapter covers include

+   * What is a signal?
+   * Signal terminology
+   * Early signal APIs and their problems
+   * The POSIX and Linux signal API
+   * Sending and receiving signals
+   * Manipulating signal sets