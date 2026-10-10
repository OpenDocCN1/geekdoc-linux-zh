# DIFFERENCES BETWEEN IPCHAINS AND IPFWADM

Some of these changes are a result of kernel changes and some a result of ipchains being different from ipfwadm.

+   - Many arguments have been remapped; capitals now indicates a command and lower-case now indicates an option.

+   - Arbitrary chains are supported, so even built-in chains have full names instead of flags (for example, input instead of -I).

+   - The -k option has vanished; use !-y.

+   - The -b option actually inserts/appends/deletes two rules, rather than a single bidirectional rule.

+   - The -b option can be passed to -C to do two checks (one in each direction).

+   - The -x option to -I has been replaced by -v.

+   - Multiple source and destination ports are not supported any-more. Hopefully being able to negate the port range will some-what make up for that.

+   - Interfaces can only be specified by name (not address). The old semantics got silently changed in the 2.1 kernel series anyway.

+   - Fragments are examined, not automatically allowed through.

+   - Explicit accounting chains have been done away with.

+   - Arbitrary protocols over IP are not tested for.

+   - The old behavior of SYN and ACK matching (which was previ-ously ignored for non-TCP packets) has changed; the SYN option is not valid for non-TCP-specific rules.

+   - Counters are now 64-bit on 32-bit machines, not 32-bit.

+   - Inverse options are now supported.

+   - ICMP codes are now supported.

+   - Wildcard interfaces are now supported.