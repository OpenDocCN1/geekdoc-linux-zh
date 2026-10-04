# Figure 4.15 Adding Executable File Designators

![](bbox=[0.353, 0.107, 0.646, 0.335])

Configuring your Software Restriction Policies is quite bit of work, and as such, you should minimize these policies due to the research and development investment. The first complex prerequisite is actually obtaining the desired file you want to deny access to. Numerous methods for obtaining the file exist, and it is easy to verify the malicious code once you opening it in a text editor. It may be more difficult if it is a compiled file such as an .exe; you may have to search for file hashes that other security professionals have released. After you are assured that you have safely obtained the file and stored it in a secure location, you will be ready to create a hash rule. The following steps walk you through creating a new hash rule within your Software Restriction Policy:

+   1. Prerequisite: Safety retrieve the file you want to deny access to.
2. Open the MMC console and add the Group Policy snap-in.
3. Open the interface window for modifying your Software Restriction Policies.
4. Click on the Additional Rules folder.
5. Right-click inside the folder and scroll up to select the New Hash section.
6. Click Browse and open the target file add that you want to create the hash rule for.
7. Once you have selected the file, ensure that the Security level is set to Disallowed and feel free to enter a brief description in the Description field.
8. Click OK.