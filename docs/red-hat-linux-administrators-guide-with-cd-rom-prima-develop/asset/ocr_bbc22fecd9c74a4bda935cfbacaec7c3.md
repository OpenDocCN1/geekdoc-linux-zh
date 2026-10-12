| Commands | Definition |
| :--- | :--- |
| \*A chain | Adds a rule to the chain |
| \*D chain rule_number | Deletes a rule number from the chain |
| \*I chain rule_number | Inserts a rule into the chain before the designated number |
| \*R chain rule_number | Replaces the rule number in the chain |
| \*F chain | Flushes the chain. Using this command is the same as sending a \-D command to each chain one by one |
| \*L chain | Lists the rules in the chain |
| \*N chain | Creates a new user-defined chain |
| \*X chain | Deletes a chain |
| \*P chain target | Sets the default target |

Additional options are available for customizing ipchains even further. But for the purposes of this example, these tables cover the majority of the options.

# ## Setting Up the Host or Gateway

If you are to provide IP masquerading, support for the feature must be compiled into the kernel. Most Red Hat releases already provide IP masquerading. However, you may need to enable some customized options. If you need assistance to compiling a kernel, refer to Chapter 14.

For your convenience, Listing 16.3 shows the major steps needed to compile a kernel with IP masquerading enabled. You will need to provide the IP masquerading options in the kernel yourself.

# ## Listing 16.3 The Basic Steps Needed to Compile a Kernel with IP Masquerading Enabled

```
    cd /usr/src/linux
    make config                # or chose one of the two below
        make menuconfig
        make xconfig
    make dep
    make bzImage
        # edit your /etc/lilo.conf file now.
    make modules
```