# ## Configuring Gopher

Installing and configuring Gopher (and Gopher+) is a matter of setting a number of con-figuration options before compiling the system software (it is usually not precompiled for you) and configuring some standard files. Gopher+ is done in the same manner, although with some extra parameters. Because Gopher is more likely to be on a Linux site than Gopher+, we’ll concentrate on that.

Throughout this section, we will use filenames without full path extensions because it really doesn’t matter where you install the Gopher software, as long as the directory paths are set correctly. There is no real standard configuration for directory locations, so feel free to choose whatever works best for you.

# ### The gopherd.conf File

The configuration parameters for Gopher (and Gopher+) are in a file called gopherd.conf, which is read by the Gopher daemon gopherd. The default settings gener-ally need a little modification, although many changes are simply changing commented lines to uncommented, and vice versa.

The first step is to create an alias for the Gopher service on your machine. Perform this step with the line that defines the hostalias. There should be a line in the file that looks like this:

```
hostalias: tpci
```

The alias is used to find the Gopher server on your system and should not be directly tied to a real machine, so you can make changes whenever you wish. The best approach is to create an alias and tie it to a physical machine with DNS. If you are running a standalone machine, you can use either an alias tied to your machine name or your machine name directly.

You can also control the number of Gopher connections allowed at one time. This is sometimes necessary to prevent a system from bogging down due to excessive user load. The maximum number of connections Gopher allows is given in a file, usually in the directory PIDS_Directory. A line in the gopherd.conf file usually has this variable com-mented out because early versions didn’t implement it properly or it was unstable. If you want to allow this feature, remove the comment symbol and make sure the directory it points to has the necessary files for your version of Gopher. The line usually looks like this:

```
#PIDS_Directory: /pids
```

![](bbox=[0.83, 0.78, 0.96, 0.96])