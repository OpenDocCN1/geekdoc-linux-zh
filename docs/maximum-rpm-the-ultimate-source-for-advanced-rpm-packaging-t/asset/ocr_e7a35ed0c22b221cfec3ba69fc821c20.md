# ## 20.2.2. Getting Software to Build

Looking at the docs/INSTALL file, we find that the steps required to get amanda configured and ready to build are actually fairly simple. The first step is to modify tools/munge to point to cpp, the C preprocessor.

Amanda uses cpp to create makefiles containing the appropriate configuration information. This approach is a bit unusual, but not unheard of. In munge, we find the following section:

```
# Customize CPP to point to your system's C preprocessor.
# if cpp is on your path:
CPP=cpp

# if cpp is not on your path, try one of these:
# CPP=/lib/cpp              # traditional
# CPP=/usr/lib/cpp          # also traditional
# CPP=/usr/ccs/lib/cpp     # Solaris 2.x
```

Since cpp exists in /lib on Red Hat Linux, we need to change this part of munge to

```
# Customize CPP to point to your system's C preprocessor.
# if cpp is on your path:
#CPP=cpp

# if cpp is not on your path, try one of these:
CPP=/lib/cpp               # traditional
# CPP=/usr/lib/cpp          # also traditional
# CPP=/usr/ccs/lib/cpp     # Solaris 2.x
```

Next, we need to take a look in config/ and create two files:

+   - config.h, which will contain platform-specific configuration information
+   - options.h, which will contain site-specific configuration information

There are a number of sample config.h files for a number of different platforms. There is a Linux-specific version, so we copy that file to config.h and review it. After a few changes to reflect our Red Hat Linux environment, it is ready. Now let’s turn our attention to options.h. In the case of options.h, there’s only one sample file: options.h-vanilla. As the name implies, this is a basic file that contains a series of #defines that configure amanda for a typical environment. We’ll need to make a few changes:

+   - Define the paths to common utility programs.
+   - Keep the programs from being named with the suffix -2.3.0.
+   - Define the directories where the programs should be installed.

While the first change is pretty much standard fare for anyone used to building software, the last two changes are really due to RPM. With RPM, there’s no need to name the programs with a version-specific name, as RPM can easily upgrade to a new version and even downgrade back if the new version doesn’t work as well. The default paths amanda uses segregate the files