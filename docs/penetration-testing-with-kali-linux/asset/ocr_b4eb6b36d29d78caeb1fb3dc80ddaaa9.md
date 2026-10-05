# OffSec Certificate (PAC)

Privileged Account Certificate (PAC)¹¹²⁰ validation¹¹²¹ is an optional verification process between the SPN application and the domain controller. If this is enabled, the user authenticating to the service and its privileges are validated by the domain controller. Fortunately for this technique, service applications rarely perform PAC validation.

As an example, if we authenticate an IIS server that is executing in the context of the service account iis, the IIS application will determine which permissions we have on the IIS server depending on the group memberships present in the service ticket.

With the service account password or its associated NTLM hash, we can forge our service ticket to access the target resource (in our example, the IIS application) with any permissions we desire. This custom-created ticket is known as a silver ticket¹¹²² if the service principal name is used on multiple servers, the silver ticket can be leveraged against them.

In this section, we'll create a silver ticket to get access to an HTTP SPN resource. We identified in the previous section, the iis_user account is mapped to an HTTP SPN. Therefore, the password of the user is used to create service tickets for it. For the purposes of this example, let's assume we've identified the iis_service user has an established session on CLIENT75.

In general, we need to collect the following three pieces of information to create a silver ticket:

+   * SPN password hash
* Domain SID
* Target SPN

Let's get started into the attack by connecting to CLIENT75 via RDP as jeff with the password HenchmanPutridBonbon11.

First, let's confirm if our current user has no access to the resource of the HTTP SPN mapped to iis_service. So do we, use iwr-DefaultCredentials so that the credentials we send are used by the web request.

```
PS C:\Users\jeff> iwr -DefaultCredentials http://web04
is:
401 - Unauthorized: Access is denied due to invalid credentials.
Server Error
```

> 401 - Unauthorized: Access is denied due to invalid credentials.
You do not have permission to view this directory or page using the credentials that you supplied.

```
At line:char:1
+ iwr-UseDefaultCredentials http://web04
```