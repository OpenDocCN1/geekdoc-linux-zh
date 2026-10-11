```
```
Listing 16.4: continued
77:    }
78:     
79: /*
80:  * Accept this dgram request, and
81:  * launch the server:
82:  */
83:    log("Address %s port %d accepted.\n",
84:        str_addr, ntohs(adr_clnt.sin_port));
85:     
86: /*
87:  * inetd has provided argv[0] from the
88:  * config file /etc/inetd.conf; we have
89:  * used this to indicate the server's
90:  * full pathname for this example.  We
91:  * simply pass any other arguments and
92:  * environment as is.
93:  */
94:    log("Starting '%s'\n",argv[0]);
95:    log_close();    /* No longer need this */
96:     
97:    z = execve(argv[0],argv,envp);
98:     
99: /*
100:  * If control returns, then execve(2)
101:  * failed for some reason:
102:  */
103:    log_open(LOGPATH);     /* Re-open log */
104:    bail("execve(2), starting server");
105:    return 1;
106: }
```
```

The wrapper program shown in Listing 16.4 implements the following very simple security policy:

+   * If the client's address is 127.7.7.7, his request is allowed to go to the datagram server. No restriction upon client's port number is applied.
+   * If the client's address is any other IP address, the request is logged and denied.

# NOTE

The policy address of 127.7.7.7 was chosen as an example that all readers should be able to test (even those readers without an actual network established). The reader is encouraged to modify the program if he does have a network, in order to try out addi-tional policy rules.