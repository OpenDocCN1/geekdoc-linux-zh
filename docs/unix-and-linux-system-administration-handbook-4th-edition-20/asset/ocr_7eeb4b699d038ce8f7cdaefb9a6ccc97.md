# 18.10 EXERCISES

+   * E18.1 Explore your local NFS setup. Is NFS used, or is a different solution in place? Is automounting used? What tradeoffs have been made?

+   * E18.2 In NFS versions 2 and 3, what is the relationship between mount, nfsd, and portmap? What does the NFS dependency on portmap mean in terms of security?

+   * E18.3 What are some of the conceptual changes between NFS versions 3 and 4? How does the issue of stateful versus stateless change other attributes of the protocol?

+   * E18.4 Your employer needs you to export /usr and /usr/local through NFS. You have been given the following information and requests:
  a) Because of office politics, you want only your department (local subnet 192.168.123.0/24) to be able to use these exported filesystems. What lines must be added to which files to implement this configuration? Pay attention to the proper export options.
  b) List the steps needed to make mount and nfsd recognize these new shared filesystems. How could you verify that the directories were being shared without mounting them?
  c) Outline a strategy that would make all machines on your local subnet automatically mount the exported directories on the mount points /mnt/usr and /mnt/usr/local.