# Real World Scenario

# **Booting School VMs with Shell Scripts**

A school environment is an excellent setting for using guest virtual machines, especially in computer science classes. VMs provide an economical and highly flexible solution.

On the servers, guest VMs are configured to employ either temporary or permanent storage, depending on class needs. For example, students who do not need long-term storage for their files on the VM are provided with guest virtual machines with transitory virtual disks. Students who do need to store and later access their files, such as programming students, are provided with guest machines with persistent storage.

These guest virtual machines are booted as needed via scripts. The scripts can be initiated by an instructor prior to class or scheduled via a cron job (covered in Chapter 26, “Automating Jobs”) or even via systemd timers (systemd was covered in Chapter 6, “Maintaining System Startup and Services”).

In the classroom, either thin clients or student (or school-provided) laptops are available for accessing the guest virtual machines. The configuration and deployment of such machines simplifies many school computing environment complications and typically lowers associated costs.

# **Kickstarting with Anaconda**

You can quickly and rather easily bootstrap a new system (physical or virtual) using the *kickstart installation method*. This RHEL-based technique for setting up and conducting a system installation consists of the following:

+   1. Create a kickstart file to configure the system.

+   2. Store the kickstart file on the network or on a detachable device, such as a USB flash drive.

+   3. Place the installation source (e.g., ISO file) where it is accessible to the kickstart process.

+   4. Create a boot medium that will initiate the kickstart process.

+   5. Kick off the kickstart installation.

# **Creating the Kickstart File**

A *kickstart file* is a text file that contains all the installation choices you desire for a new system. While you could manually create this file with a text editor, it is far easier to use an *anaconda file*. For Red Hat–based distros, at installation, this file is created and stored in the