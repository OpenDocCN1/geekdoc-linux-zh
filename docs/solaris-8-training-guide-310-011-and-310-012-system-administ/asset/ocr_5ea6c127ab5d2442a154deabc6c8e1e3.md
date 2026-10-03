+   - Introduction 600
- Servers and Clients 601
- NFS on Solaris 601
  - NFS Daemons 604
  - Setting up NFS 604
  - NFS Security 608
- Mounting a Remote File System 609
- WebNFS 615
  - How to Enable WebNFS Access 617
  - Using a Browser to Access an NFS URL 618
- CacheFS 619
  - Creating the Cache 620
  - Monitoring the Cache 624
  - Deleting a Cache 626
  - Checking Consistency 627
- Autofs 628
  - Autofs Maps 631
    - Master Maps 631
  - Direct Map 635
  - Indirect Map 639
- When to Use Automount 644
- Summary 645
- Apply Your Knowledge 646

The following strategies will help you prepare for the test:

- This is one of those topics that you learn best by practicing and gaining experience. You'll encounter several questions on the exam related to the topics I present in this chapter. Practice the step-by-steps and the commands I describe on a Solaris system until you can perform them from memory. Concentrate on the options that I use in the examples. These are the options most likely to appear on the exam. Again, you'll need two networked systems to practice these exercises effectively.

- Be sure you are clear on the concepts introduced in this chapter especially NFS servers versus NFS clients. Be sure that you know which NFS daemons must be running on each, for NFS to operate properly. Know how to make resources available for mounting using the /etc/dfs/dfstab file. Be prepared to state the functions of an NFS server and NFS client.

- Be sure you understand how to mount network resources and how to make an entry in the /etc/vfstab file, so that mount points are established automatically at system startup. Pay particular attention to the `mount`, `mountall`, `umountall`, `shareall`, and `unshareall` commands.

- Study the AutoFS section and get a firm understanding of the various AutoFS maps, how they are configured, and how they compare to each other. Be sure you can describe each type of AutoFS map. Know the benefits of using AutoFS and be familiar with how to setup the various maps.