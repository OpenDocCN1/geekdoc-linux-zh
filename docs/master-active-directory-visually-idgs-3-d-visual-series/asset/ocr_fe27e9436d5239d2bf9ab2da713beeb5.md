# Can there be more than one gateway?

Depending on your network configuration, you may have more than one gateway. You can think of the gateways as roads that lead out of the local subnet. The gateway allows communication to take place between different subnets. The gateway IP address refers to the router that can pass IP traffic onto another subnet. By providing the IP address of the gateway, clients can send packets bound for a different IP subnet directly to the gateway.

# How many IP addresses can I include in the exclusion range?

You can exclude as many IP addresses from the scope as desired by using the exclusion range. However, any excluded addresses are never available to clients for lease, so the general rule of thumb is to keep your exclusion range as small as possible.

![](bbox=[0.05, 0.51, 0.46, 0.82])

![](bbox=[0.5, 0.51, 0.9, 0.82])

+   - **13** This window enables you to configure scope options either now or later.
+   - **13** Click Yes to configure now.

+   - **14** Click Next to continue.

+   - **15** Enter the IP address for the default gateway.
+   - **16** Click Add.

+   - **17** Click Remove to remove existing default gateways, if necessary.
+   - **18** Click Next to continue.