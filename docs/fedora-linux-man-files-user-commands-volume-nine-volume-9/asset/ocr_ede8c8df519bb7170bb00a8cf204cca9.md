**cert.pem...**
    one or more certificates of sssage recipients: used when encrypting a sssage.

**-to, -from, -subject**
    the relevant mail headers. These are included outside the signed portion of a sssage so
    they may be included manually. If signing then many S/MIME mail clients check the
    signers certificate's email address matches that specified in the From: address.

**-purpose, -ignore_critical, -issuer_checks, -crl_check, -crl_check_all, -policy_check, -**
**extended_crl, -x509_strict, -policy -check_ss_sig -no_alt_chains**
    Set various options of certificate chain verification. See **verify** manual page for
    details.