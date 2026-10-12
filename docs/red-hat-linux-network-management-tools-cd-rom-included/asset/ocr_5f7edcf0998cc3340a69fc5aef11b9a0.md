![](bbox=[0.2, 0.07, 0.85, 0.55])

**Figure 7.2 Agent pass function.**

When an SNMP get-request is received by the agent, it calls the passtest script with the -g option, followed by the MIB OID. Thus, the agent will call the script:

/bin/sh /usr/local/passtest -g 1.3.6.1.4.1.2021.255

When the agent receives a getnext-request, the -n option is used instead of -g. With an SNMP set-request, the -s option plus the type and value of the MIB object will be supplied. These options are supplied to the script so that it can take the correct action based on the different requests.

The script is also responsible for generating the appropriate output to satisfy the SNMP request and the requirements of the agent. For instance, when an SNMP getnext-request is sent to the agent, the next OID after the supplied OID must be presented. The for-