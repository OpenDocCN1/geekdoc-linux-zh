```
GSP> co

CO
```

Leaving Guardian Service Processor Command Interface and entering Console mode. Type Ctrl-B to reactivate the GSP Command Interface.

GenericSysName [HP Release B.11.00] (see /etc/issue)
Console Login:

Anytime you are on the console, you can issue ^b and get access to GSP to issue any GSP commands and then get back to console mode with co.

The following is a list of GSP commands available on an N-Class system at the time of this writing. Although an L-Class system was used in the examples in this chapter, the GSP for the L-Class and N-Class are similar. Keep in mind that the GSP commands for your system may be somewhat different than those listed. GSP is updated occasionally, so the list for the N-Class may also be somewhat different than what is shown in Table 3-6.

# TABLE 3-6 List of GSP Commands for N-Class

| Command (Function) | Explanation |
| --- | --- |
| AR (Config) | Configure the Automatic System Restart. |
| CA (Config) | Configure Asynchronous and Modem parameters. |
| CE (Chassis Codes) | Log a chassis code in the SAS chassis code history. |
| CL (Console) | Display console history. |
| CO (Console) | Return to console mode. |