# NNLS Installation Data

| NNLS COMPONENT | DATA REQUIRED | DESCRIPTION |
| --- | --- | --- |
| eDirectory | NICI file location and filename | This is the path and filename of the NICI file you downloaded. You should insert the floppy disk containing this file in your server's floppy drive and mount it to the /media/floppy directory before beginning installation. The NNLS installation script is coded to look in this directory for the file. |
|  | Install a new tree or into an existing tree? | You must specify whether you are installing a new eDirectory tree or into an existing tree. |
|  | Tree name | The data you provide here is dependent on whether you are installing a new tree or into an existing tree. If you're installing a new eDirectory tree, you must determine a unique name. If you're installing into an existing tree, you must supply its name at this prompt. |
|  | Existing server IP address | If you're installing into an existing tree, you need to know the IP address of the server (NetWare, Linux, or Windows) that already resides in the tree. If you're installing into a new tree, you won't be prompted to provide this information. |