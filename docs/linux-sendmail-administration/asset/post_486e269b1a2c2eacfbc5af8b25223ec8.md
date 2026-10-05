
# Running Sendmail in Test Mode

The values are generally used in pairs to create the following four settings:

- HS This flag pair requests header sender address processing.
- HR This flag pair requests header recipient address processing.
- ES This flag pair requests envelope sender address processing.
- ER This flag pair requests envelope recipient address processing.

I recommend that you follow the standard practice and set all flags in pairs. There are two reasons I recommend this. First, Sendmail uses flags in pairs. If you don't explicitly set a value for one of the flags, Sendmail will use the value it has for that. Second, flags are "sticky"—when a flag is set, it stays set until explicitly reset. If you would have to keep track of the flag values if you have been fiddling with things. Thus, it is much simpler to be explicit, and set the values before you run the test.

The /tryflags affect both /parse and /try, but they don't all make sense for the /parse command. The first thing that /parse does is process the address as a delivery address. Only recipient addresses can be delivery addresses. Using the sender address to select the mailer that will be used doesn't make sense, in any real situation the sender and the recipient will not be the same address for this, while /tryflags values affect /parse ER and HR are truly useful.

# Testing with the /try Command

The /try command, on the other hand, makes effective use of all /tryflags values. The /try command essentially performs the same processing as the second half of the /parse command. The /try command takes an address and processes it for a mailer. Unlike the /parse command that selects the mailer based on the address provided, you tell the /try command which mailer it should use. Listing 10.10 shows the /try command and the impact /tryflags has on.

# Listing 10.1 Using /try to Process an Address for a Mailer

```
[root]# sendmail -bt
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter <ruleset> <address>
> /tryflags HR
/try esmtp al@bird.org for mailer esmtp
canonify input: al @ bird . org
canonify2 input: al < @ bird . org>
canonify2 returns: al < @ bird . org . >
```

![](img/b8082498451dba2bf0cf2907c85c4c83_305_0.png)

# Chapter 10 Testing Sendmail

```
canonify returns: al1 <@ bird . org . >
2 input: al1 <@ bird . org . >
2 returns: al1 <@ bird . org . >
EnvSMTP input: al1 <@ bird . org . >
PseudoToReal input: al1 <@ bird . org . >
PseudoToReal returns: al1 <@ bird . org . >
MasqSMTP input: al1 <@ bird . org . >
MasqSMTP returns: al1 <@ bird . org . >
EnvSMTP input: al1 <@ bird . org . >
final returns: al1 @ bird . org
Rcode = 0, addr = al1@bird.org
>/tryflags HS
>/try esmtp craig
Trying header sender address craig for mailer esmtp
canonify input: craig
Canonify2 input: craig
Canon2 returns: craig
canonify returns: craig
1 input: craig
1 returns: craig
HdrFromSMTP input: craig
PseudoToReal input: craig
PseudoToReal returns: craig
MasqSMTP input: craig
MasqSMTP returns: craig < @*LOCAL*>
Masqdr input: craig < @*LOCAL*>
Masqdr returns: craig < @w . foobirds .org . >
HdrFromSMTP returns: craig < @w . foobirds .org . >
final input: craig < @w . foobirds .org . >
final returns: craig < @w . foobirds .org
Rcode = 0, addr = craig@w.foobirds.org
>/quit
```

In Listing 10.2, two different addresses are processed. First, we use /tryflags to HR to process the header recipient address, and use /try@al.org for the esmtp mailer. You will notice that the results are very similar to those we saw in the /parse test in Listing 10.9. Next, we set the /tryflags to HS and use /try to process craig as a header address for the esmtp mailer. This is a realistic test that shows the processing would have happened to the sender address and the recipient address for the headers on a specific piece of mail. The sender and recipient address on a single piece of mail always go through the same mailer, because only the recipient address is used to select the mailer.

The /try command ends by displaying a return code (RCode) and the final address after processing is complete. A return code of zero means that everything went okay. A non-zero return code means that a potential delivery problem was encountered. Running an address that produces a non-zero return code through /parse will produce an error message describing the return code, as we saw earlier.

I find that I use /try much more than I use /parse. Most of the configurations I work with use a limited number of mailers, usually esmtp for external mail and local for internal mail. I usually know what mailer will handle the mail without asking Sendmail. The /parse command is most useful when you have several different mailers. A great time to use /parse is when you have a complex configuration, the /parse command tells you which mailer Sendmail will use and then processes the recipient address for mailer. You can then process the sender address with /try.

# Display and Setting Internal Values

The tests in 10.8, 10.9, and 10.10 show test mode used to process an address through some rules. Test mode can also be used to examine the contents of sendmail.cf variables and classes, and to query for runtime information, and to set values to see how they affect the operation of the system, which is exactly what is done in Listing 10.11.

# Setting Variables and Classes

```
$m
>/try esmtp craig@wren.foobirds.org
Trying header sender address craig@wren.foobirds.org for mailer esmtp
canonify input: craig @ wren . foobirds . org
... lines deleted ...
final returns: craig @ wren . foobirds . org
Rcode = 0, addr = craig@wren.foobirds.org
$m
foobirds.org
>/try esmtp craig@wren.foobirds.org
Trying header sender address craig@wren.foobirds.org for mailer esmtp
canonify input: craig @ wren . foobirds . org
... lines deleted ...
```

# Chapter 10 Testing Sendmail

final returns: craig @ wren . foobirds . org
Rcode = 0, addr = craig@wren.foobirds.org
>/try smtp sara@hawk.foobirds.org
Trying header sender address sara@hawk.foobirds.org for mailer smtp
canonify input: sara @ hawk . foobirds . org
... lines deleted ...
final returns: sara @ hawk . foobirds . org
Rcode = 0, addr = sara@hawk.foobirds.org
> $=w
wren.foobirds.org
localhost
127.0.0.1
> $=M
> .CMhawk.foobirds.org
> .CMibis.foobirds.org
> .CMowl.foobirds.org
> $=M
isbis.foobirds.org
owl.foobirds.org
hawk.foobirds.org
> /try smtp sara@hawk.foobirds.org sara@hawk.foobirds.org for mailer smtp
canonify input: sara @ hawk . foobirds . org
... lines deleted ...
final returns: sara @ hawk . foobirds . org
Rcode = 0, addr = sara@hawk.foobirds.org

Listing 10.11 an excerpt from the middle of a long sendmail -bt run. The first line shows us the contents of a variable. $m asks for the values stored in variable m. From Chapter 9 we know that m contains the masked value. When it is empty, masking is turned off. The first /try test processes the address craig@wren.foobirds.org as a header sender address. The output of the final ruleset shows that the address is not masked. We then store the value foobirds in variable m using the command .Dfobirds.org, where .D is the command, m is the variable name, and foobirds is the value. A second /try test with the address craig@wren.foobirds.org returns the masked address craig@foobirds.org. We changed the Sendmail configuration and observed the impact of the change in real time.

Next, we run another /try test to see if the address sara@hawk.foobirds.org is masked. It isn't, because it is not defined in class w or class M. We use $=w to display all of the values in w. wren.foobirds.org is there, so why it is masqueraded. But hawk.foobirds.org is not in class w. We also check class M with the $M command. That class is empty. We then use three .C to add values to class M. The first of these, .Cm.foobirds.org, where .C is the command, M is the class, and hawk.foobirds.org is the value, adds hawk to class M. After the commands are entered, $M displays three values for class M. A second /try with the address sara@hawk.foobirds.org shows that hawk is now masqueraded.

The changes we make to the Sendmail configuration using .D and .C commands only as long as the sendmail -bt run. When we terminate the run, these temporary changes vanish. Setting values in test mode allows you to observe the effect of potential configuration changes before you make the changes.

In Listing 10.12, we don't actually change configuration values. In this example, we ask Sendmail to display the values it obtains from external information sources.

# Listing 10.12 Requesting Outside Information from Sendmail

```
> /mx foobirds.org
getxr(foobirds.org) returns 2 value(s):
wren.foobirds.org.
parrot.foobirds.org.
> /canon redbreast
getanname(redbreast) returns robin.foobirds.org
> /map generics kathy
map_lookup: generics (kathy) returns kathy.mcafferty (0)
```
