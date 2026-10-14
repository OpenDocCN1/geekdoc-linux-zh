# 8.7 Using EVM

This section will not attempt to cover every possible function within the EVM subsystem; instead, it will discuss some of the interesting uses we have discovered and how they relate to the TruCluster Server product. For more in depth analyses of EVM, we suggest the Tru64 UNIX System Administration Guide, or the following reference pages:

+   - evmget(1)
+   - evmpost(1)
+   - evmsort(1)
+   - evm(5)
+   - EvmFilter(5)
+   - evmstart(8)
+   - evmviewer(8)

+   - evminfo(1)
+   - evmshow(1)
+   - evmwatch(1)
+   - EvmEvent(5)
+   - evmreload(8)
+   - evmstop(8)

A complete list of reference pages can be obtained by using the "man -k" command, or our section-based sman script (see Appendix B for where to get it).

# 8.7.1 How Can I Find Out Which Events are Registered with EVM?

You can retrieve the registered events by using the evmwatch command with the "-i" switch.

> NOTE:

Prior to Tru64 UNIX version 5.1, the "-A" command option did not exist for the evmwatch and evmget commands. The "-A" switch added to the evmwatch command automatically invokes evmshow, whereas the evmget command automatically invokes the evmsort command. If you are using Tru64 UNIX version 5.0A, use the following command in place of the "-A" command option to evmwatch:

```
# evmwatch -i | evmshow
```

```
# evmwatch -A -i
```