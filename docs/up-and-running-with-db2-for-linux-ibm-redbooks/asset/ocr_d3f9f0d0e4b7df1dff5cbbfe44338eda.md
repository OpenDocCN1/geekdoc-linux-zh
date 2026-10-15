By default, the response file that gets created is called db2ese.rsp. However, you have the option to change the name and destination directory while using the DB2 Setup wizard. Refer to Figure 2-11 on page 60.

# Creating a response file using the DB2 Setup wizard

Near the beginning of the DB2 UDB ESE Setup wizard, you will see the following window (Figure 2-12).

![](bbox=[0.39, 0.315, 0.715, 0.475])

Figure 2-12 Save settings in response file

Simply check off the checkbox beside Save settings in a response file. This will save all installation settings to a file called db2ese.rsp. We suggest you change the destination directory to an exported file system (for example, /software) available to everyone on the network. The target directory of the response file is specified on the Start copying files window of the DB2 Setup wizard, shown in Figure 2-11 on page 60.

To install DB2 using the response file, refer to the instructions in "Step 2 - Use response file to install DB2 on remaining machines" on page 64. If you want to create a response file by editing a sample response file, refer to "Creating a response file using the sample response file" on page 66.

# 2.3.2 Multiple partition installation

There are several ways in which you can install DB2 on a multiple-partition environment: (1) use the DB2 Setup wizard to install DB2 and create a new instance on the primary machine, then use a response file to install DB2 on the remaining machines participating in the partitioned database, or (2) edit a sample response file and use this file to install DB2 on each machine in the cluster, or (3) use db2_install or a combination of DB2 Setup wizard and db2_install to set up your environment.

The easiest method is to use the DB2 Setup wizard on the primary machine, and then a response file on the remaining machines participating in the partitioned database system. We discuss this method first.

# Multiple partition install using DB2 Setup

With this method, the first step is to use the DB2 Setup wizard on the instance-owning machine to install DB2 and create a new instance. This instance