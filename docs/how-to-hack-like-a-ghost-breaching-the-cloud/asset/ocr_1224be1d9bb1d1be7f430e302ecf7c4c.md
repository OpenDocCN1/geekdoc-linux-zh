# 2

# RETURN OF COMMAND AND CONTROL

![](bbox=[0.15, 0.48, 0.3, 0.65])

Let’s build an attacking infrastructure by starting with the basic tooling of any attacker: the Command and Control (C2) server. We’ll look at three frameworks and test each on a virtual machine we’ll use as the target. First, we’ll look at how command and control used to be done, to see how we got where we are today.

# Command and Control Legacy

For the better part of the last decade, the undefeated champion of C2 frameworks—the one that offered the widest and most diverse array of exploits, stagers, and reverse shells—was the infamous Metasploit framework (https://www.metasploit.com/). Perform a quick search for a pentesting or hacking tutorial, and I bet the first link will refer you to a post describing how to set up a meterpreter—the name of the custom payload used by