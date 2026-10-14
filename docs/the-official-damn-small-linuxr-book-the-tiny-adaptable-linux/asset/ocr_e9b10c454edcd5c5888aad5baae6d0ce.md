Figure 7-3 shows an example of Damn Small Linux running in VMPlayer in Windows XP.

![](bbox=[0.15, 0.22, 0.9, 0.78])

# FIGURE 7-3 Damn Small Linux running in VMPlayer on a Windows XP host system.

# Comparing VMPlayer to Qemu

In many ways, Qemu and VMPlayer performance benchmarks are comparable. Some studies have put Qemu with the KQEMU accelerator ahead in performance. In my limited testing, VMPlayer boots faster and seems to struggle less with resources during general use. It could be that our default settings in Qemu are limiting the system; we will have to do further testing to figure out the discrepancy.

VMPlayer is much larger than Qemu (25MB versus less than 2MB), and it needs to be installed on the host operating system. So, there is not a way to run VMPlayer from a low impact pen drive like QEMU. If you are in a situation where you are using a Windows computer and you want a way to get back into running