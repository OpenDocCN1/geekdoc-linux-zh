The sendmail program responds with the indented lines after receiving input. If you try to send e-mail to an unknown domain, sendmail complains because it also does name server lookups and attempts to resolve the domains, in most cases, before sending the e-mail. If sendmail cannot resolve a domain, it will either complain or place the mail in the queue for a later lookup.

If the mail went through just fine, then sendmail is operational on your system. You can now begin doing some tweaking to optimize its performance.

# ## Customizing the sendmail.cf File

You can tweak quite a few variables in the sendmail.cf file. Most are preceded by comments that explain the variables. Listing 17.2 shows just a few of the options that I find myself needing to adjust depending on the function of the Linux machine. You may customize these options to suit your own machine.

# ### Listing 17.2 Options within the sendmail.cf File That You Can Configure to Optimize the sendmail Program to Your Own Needs

```
```text
# maximum message size
O MaxMessageSize=2500000

# This sets the maximum size at 2.5 megabytes.  The default is set
at one megabyte.

# No email over 2.5 megabytes in size   will be allowed to pass.
# privacy flags
O PrivacyOptions=goneaway
# This adjusts the types of connections users from outside might run
into.

# default UID (can be username or userid:groupid)
O DefaultUser=1:1

# If you want to run sendmail as root, the above settings will work.
# Remember that UID and GID 1 are both reserved for root.
# Here you can place an alternate user to run sendmail.
# maximum number of recipients per SMTP envelope
O MaxRecipientsPerMessage=100
# This option prevents a user from sending out emails to more than
100 people using the single email they wrote.
# This prevents those sending out spam and junk emails.
```
```