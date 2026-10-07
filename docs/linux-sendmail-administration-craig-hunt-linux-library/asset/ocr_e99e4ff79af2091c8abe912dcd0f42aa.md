# Chapter 5 Understanding a Vendor's Configuration

canonify input: craig
Canonify2 input: craig
Canonify2 returns: craig
canonify returns: craig
1 input: craig
1 returns: craig
HdrFromL input: craig
AddDomain input: craig
AddDomain returns: craig < @LOCAL*
MasqHdr input: craig < @ @LOCAL*
MasqHdr returns: craig < @wren . foobirds . org .
HdrFromL returns: craig < @wren . foobirds . org .
final input: craig < @wren . foobirds . org .
final returns: craig < @wren . foobirds . org
> ^D

We run two tests using Sendmail -bt mode. In both cases we use a header/address, and we give it the address craig to process through the local mailer. The first test uses the generic-linux.cf configuration, which does not use the always_add_domain feature. The address goes in as comes out craig. In the second test we use the redhat.cf configuration, which uses the always_add_domain feature. In this test, craig is converted to craig@wren.foobirds.org. The effect of always_add_domain is clearly shown.

This is a good feature to use. The address shown, on local mail, is valid everywhere. This helps avoid confusion among your users, and confused users you want to avoid!

access_db This feature allows Sendmail to use the access database to decide what hosts, domains, and networks are acceptable sources of e-mail. An optional argument that defines the database type and path can be used with the access_db feature. The default database type is hash and the default path is /etc/mail/access. The access database is described in Chapter 6. In its fighting spam is covered in Chapter 11.

blacklist_recipients This feature allows the access database to be used to block mail from specific recipients. Normally, the access database is used to control mail from undesirable sources. With this feature, the access database also can be