# 7.2 Remoting tools

Due to the modular nature of Linux, there are numerous options when implementing a thin or slim client desktop solution. The options include basic remote access, where one workstation remotely displays the desktop of another workstation, network bootingless hardware, remote execution of a single application with a local display, or multiple users connecting to a single workstation.

# 7.2.1 Remote access

Remote access is where the entire application logic resides on a server and the client only runs presentation logic. Implementations include Virtual Network Computing (VNC), NoMachine NX, or even desktop, a Linux client for Microsoft Remote Display Protocol (RDP) servers. However, because this kind of remoting usually requires a significant amount of network resources, remoting of the entire operating system is usually not used as a user's standard environment. Instead, they are used for situations such as remote diagnosis and help desk scenarios, or accessing a desktop workstation out of the office.

Figure 7-6 Sabayon editing a profile

![](bbox=[0.15, 0.078, 0.843, 0.473])

154 Linux Client Migration Cookbook, Version 2