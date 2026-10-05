# ENABLING YUM SOFTWARE REPOSITORIES

# OBJECTIVES

After completing this section, you will be able to enable and disable use of Red Hat or third-party Yum repositories by a server.

# ENABLING RED HAT SOFTWARE REPOSITORIES

Registering a server to the subscription management service automatically grants access to software repositories based on the attached subscriptions. To view all available repositories:

```
[user@host~$ yum reposolist all
Loaded plugins: langpacks
repo id status repo name
rhel-8-server-debug-rpms/8Server/x86_64 Red Hat Enterprise Linux 8 Server
(Debug RPMs) disabled
rhel-8-server-rpms/8Server/x86_64 Red Hat Enterprise Linux 8 Server
enabled: 5,071
rhel-8-server-source-rpms/8Server/x86_64 Red Hat Enterprise Linux 8 Server
(Source RPMs) disabled
repolit: 5,071
```

The yum-config-manager command can be used to enable or disable repositories. To enable a repository, the command sets the enabled parameter to 1. For example, the following command enables the rhel-8-server-debug-rpms repository:

```
[user@host~$ yum-config-manager --enable rhel-8-server-debug-rpms
Loaded plugins: langpacks
================================= repo: rhel-8-server-debug-rpms ==================================
[rhel-8-server-debug-rpms]
async = True
width = 0
base_persistdir = /var/lib/yum/repos/x86_64/8Server
baseurl = https://cdn.redhat.com/content/dist/rhel/8/8Server/x86_64/debug
cache = 0
cabled = /var/cache/yum/x86_64/8Server/rhel-8-server-debug-rpms
check_config_file_age = True
cost = 1000
deltm_percentage =
enabled = 1
... omitted...
```

Red-Hat sources provide software through third-party repositories, which can be accessed by the yum command from a website, FTP server, or the local file system. For example, Adobe provides some of its software for Linux through a Yum repository. In a Red Hat classroom, the content.example.com classroom server hosts Yum repositories.