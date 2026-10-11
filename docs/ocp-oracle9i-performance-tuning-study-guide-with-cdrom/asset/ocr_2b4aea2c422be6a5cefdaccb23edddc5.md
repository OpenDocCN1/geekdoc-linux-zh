In Oracle⁹ⁱ the overall size of the SGA is defined by a single `init.ora` parameter: `SGA_MAX_SIZE`. Within this maximum, two of the individual components of the SGA—Shared Pool and Database Buffer Cache—can be dynamically resized using the ALTER SYSTEM command without shutting down and restarting the instance. If the value for `SGA_MAX_SIZE` is less that the sum of its components at instance startup, Oracle will ignore the setting for `SGA_MAX_SIZE` and use the sum of the components as the value instead.

![](bbox=[0.13, 0.26, 0.2, 0.33])

As of this writing, neither the Large Pool nor the Java Pool can be dynamically resized using the ALTER SYSTEM command. However, Oracle has hinted that this may be an enhancement in subsequent releases of Oracle⁹ⁱ.

In order to achieve this dynamic SGA management, a new unit of SGA storage, the granule, was added to the Oracle architecture model. In Oracle⁹ⁱ, memory within the SGA is divided into units called granules. A granule is a piece of contiguous virtual memory allocated within the SGA. The size of each granule varies according to the overall size of the SGA as defined by the `init.ora` parameter `SGA_MAX_SIZE`. Table 1.4 shows the two possible sizes for SGA granules.

# **TABLE 1.4** SGA Size and Granule Size

| **Total SGA Size** | **Granule Size** |
| Less than 128MB | 4MB |
| 128MB or larger | 16MB |

When the instance is initially started, granules equal to the value specified by `SGA_MAX_SIZE` are created within the SGA. Each SGA component then acquires the space it needs by utilizing these available granules. Oracle enforces minimum granule requirements for each SGA component. These minimum values are shown in Table 1.5.

![](bbox=[0.13, 0.8, 0.2, 0.88])

The minimum SGA size of an Oracle⁹ⁱ SGA is three granules, or 12MB.