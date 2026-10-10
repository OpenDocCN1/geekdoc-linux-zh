# Kexec and Kdump

Now that you have learned how to use Kprobes, let’s continue and look at more facets of Linux RAS. Kexec and Kdump are serviceability features introduced in the 2.6 kernel.

Kexec uses the image overlay philosophy of the UNIX exec() system call to spawn a new kernel over a running kernel without the overhead of boot firmware. This can save several seconds of reboot time because boot firmware spends cycles walking buses and recognizing devices. The less the reboot latency, the less the system downtime; so, this was one of the main motivations for developing kexec. However, kexec’s most popular user is kdump. Capturing a dump after a kernel crash is inherently unreliable because kernel code that accesses the dump device might be in an unstable state. Kdump circumvents this problem by collecting the dump after booting into a healthy kernel via kexec.

# Kexec

Before you can kexec a kernel, you need to do some preparations:

+   1. Compile and boot into a kernel that has kexec support. For this, turn on CONFIG_KEXEC (Processor Type and Features → Kexec System Call) in the kernel configuration menu. This kernel is called the first kernel or the running kernel.
+   2. Prepare the kernel that is to be kexec-ed. This second kernel can be the same as the first kernel.
+   3. Download the kexec-tools package source tar ball from www.kernel.org/pub/linux/kernel/people/horms/kexec-tools/kexec-tools-testing.tar.gz. Build and produce the user-space tool called kexec.

The kexec tool built in Step 3 is invoked in two stages. The first stage loads the second kernel image into the buffers of the running kernel, while the second stage actually overlays the running kernel:

+   1. Load the second (overlay) kernel using the kexec command:
+   
+      ```bash
+      bash> kexec -1 /path/to/kernelsources/arch/x86/boot/bzImage --
+      append="root=/dev/hdaX" --initrd=/boot/myinitrd.img
+      ```
+   
+      bzImage is the second kernel, hdaX is the root device, and myinitrd.img is the initial root filesystem. The kernel implementation of this stage is mostly architecture-independent. At the heart of this stage is the sys_kexec() system call. The kexec command loads the new kernel image into the running kernel’s buffers using the services of this system call.
+   2. Boot into the second kernel:
+   
+      ```bash
+      bash> kexec -e
+      ... → Kernel boot up messages
+      ```
+   
+      Kexec abruptly starts the new kernel without gracefully halting the operating system. To shut down prior to reboot, invoke kexec from the bottom of the halt script (usually /etc/rc.d/rc0.d/S01halt) and invoke halt instead.
+   
+      The implementation of the second stage is architecture-dependent. The crux of this stage is a reboot_code_buffer that contains assembly code to put the new kernel in place to boot.