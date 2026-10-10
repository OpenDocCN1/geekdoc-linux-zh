# Table 2.25 (continued)

| OPTION | DESCRIPTION |
| :--- | :--- |
| RequiredAuthentications (Shown in Figure 4.6 and 4.7 with the Password Authentication drop down box or the Public Key drop down box) | Identifies the types of authentication methods that are required for authentication. If the value is empty, any values in AllowedAuthentication will be honored. |
| AuthInteractiveFailureTimeout (sshd2_config file only) | Identifies the number of failures a keyboard-interactive session may have. |
| AuthKbdInt.NumOptional (sshd2_config file only) | Identifies the number of submethods required before valid authentication. |
| AuthKbdInt.Optional (sshd2_config file only) | Identifies the optional submethod that Keyboard-Interactive will use. The options can be SecureID, plugin, and password. |
| AuthKbdInt.Required (sshd2_config file only) | Identifies the required submethods that must be present in order for valid authentication. |
| AuthKbdInt.Retries (sshd2_config file only) | Identifies the number of retries a user can attempt the keyboard-interactive process in order to authenticate to the SSH server. |

# Host Restrictions

The Host Restrictions section of the sshd2_config file should look like the following:

```
#    AllowHosts
#    DenySHosts
```

The Host Restrictions section of the SSH configuration GUI should look like Figure 2.10.