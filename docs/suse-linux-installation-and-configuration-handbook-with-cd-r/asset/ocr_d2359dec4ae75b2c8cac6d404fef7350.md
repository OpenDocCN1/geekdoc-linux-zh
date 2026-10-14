To set up XDM or KDM, start YaST and follow these steps:

+   1. Choose System Administration, Login Configuration. The Configure Login GUI dialog will pop up (see Figure 3.17).
+   2. In the Configure Login GUI dialog, select Login GUI for a graphical login, instead of ASCII.
+   3. If you have KDE installed, you will be able to select KDM in the Display manager field; otherwise, it will be disabled and you will be able to use only XDM. Choose KDM, if available. You can learn more about configuring KDM in Chapter 24, "Configuring the Desktop."
+   4. Select the Shutdown Behaviour of KDM for all. This will enable anyone to shut down the system by clicking shutdown and confirming the shutdown. You can learn more about this option in Chapter 24.

**FIGURE 3.17**
You can use YaST to configure the system to start in GUI login mode.

![](bbox=[0.32, 0.48, 0.78, 0.75])

# Setting Up Frame Buffer Device X Server

The Frame Buffer Device that comes with the kernel version 2.2.x is a blessing for those who have cards not currently supported by X. The only constraint is that the card should support VESA version 2. You need to prepare some settings for the frame buffer device X server to work:

**Kernel Preparation**—You do not have to recompile the kernel to prepare it for the frame buffer device X server unless you are using a kernel you recompiled previously. The kernel that comes precompiled with SuSE Linux is equipped with frame buffer support. If you want to recompile the kernel by yourself, you should include the following three options in the kernel: