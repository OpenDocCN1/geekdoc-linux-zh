# 252

The possible data types and their formats are listed below.

| Data Type | Format | dhcp_inititab(4) Type |
| --- | --- | --- |
| Unsigned Number | One or more decimal digits | UNNUMBER8, UNNUMBER16, UNNUMBER32, UNNUMBER64 |
| Signed Number | One or more decimal digits optional, preceded with a minus sign | SNNUMBER8, SNNUMBER16, SNNUMBER64 |
| IP Address Octet | Dotted-decimal notation | IP OCTET |
| String | The string 0XR followed by a two-digit hexadecimal value Zero or more ASCII characters | ASCII |

# Options

+   -c Display the output in a canonical format. This format is identical to the OCTET format with a granularity of 1. New in the Solaris 8 release.

+   -i interface In general, you should need to use this option on hardware with two or more interfaces configurable by DHCP, and for a parameter that is interface specific.

+   -n limit When the tag is one with a list of values, limit the number printed.

# Operands

+   -code Numeric code for the requested DHCP parameter as defined by the DHCP specification. Vendor options are specified by adding 256 to the actual vendor code. New in the Solaris 8 release.

+   -identifier Mnemonic request for the DHCP parameter as listed in dhcp_inititab(4).

# Exit Status

+   -0 Successful operation.
-2 DHCP was not successful. The DHCP agent may not be running, the interface might have failed to configure, or no satisfactory DHCP responses received.
-3 Bad arguments.
-4 A timer was set with wait (see ifconfig(1M)), and the interface had not configured before it expired.
-6 Some system error (should never occur).