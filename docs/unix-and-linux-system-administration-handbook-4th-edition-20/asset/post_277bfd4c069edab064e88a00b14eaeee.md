
## DKIM in sendmail

You can implement DKIM for sendmail by using either filters (in-line filtering; see page 767) or a dual-server setup in conjunction with amavisid. Here we cover the use of DKIM-milter to sign and verify messages.

sendmail's configuration primitives `masqueraded_as` and `genericstable` rewrite headers, those primitives must be implemented before any DKIM signature is added; otherwise, the signature will not remain valid.

To support DKIM, sendmail must be built with milter support, the OpenSSL and Berkeley DB libraries available, and the DKIM-milter package installed (it found at sourceforge). Use OpenSSL to generate keys, and add them to your DNS name as described on page 591, or use dkim-genkey as shown on page 846.

```bash
$ dkim-testkey -k /var/db/dkim/email.key.pem -s ma
```

If all's well, dkim-testkey says nothing.

In your sendmail configuration file, `sendmail.mc`, add the line
`INPUT_MAIL_FILTER('dkim-filter', 'S=inet:8891@localhost')`

and rebuild the `sendmail.cf` file (/Build sendmail.cf: `sudo make install-cf`). Then restart sendmail and start the dkim-filter program.

## DKIM in Exim

The Exim 4.70 release (late 2009) added native support for DKIM and dropped support for Yahoo!'s DomainKeys. Expect the feature set to continue to evolve as the Exim developers work out bugs and gain experience with DKIM.

Exim's DKIM support is enabled by default. To turn it off, set `DISABLE_DKIM=in` in `Local/Makefile` and rebuild and reinstall the package.

The Exim implementation sends outgoing messages in the SMTP transport configuration and verifies signatures on incoming messages through a new ACL, `acl_smtp_dkim`. Hub machines can disable the signature verification on messages they relay for local hosts by setting `dkim_disable_verify` for those messages.

## Signing outgoing messages

The first DKIM implementation chore is to generate your cryptographic keys with OpenSSL as described on page 591 (in the DNS chapter). Several new Exim options must be defined for use by the SMTP transport. The options can include variables to be expanded when the transport is called. Table 20.26 contains a list of the DKIM-related signing options.

## A complete example

### DKIM signing options in Exim

| Option Type | Req'd | Contents |
|---|---|---|---|
| dkim_domain | String | Yes | Domain to sign with |
| dkim_selector | String | Yes | Key selector (name) |
| dkim_private_key | String | Yes | Private key or filename that contains |
| dkim_canon | String | No | Canonicalization method |
| dkim_strict | String | No | If true, errors defer mail back to queue |
| dkim_sign_headers | String | No | Headers to include in signature |

The first three “options” are required and must be configured; the rest are optional. By default, the canonicalization method (`dkim_canon`) is relaxed, messages that cause signing errors are sent without (`dkim_strict`), and Exim uses RFC4871 list of headers to sign (`dkim_sign_headers`). Mandatory options are straightforward, but if you have a complex site that hosts real or virtual domains, you will have to be clever in defining them.

### Verifying incoming signed messages

Incoming DKIM-signed mail messages are verified in the `acl_smtp` acl. This ACL is called for each signature and returns one of the following codes:

- none – message is not signed
- invalid – signature could not be verified (key unavailable or invalid)
- fail – signature failed verification for headers, body, or both
- pass – signature is valid

The status is returned in the `$dkim_verify_status` variable, with failure details in `$dkim_verify_reason`. There are lots of `$dkim_variable` tags that give access to the various fields of the signature and allow you to implement special policies (e.g., flagging messages from gmail.com that do not have signatures, or rejecting messages from paypal.com that do not verify).

### A complete example

The following example is adapted from Phil Pennock’s DKIM setup. It includes definitions of `acl_process_dkim` to verify signatures and a router and transport (`dnslookup_signed` and `remote_dksnim`, respectively) to the actual signing.

This configuration allows multiple domains to sign.
