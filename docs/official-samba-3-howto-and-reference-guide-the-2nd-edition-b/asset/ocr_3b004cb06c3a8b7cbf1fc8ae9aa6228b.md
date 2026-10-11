This parameter determines whether or not smbclient(8) will attempt to authenticate itself to servers using the NTLMv2 encrypted password response.

If enabled, only an NTLMv2 and LMv2 response (both much more secure than earlier versions) will be sent. Many servers (including NT4 < SP4, Win9x and Samba 2.2) are not compatible with NTLMv2.

Similarly, if enabled, **NTLMv1**, **client lanman auth** and **client plaintext auth** authentication will be disabled. This also disables share-level authentication.

If disabled, an NTLM response (and possibly a LANMAN response) will be sent by the client, depending on the value of **client lanman auth**.

Note that some sites (particularly those following ‘best practice’ security policies) only allow NTLMv2 responses, and not the weaker LM or NTLM.

# **client plaintext auth** **(G)**  Default: *client plaintext auth* = *yes*

Specifies whether a client should send a plaintext password if the server does not support encrypted passwords.

# **client schannel** **(G)**  Default: *client schannel* = *autoyes*

Example: *client schannel* = *yes*

This controls whether the client offers or even demands the use of the netlogon channel. *client schannel* = *no* does not offer the channel, *client schannel* = *auto* offers the channel but does not enforce it, and *client schannel* = *yes* denies access if the server is not able to speak netlogon channel.

# **client signing** **(G)**  Default: *client signing* = *auto*

This controls whether the client offers or requires the server it talks to to use SMB signing. Possible values are *auto*, *mandatory* and *disabled*.

When set to auto, SMB signing is offered, but not enforced. When set to mandatory, SMB signing is required and if set to disabled, SMB signing is not offered either.

# **client use spnego** **(G)**  Default: *client use spnego* = *yes*

This variable controls whether Samba clients will try to use Simple and Protected NEGociation (as specified by rfc2478) with supporting servers (including Windows×P, Windows×000 and Samba 3.0) to agree upon an authentication mechanism. This enables Kerberos authentication in particular.

# **comment** **(S)**  Default: *comment* = *No comment Fred’s Files*

Example: *comment* = *Fred’s Files*