VMware provides formal, official support for these editions of Linux as a guest operating system:

+   - Red Hat Linux 5.x to 6.x
+   - Caldera OpenLinux 1.3 to 2.x
+   - SuSE Linux 5.3 to 6.x
+   - TurboLinux 6.0
+   - Corel Linux OS 1.0

(In general, it's safe to assume that newer versions than those listed will work as well.)

If you're extremely clever, knowledgeable, and patient, you might be able to make other distributions work, but you do so on your own, because VMware does not officially support those configurations. You may have difficulty installing VMware tools or getting certain virtual device drivers to work properly.

> VMware can be coaxed to run on some Slackware Linux and Linux-Mandrake hosts, despite the fact that VMware does not support these distributions as host operating systems. But the techniques required to make VMware run on these hosts don't carry over to running them as guests. Unless you know what you're doing and you have a lot of time to kill, stick with the approved list.

![](bbox=[0.07, 0.58, 0.15, 0.72])

In this chapter, I demonstrate Linux on Linux by installing Corel Linux OS. Because it's the newest major Linux distribution, many people have not yet had a chance to try it. Plus, it is a unique case, being the only Linux distribution currently supported as a guest OS, but not as a host OS.

If Corel Linux isn't your cup of tea, keep reading. Although each Linux distribution has its own particular installation engine, the techniques are similar for any supported version of Linux, and I note some special exceptions for other distributions.

> Read everything that follows in this chapter very carefully. It might get confusing, because both your host and guest operating systems are Linux. Wherever there might be confusion, I am sure to distinguish between the host (which is your PC and the Linux operating system you boot into every time you turn on your computer) and the guest (the VMware virtual machine that will be running Corel Linux OS in my examples). Be sure you understand which Linux I am referring to before you follow any of the steps.

![](bbox=[0.07, 0.88, 0.15, 0.98])