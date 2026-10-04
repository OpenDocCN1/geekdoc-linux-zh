在TCP/IP的术语里，大端字节序又称为“网络字节序（Network Byte Order）”，网络主机采用的字节序叫作“主机字节序”。x86和其他一些平台的主机字节序是小端字节序，但是IBM POWER等名服务器系列均采用大端字节序。因此，在主机字节序为大端字节序的平台上使用htonl()或htons()函数转换字节序，其实不会进行真正意义的字节重排。

+   [1] Debian网站提供虚拟机下载：nhttps://people.debian.org/~aurel132/qemu/mips/.