Table 9.11 What a remote machine or user needs to be able to gain ssh access.
|Option|Purpose|Values|
---|---|---|
|AccountExpireWarningDays|Specifies when to start printing messages warning that the account is about to expire.|A positive integer; the default is 14 days. 0 shuts off this feature.|
|ForcedEmptyPasswordChange|Forces a user to enter a password if either they left it blank or this is their first login. This is not a secure default.|Either **yes** or **no**; the default is **no**.|
|ForcedPasswordChange|Forces the user to change their password if it is expired.|Either **yes** or **no**; the default is **yes**.|
|IgnoreRhosts|Does not accept entries in ~/.rhosts or ~/.shosts as valid for authentication.|Either **yes** or **no**; the default is **no**.|
|IgnoreRootRhosts|Does not accept entries in ~/.rhosts or ~/.shosts as valid for authentication for a remote root login.|Either **yes** or **no**; the default is whatever you have IgnoreRhosts set to.|
|KerberosAuthentication|Specifies that Kerberos v5 authentication is accepted.|Either **yes** or **no**; the default is **yes**.|
|KerberosOrLocalPassword|Specifies whether a failed Kerberos authentication defaults to a regular password check.|Either **yes** or **no**; the default is **no**. It is not a good idea to change this default, because if Kerberos authentication fails, it means that the user may be an intruder.|
|KerberosTgtPassing|Specifies whether a Kerberos TGT can be passed to the ssh server.|Either **yes** or **no**; the default is **yes**.|
|PasswordAuthentication|Allows password authentication.|Either **yes** or **no**; the default is **yes**.|
|PasswordExpireWarningDays|Specifies when to start printing messages warning that the password is about to expire.|A positive integer; the default is 14 days. A 0 shuts off this feature.|
|PermitEmptyPasswords|Specifies whether the server allows login to accounts with empty passwords.|Either **yes** or **no**; the default is **yes**. It is often a good idea to change this value to **no**.|

(continued)