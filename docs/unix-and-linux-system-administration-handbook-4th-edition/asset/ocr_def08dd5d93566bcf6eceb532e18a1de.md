# Table 20.26 DKIM signing options in Exim

| Option | Type | Req'd | Contents |
|---|---|---|---|
| dkim_domain | String | Yes | Domain to sign with |
| dkim_selector | String | Yes | Key selector (name) |
| dkim_private_key | String | Yes | Private key or filename that contains it |
| dkim_canon | String | No | Canonicalization method: simple or relaxed |
| dkim_strict | String | No | If true, signing errors defer mail back to queue |
| dkim_sign_headers | String | No | Headers to include in signature |

The first three "options" are required and must be configured; the rest are truly optional. By default, the canonicalization method (dkim_canon) is relaxed, messages that cause signing errors are sent without signatures (dkim_strict), and Exim uses the RFC4871 list of headers to sign (dkim_sign_headers). The mandatory options are straightforward, but if you have a complex site that hosts multiple real or virtual domains, you will have to be clever in defining them.

# Verifying incoming signed messages

Incoming DKIM-signed mail messages are verified in the acl_smtp_dkim ACL. This ACL is called once for each signature and returns one of the following codes:

+   - none – message is not signed
+   - invalid – signature could not be verified (key unavailable or invalid)
+   - fail – signature failed verification for headers, body, or both
+   - pass – signature is valid

The status is returned in the $dkim_verify_status variable, with failure details in $dkim_verify_reason. There are lots of other $dkim_variable tags that give you access to the various fields of the signature and allow you to implement special policies (e.g., flagging messages from gmail.com that do not have signatures, or rejecting messages from paypal.com that do not verify).

# A complete example

The following example is adapted from Phil Pennock's DKIM setup.22 It includes definitions of acl_process_dkim to verify signatures and a router and a transport (dnslookup_signed and remote_dksign, respectively) to do the actual signing.

This configuration allows multiple domains to be signed and provides for multiple keys so that key rollover is possible. This file is stored in CDB format and maps keys such as "example.org" to values such as "d200912".

Key selectors are named dyyyymm, where d is just the letter "d" for date, yyyy is the year the key was generated, and mm is the month it was generated. Key files are named rsa.private.selector.domain and are stored in a key directory defined