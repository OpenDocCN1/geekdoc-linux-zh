Then you can choose a vDC from options based on your entitlements within that
environment.

# Connecting to vCloud Air

Connecting to vCloud Air became a very simple task with the release of PowerCLI
6.0 R1. PowerCLI 6.0 R1 introduced cmdlets that allow you to connect and discon-
ect from vCloud Air: `Connect-PSIServer` and `Disconnect-PSIServer`.

The cmdlets allow you to log into your vCloud Air account without having to spec-\ify a vCloud Director API URL or vCloud Org based on your entitlements in thosenenenvironments. `Connect-PSIServer` requires only your username and password. There
are three ways that you can connect to vCloud Air with this cmdlet. The first is hard-
coding your username and password in the command. This approach is not recomm-
mended for scripts, but if you are logging into vCloud Air manually, you would type
it out like this:

```
Connect-PSIServer -User BrianGraf@contoso.com -Password VMware!
```

The second method uses the -Credential parameter with the Get-Credential
cmdlet to prompt for the username and password upon execution:

```
Connect-PSIServer -Credential (Get-Credential)
```

The third method leverages the Credential Store. Beginning with PowerCLI 4.1,
VMware included what is known as the Credential Store, which is populated
withVICentialStoreItems. These items, which are encrypted and encrypted
for in the `${env:APPDATA}\VMware\credentialstore\credentials.xml` file on your
local machine. Using the Credential Store, you can input your username and pass-
word for a given once, which can then be used to connect to hosts with
much less effort:

```
New-CredentialStoreItem -Host vchs.vmware.com -User BrianGraf@
contoso.net *
-Password VMware!
```

This Credential Store code sets the username and password for the host, vchs.
vmware.com, so that any future attempts to log into vCloud Air using the Connect-
PSIServer cmdlet will not require credentials. You can also store your vCloud Air
credentials in the Credential Store using the Connect-PSIServer cmdlet and by add-
ing the -SaveCredentials parameter, which will eliminate the need to run the New-
VICentialStoreItem command.