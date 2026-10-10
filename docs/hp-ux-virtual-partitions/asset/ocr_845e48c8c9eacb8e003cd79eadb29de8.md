| Command | Description |
| :--- | :--- |
| **vparcreate** | form: `vparcreate -p vp_name [-B boot_attr] [-D db_file]`<br>`[-S static_attr]`<br>`[-b kernel_path] [-o boot_opts] [-a src] [-a...]` |
| Create a Virtual Partition. | To create a Virtual Partition with three processors (`num`) total, two bound (`min`), 2048MB RAM, all components on 0/0, boot disk at 0/0/1/1.2.0, with a kernel of `/stand/vmunix`, autolinux, on disk and console at 0/0/4/0:<br><br>```
# vparcreate -p vpR_name -a cpu::3 -a cpu::2:4
-a mem::2048MB -a io::0/0 -a io::0/0/1/1.2.0:boot
-b /stand/vmunix -B auto
```
<br>notes:<br>- `HP-UX 11i` must be loaded on volume before or after Virtual Partition is created. If `HP-UX 11i` is loaded after `vPar` is created, `vparboot -p vp_name -I ignite_kernel` is used to load 11i.<br>- `/stand/vmunix` is default and does not need to be specified.<br>- `vPar` was not set to `static`, meaning that it can be modified later.<br>- `CPUs` are three total (`num`), two bound (`min`), and as many as two unbound (`max`). |

| Command | Description |
| :--- | :--- |
| **vparmodify** | `vparmodify -p vp_name [-B boot_attr] [-D db_file] [-S static_attr]`<br>`[-b kernel_path] [-o boot_opts] [-P new_vp_name]` |
| Modify the attributes of a Virtual Partition.<br><br>(Note that `CPUs` are added relative to the current number with `-a, -a cpu::2` adds two `CPUs` to the current number of `CPUs`. `-m cpu::3` specifies an absolute number of `CPUs` of three.) | `[-a src] [-a...]`<br>`[-m src] [-m...]`<br>`[-d src] [-d...]`<br><br>To add processor at path `1/09` (adds this proc to those already assigned):<br>``` # vparmodify -p vPar_name -a cpu::1/09 ```<br>To specify an absolute number of three processors:<br>``` # vparmodify -p vPar_name -m cpu::3 ``` |

| Command | Description |
| :--- | :--- |
| **vparremove** | `vparremove -p vp_name [-D db_file] [-f]` |
| Delete a Virtual Partition. | To delete a Virtual Partition in the currently running database:<br>``` # vparremove -p vPar_name ``` |

| Command | Description |
| :--- | :--- |
| **vparreset** | `vparreset -p vp_name [-h|-q] [-q] [-f]` |
| Reset a Virtual Partition. | To reset a Virtual Partition simulating the TOC operations at the Crl+B prompt. Without the -h option, the default command simulates only a TOC.<br><br>``` # vparreset -p vPar_name ```<br><br>To force a hard reset of a Virtual Partition:<br><br>``` # vparreset -p vPar_name -h -f ``` |