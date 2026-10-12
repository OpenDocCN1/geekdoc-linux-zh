# Configuring Linuxconf modules

You can add new modules or deactivate existing modules. Modules are kept in the /usr/lib/linuxconf/modules directory. To add a new module, download the necessary RPM package from a Linuxconf FTP site. The list of FTP sites carrying Linuxconf files is available at http://dns.solucorp.qc.ca/linuxconf/available.html.

After you download the new Linuxconf module, use the rpm -ivh module_package command to install it. Once installed, the module automatically appears in the module list in Linuxconf. It is also automatically activated.

To deactivate a module, do the following:

+   1. Run Linuxconf from your console or X Window.

+   2. Select Control\> Control files and systems\> Configure Linuxconf modules from the left side of the Linuxconf screen. You will see a screen similar to that shown in Figure 4-7.

![](bbox=[0.13, 0.51, 0.86, 0.89])