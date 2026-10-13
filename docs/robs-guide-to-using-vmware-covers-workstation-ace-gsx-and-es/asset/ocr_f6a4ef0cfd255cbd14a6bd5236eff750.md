# 5.3 Creating VMware ACE Projects

Virtual machines do not run inside ACE directly; they must be organized in projects. To start a new project, click the icon in the ACE Manager home window or select File → New Project.

+   1. Provide a name for your project and a location where you would like to store the project files.
+   
+   2. Next, you are asked if you want to start the Add Virtual Machine Wizard. For this example, I have selected to do so.
+   
+   3. The wizard that is used to add new virtual machines is very much like the one in VMware Workstation. An important different first step is that you can choose to create an entire new machine or to use an existing machine. Creating a new virtual machine is identical to this process in VMware Workstation, except that you can not use raw physical partitions for your virtual machine since these can not be copied to end user computers.
+   
+   If you choose to use an existing virtual machine, browse to the .vmx file of that machine to add it to your project.
+   
+   4. When the Add Virtual Machine Wizard is complete, you will be prompted to configure policies for the virtual machines in the newly created project. Configuring policies is discussed later in this chapter.