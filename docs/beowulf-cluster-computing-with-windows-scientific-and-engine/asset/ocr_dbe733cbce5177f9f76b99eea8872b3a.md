Users request service of a batch server by calling the appropriate library routine and passing it the required parameters. The parameters correspond to the options and operands on the commands. The user must ensure that the parameters are in the correct syntax. Each function will return zero upon success and a nonzero error code on failure. These error codes are available in the header file 'PBS_error.h'. The library routine will accept the parameters and build the corresponding batch request. This request is then passed to the server communication routine. (The PBS API is fully documented in the PBS External Reference Specification.)

# ## 16.3 Installing PBS

PBS is able to support a wide range of configurations. It may be installed and used to control jobs on a single system or to load balance jobs on a number of systems. It may be used to allocate nodes of a cluster or parallel system to both serial and parallel jobs. It can also deal with a mix of these situations. However, given the topic of this book, we focus on the recommended configuration for clusters. The PBS Administrator Guide explains other configurations.

When PBS is installed on a cluster, a MOM daemon must be on each execution host, and the Server and Scheduler should be installed on one of the systems or on a front-end system.

For Windows 2000 clusters, PBS is provided in a single package that contains

+   - the *PBS Administrator Guide* in PDF form
+   - the *PBS User Guide* in PDF form,
+   - the PBS Pro software, and
+   - supporting text files: software license, README, release notes, and the like.

The PBS Pro install program will walk you through the installation process. If you are installing from the PBS Pro CD-ROM, insert the CD-ROM into your computer's CD-ROM drive, browse to your CD-ROM drive, and double-click on the Install Program icon.

Alternatively, you can download the latest PBS Pro package from the PBS Pro Web site, and save it to your hard drive. From there you can manually run the installation program by typing

```
```
install.exe
```
```

The installation program will prompt you for the names of directories for the different parts of PBS and the type of installation (full, server-only, execution host