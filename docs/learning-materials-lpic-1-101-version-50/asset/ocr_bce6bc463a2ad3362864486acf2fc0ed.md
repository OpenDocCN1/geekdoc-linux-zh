```
# yum install p7zip
Loaded plugins: fastestmirror, langpacks
Loading mirror speeds from cached hostfile
\* base: mirror.ufscar.br
\* epel: mirror.glob0.com
\* extras: mirror.ufscar.br
\* updates: mirror.ufscar.br
Resolving Dependencies
---> Running transaction check
---> Package p7zip.x86_64 0:16.02-10.el7 will be installed
---> Finished Dependency Resolution

Dependencies Resolved

=============================================================
Package           Arch           Version            Repository   Size
=============================================================
Installing:
p7zip             x86_64         16.02-10.el7       epel          604 k

Transaction Summary
=============================================================
Install  1 Package

Total download size: 604 k
Installed size: 1.7 M
Is this ok [y/d/N]:
```

To upgrade an installed package, use yum update `PACKAGENAME`, where PACKAGENAME is the name of the package you want to upgrade. For example:

```
# yum update wget
Loaded plugins: fastestmirror, langpacks
Loading mirror speeds from cached hostfile
\* base: mirror.ufscar.br
\* epel: mirror.glob0.com
\* extras: mirror.ufscar.br
\* updates: mirror.ufscar.br
Resolving Dependencies
---> Running transaction check
---> Package wget.x86_64 0:1.14-18.el7 will be updated
---> Package wget.x86_64 0:1.14-18.el7_6.1 will be an update
---> Finished Dependency Resolution
```