![](bbox=[0.175, 0.93, 0.826, 0.47])

Very nice! We successfully cracked the NTLM hash and used the password to log in via RDP.

In this section we obtained a basic understanding of the SAM and NTLM hashes. We also demonstrated how we can use Mimikatz to obtain NTLM hashes and followed our cracking methodology to crack the hash.

While we did all of this on a local system without an Active Directory environment, this process applies to enterprise environments and is a crucial skill for most real-life penetration tests. In the next section we will demonstrate how we can leverage NTLM hashes even if we are unable to crack them.

# 13.3.2 Passing NTLM

In the last section, we obtained an NTLM hash and cracked it. Depending on the strength of the password this may be time-consuming or unfeasible. In this section, we'll demonstrate how we can leverage an NTLM hash without cracking it.

First, we will demonstrate the pass-the-hash (PtH) technique. We can use this technique to authenticate to a local or remote target with a valid combination of username and NTLM hash rather than a plaintext password. This is possible because NTLM/LM hashes are not saved and remain in session memory. Moreover, if we discover a password hash on one target, we can use it to not authenticate to that target, but to another target as well, as the second target has an account with the same username and password. To leverage this into code execution of any kind, the account also needs administrative privileges on the second target.