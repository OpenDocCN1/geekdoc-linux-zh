# # Choosing Grsec Features

Grsec includes more than a few features, not all of which are relevant to every situation. Some of the features available with Grsec are specialized to certain situations, and some are very advanced, requiring extensive additional configuration to work properly. Enabling some of the Grsec options is simply a matter of turning them on within the kernel configuration. This section examines the Grsec options.

# ## SECURITY LEVEL

Grsec enables you to select one of four security levels, three of which are predefined. The predefined security levels include Low, Medium, and High, with the fourth level called Customized. One method for evaluating Grsec and its features is to apply the Low Security Level, compile, and run with the kernel as such. If you notice no ill effects of running with the Grsec-Enhanced Low Security Level, apply the Medium Security Level, compile, and run with that. Increase the security level to the highest level possible.

Recommendation:
Choose one of the default provided security levels and increase as much as possible, or choose a customized level and work through the other options contained in this section.

# ## PAX CONTROL

Pax Control provides a means to defend against certain types of exploits that attack a program's address space. For instance, Pax Control can give protection against both stack and heap-based buffer overflows, among other things. Also included is integration between Pax and Mandatory Access Control (MAC) functions.

Recommendation:
Use your discretion. Some of the Pax options can be more involved to configure properly.

# ## ADDRESS SPACE PROTECTION

Address Space Protection provides many useful options that can enhance security, including prevention of methods to inject code into a running monolithic kernel. Some of the options included within Address Space Protection can break applications, most notably X Windows. Therefore, if you use X Windows, extra caution should be taken when choosing Address Space Protection options.

Recommendation:
Enable these options unless you're running X Windows. If you're running X Windows, be wary of these options. These protections are great enough that it is worth a potential recompile in case one of the options breaks an application.