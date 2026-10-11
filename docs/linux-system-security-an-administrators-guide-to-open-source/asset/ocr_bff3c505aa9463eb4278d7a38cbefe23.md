# Fig. 11.3 RSA Authentication

![](bbox=[0.08, 0.08, 0.98, 0.38])

also be required to enter his or her passphrase each time this authentication procedure is utilized. The submission of passphrases can be accomplished automatically by using the ssh-agent program, discussed in *Managing RSA Authentication with ssh-agent and ssh-add* on page 301.

If this scheme is turned on and fails for any reason, then the sshd will prompt the user for an appropriate password based on compile-time options.

# NOTE

> The RhostsAuthentication, RhostsRSAAuthentication, and RSAAuthentica-
>   tion keywords discussed in the preceding sections were based on the values set in
>   */etc/ssh/sshd_config*. These keywords control the behavior of the server. How-
>   ever, they must be set to *yes* either by option to *ssh* at the command line, in
>   *SSH*.*/.ssh/config, or in */etc/ssh/ssh_config* on the client system in order for the cli-
>   ent to attempt to negotiate that particular authentication scheme. In other words, if
>   any of the aforementioned keywords is set to *no* on the client side, then the associ-
>   ated authentication scheme will never be attempted; whereas, if any of the afore-
>   mentioned keywords is set to *no* on the server side, then the authentication scheme
>   is not allowed.

# What Are All Those Keys, Again?

Keeping track of all the keys used by SSH is a bit difficult. Table 11.1 lists the keys associated with SSH, details about how they are generated and how long they last, and their purpose. This table provides a handy quick reference of the SSH keys.

# Compiled Authentication Scheme.

If you have compiled *ssh* (see *Compiling SSH* on page 265) with a special authentication mechanism, such as TIS or SecurID, then that scheme may be invoked whenever the appropriate key-words are set in */etc/ssh/sshd_config* and */etc/ssh/ssh_config* files. If so