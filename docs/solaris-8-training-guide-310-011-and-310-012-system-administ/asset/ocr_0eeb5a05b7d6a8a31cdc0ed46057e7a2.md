# STEP BY STEP

# 1.4 Breaking Out of a Hung System

+   1. Use the abort key sequence for your system (Stop+A or L1+A).

The monitor displays the ok PROM prompt.

2. Type the sync command to synchronize the disks:

`ok sync`

3. When you see the syncing file systems message, press the abort key sequence for your system again.

4. Type the appropriate reset command to reset the hardware and start the boot process:

`ok reset`

5. After you receive the login: message, log in and type the following to verify that the system is booted to the specified run level:

`# who -r`

6. The system responds with the following:

`run-level 3 Jun 9 09:19 3 0 S`

Step by Step: Step by Steps are hands-on tutorial instructions that walk you through a particular task or function relevant to the exam objectives.

Figures: Detailed figures help clarigy your understanding of the text.

![](bbox=[0.06, 0.5, 0.28, 0.57])

FIGURE 19.22
Computers/Networks window

As shown in the pop-up menu on Figure 19.22, you can add a computer to the network.

Double-click the Computers icon, and all of the computers in your domain are displayed, as shown in Figure 19.23.

![](bbox=[0.06, 0.65, 0.28, 0.77])

FIGURE 19.23
Computers in your domain.

Double-click the specific computer's icon, and the Computers Properties window appears, as shown in Figure 19.24.

![](bbox=[0.06, 0.82, 0.28, 0.91])

FIGURE 19.24
Computers Properties window.