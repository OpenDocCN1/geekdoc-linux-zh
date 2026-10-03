```
# Notes:
# 1.      You can add comments after the pound sign (#) anywhere on a line.
# 2.      Rules are matched in descending order: first rule through the last rule.
# 3.      Rules can be continued to a new line by using the backslash (\\) before
#         the carriage return.
# 4.      Don't use the "*" character or other shell wildcards, because the rules
#         file is interpreted by a Bourne shell script.
#
################################################################################
#
# RULE_KEYWORD AND RULE_VALUE DESCRIPTIONS
#
#
#       rule_keyword  rule_value Type    rule_value Description
# ---------------  ----------  ----    -----------------------
#       any      minus sign (-) always matches
#       arch    text    system's architecture type
#       domainname    text    system's domain name
#       disksize  text range    system's disk size
#               disk device name (text)
#               disk size (MBytes range)
#       hostname  text    system's host name
#       installed text text    system's installed version of Solaris
#               disk device name (text)
#               OS release (text)
#       karch text    system's kernel architecture
#       memsize   range    system's memory size (MBytes range)
#       model text    system's model number
#       network   text    system's IP address
#       totaldisk range    system's total disk size (MBytes range)
#
#
################################################################################
#
# RULE EXAMPLES
#
# The following rule matches only one system:
#
#hostname sample_host     -     host_class     set_root_pw
#
# The following rule matches any system that is on the 924.222.43.0 network
# and has the sun4u kernel architecture:
#     Note: The backslash (\\) is used to continue the rule to a new line.
#
#network 924.222.43.0 && \
#        karch sun4c     -     net924_sun4u     -
#
# The following rule matches any sparc system with a c0t3d0 disk that is
# between 400 to 600 MBytes and has Solaris 2.1 installed on it:
#
#arch sparc && \
#        disksize c0t3d0 400-600 && \
#        installed c0t3d0s0 solaris_2.1 - upgrade  -
```