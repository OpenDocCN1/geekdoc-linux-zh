![](bbox=[0.11, 0.03, 0.28, 0.1])

# 1.7.4 Client Machines

You will be assigned three dedicated client machines that are used in conjunction with the course material and exercises. These include a Windows 10 client, Debian Linux client, and a Windows Server 2016 Domain Controller.

You will need to **revert the machine you wish to use via the student control panel whenever you connect to the VPN**. When you choose to revert either the Windows 10 or Windows Server 2016 clients, both machines will be reverted. Your assigned client machines are automatically powered off and reverted to their initial state after you have been disconnected from the VPN for a period of time.

With the above in mind, we highly recommend that you **do not store any information on any of your client machines that you are not willing to lose**.

# 1.7.5 Kali Virtual Machine

The VMware image⁸ that we provide for your use during the course is a default 64-bit build of Kali Linux. We recommended that you download and use the VMware image via the URL provided in the emailed welcome package. While you are free to use the VirtualBox or Hyper-V image or even your own Kali installation, we can only provide support for the provided VMware image. These images are provided courtesy of Offensive Security and are not supported by the Kali Linux project team.

# 1.7.6 Lab Behavior and Lab Restrictions

The Offensive Security lab is a shared environment. Please keep the following in mind as you explore the lab:

+   - Avoid changing user passwords. Instead, add new users to the system if possible. If the only way into the machine is to change the password, kindly change it back once you are done with that particular machine.
+   - Any firewall rules that you disable on a machine should be restored once you have gained the desired level of access.
+   - Do not leave machines in a non-exploitable state.
+   - Delete any successful (and failed) exploits from a machine once you are done. If possible, create a directory to store your exploits. This will minimize the chance that someone else will accidentally use your exploit against the target.

You can accomplish all of this by remembering to revert each machine once you are done with it. To revert a machine, use the student control panel.

The following restrictions are strictly enforced in the internal VPN lab network. If you violate any of the restrictions below, Offensive Security reserves the right to disable your lab access.

⁸ https://www.offensive-security.com/kali-linux-vm-vmware-virtualbox-image-download/