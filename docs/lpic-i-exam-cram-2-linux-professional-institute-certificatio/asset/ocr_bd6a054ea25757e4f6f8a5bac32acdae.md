> **ALERT**
> If you have been running **inetd** and are converting to run **xinetd**, the most important file is `/etc/inetd.conf`, which contains entries that define which services should be provided on demand. These lines should form the basis of the new **xinetd** configuration. Red Hat includes a utility named **inetdconvert** that can help with this process.

# # xinetd Configuration Files

The **xinetd** daemon initially uses the `/etc/xinetd.conf` file to set a few daemon configuration settings and the defaults that will be picked up by all **xinetd**s governed services and to specify the include directory. (These defaults are overridden by any settings in the individual service configuration files.)

The include directory is typically `/etc/xinetd.d`, which contains a single text file for each governed service. The service configuration files contain the definition of a service and any special settings that need to be set for correct functioning.

Figure 18.1 shows the relationships between the components of the **xinetd** services and files.

![](bbox=[0.1, 0.48, 0.8, 0.61])

**Figure 18.1** How **xinetd** works.

As you can see, **xinetd** reads `/etc/xinetd.conf` and gets its configuration, including the include directory location; then it waits for a client request for one of its services. When a client request arrives, xinetd looks at the packets and finds the target port/service and looks that service up by name in the `/etc/xinetd.d` directory. This directory contains one file per service, named exactly as the service name appears in `/etc/services`.

The `/etc/xinetd.conf` file is simple by nature:

```
```bash
# Simple configuration file for xinetd
# Some defaults, and include /etc/xinetd.d/
defaults
{
    instances                  = 60
    log_type                   = SYSLOG authpriv
    log_on_success             = HOST PID
    log_on_failure             = HOST
    cps                        = 25 30
}
include /etc/xinetd.d
```
```