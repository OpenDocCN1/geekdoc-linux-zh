# Virtual Partitions Command Summary

| Command | Description |
| :--- | :--- |
| **vparcreate** Create a Virtual Partition. | form: `vparcreate -p vp_name [-B boot_attr] [-D db_file] [-S static_attr] [-b kernel_path] [-o boot_opts] [-a rsrc] [...,]` |
| | To create a Virtual Partition with three processors ($num$) total, two bound ($min$), 2048MB RAM, all components on /0/0, boot disk at 0/0/1/2.0, with a kernel of /stand/vmunix, autoboost on, and console at 0/0/4/0: |
| | `# vparcreate -p vPar_name -a cpu::3 -a cpu::2:4 -b mem::2048 -a io::0/0 -a io::0/0/1/2.0:boot -b /stand/vmunix -B auto` |
| | Notes: - HP-UX 11i must be loaded on volume before or after Virtual Partition is created. If HP-UX 11i is loaded after vPar is created, `vparboot -p vp_name -I ignite_kernel` is used to load 11i. - /stand/vmunix is default and does not need to be specified. - vPar was not set to *static*, meaning that it can be modified later. - CPUs are three total ($num$), two bound ($min$), and as many as two unbound ($max$). |
| **vparmodify** Modify the attributes of a Virtual Partition. (Note that CPUs are added relative to the current number with $-a$. $-a\ cpu::2$ adds two CPUs to the current number of CPUs. $-m\ cpu::3$ specifies an absolute number of CPUs of three.) | form: `vparmodify -p vp_name [-B boot_attr] [-D db_file] [-S static_attr] [-b kernel_path] [-o boot_opts] [-P new_vp_name] [-a rsrc] [...,] [-m rsrc] [...,] [-d rsrc] [...,]` |
| | To add processor at path /109 (adds this proc to those already assigned): `# vparmodify -p vPar_name -a cpu::109` To specify an absolute number of three processors: `# vparmodify -p vPar_name -m cpu::3` |
| **vparremove** Delete a Virtual Partition. | form: `vparremove -p vp_name [-D db_file] [-f]` |
| | To delete a Virtual Partition in the currently running database: `# vparremove -p vPar_name` |