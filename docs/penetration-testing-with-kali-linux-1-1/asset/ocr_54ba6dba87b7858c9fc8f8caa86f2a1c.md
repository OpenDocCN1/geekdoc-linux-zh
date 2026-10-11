# **25. Trying Harder: The Labs**

You have been hired to perform a penetration test on the internal VPN lab network for the duration of the course. The main objective is to get as many shells on as many machines and subnets as possible. Your goal is to obtain the highest possible privilege level (administrator/root) on each machine.

You may alter administrator or root passwords on lab machines as needed or add additional users to the system, provided you revert the machine back to its pristine state via your student control panel once you have finished attacking it. Some machines have multiple attack vectors, so it is highly recommended that you take the time to locate as many as possible. While you may certainly use web shells to get an initial foothold on a machine, your real goal is a reverse shell back to your Kali virtual machine or GUI access to the target.

**Note:** The **proof.txt** files that are located on each machine are to be documented in your lab report, should you opt to submit one. These files should not be seen as the end goal (this is a penetration test, not a capture the flag event). There is no greater feeling than getting high-privileged shells on lab machines, and you will soon be experiencing that feeling.

# 25.1  Real Life Simulations

The internal VPN lab network contains a number of simulated clients that can be exploited using client-side attacks. These clients are programmed to simulate common corporate user activity. Subtle hints throughout the lab can help you locate these simulated clients. Thorough post-exploitation information gathering may also reveal communication between client machines.

The various simulated clients will perform their task(s) at different time intervals. The most common interval is five minutes.

Some of the lab machines contain clean-up scripts. These are used in client-side attack vectors in particular to help ensure that the machine/service remains available for use by other students.

# 25.2  Machine Dependencies

Some targets can not be exploited without first gathering specific additional information on another lab machine. Others can only be exploited through a pivot. Student administrators will not provide details about machine dependencies. Determining whether or not a machine has a dependency is an important part of the information gatering process, so you’ll need to discover this information on your own.

# 25.3  Unlocking Networks

Initially, the PWK control panel will allow you to revert machines on the Student Network as well as your own dedicated lab client machines. Certain vulnerable machines in the lab will contain a **network-secret.txt** file with a MD5 hash in it. These hashes will unlock additional networks in your control panel.