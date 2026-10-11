+   2. Identify the bad characters that cannot be included in the payload and return address.

# 12.6 Finding a Return Address

As a final step, we need to find a valid assembly instruction to redirect code execution to the memory location pointed to by the ESP register. The EDB debugger comes with a set of plugins, one of which is named *OpcodeSearcher*.

![](bbox=[0.14, 0.25, 0.88, 0.49])

Figure 231: The *OpcodeSearcher* plugin for EDB

Using this plugin, we can easily search for a JMP ESP instruction or equivalent in the memory region where the code section of the crossfire application is mapped: