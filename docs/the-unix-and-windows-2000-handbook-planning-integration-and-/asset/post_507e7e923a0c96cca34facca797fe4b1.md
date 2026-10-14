
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter <ruleset> <address>
>

Every message is processed by Sendmail using the options, configurations, and rulesets contained in the sendmail.cf file. Rulesets consist of an S# configuration command, which signifies the start of a rule (a number is inserted for the # sign). Lines beginning with an R signify a rule line and become part of the previous S# ruleset. An example of Ruleset 3 is provided below:

```
######################################
### Ruleset 3 - Name Canonicalization ###
######################################
S3

# handle null input (translate to <@> special case)
R $@               $: @ $@

# strip group: syntax (not inside angle brackets!) and trailing semicolon
R$* < $* > $* <@>   $: $1 < $2 > $3          mark addresses
R@ $* <@>           $: @ $1                 unmark <addr>
R$* :: $* <@>       $: $1 : $2              unmark @host...
R: include: $* <@>  $: : include: $1         unmark :include:
RS* [ $* : $* ] <@> $: $1 [ $2 : $3 ]        unmark IPv6 addrs
RS* : $* [ $* ]     $: $1 [ $2 [ $3 ] <@>    remark if leading colon
RS* : $* <@>        $: $2                   strip colon if marked
RS* <@>             $: $1                   unmark
RS* :               $: $1                   strip trailing sem
S10
```

There are three values contained on the rule line. The first field, or left-hand side (lhs), is matched against the sender/recipient address on the message. The second field, or right-hand side (rhs), is expanded if the lhs matches the address. The final field is optional and contains comments. The rules are processed in order until a match is found.

Next you will need to enter rulesets and addresses. The following brief description of rulesets is in order of processing by Sendmail. Ruleset 3 performs pre-processing on the sender and recipient addresses to make them legible to the Sendmail program. Ruleset 0 determines which MDA will be utilized for each recipient address. Ruleset 1 processes the sender address, and Ruleset 2 processes all recipient addresses. Ruleset 4 processes all addresses and converts them from internal to external representations. Finally, Ruleset 5 processes all local addresses that have not been aliased to allow for selection of a different delivery agent (examples include forwarding to other types of networks or using a firewall as a mail exchanger to protect “interior” machines).

Ruleset 0 does the most important work of determining how the message will be sent. Ruleset 0 returns a tuple that is made up of the keys in Table 9.3. The first key determines the delivery agent. Email addresses not local to your domain in the recipient field should return ESMTP. For recipients local to your domain, Ruleset 0 will return the local delivery agent. We will use Rulesets 3 and 0 in all of our examples. You can enter a single ruleset or multiple rulesets (separate with commas), but only one address.

The first example (Listing 9.4) tests the address of local user joe.

### Table 9.3 Ruleset 0 Output Fields

| Key | Definition (Value is all text following the key, ignoring spaces and not including the next key.) |
| --- | --- |
| $# | Delivery agent |
| $@ | Host |
| $: | User |

### Listing 9.4 Ruleset Output for Local User

```
> 3.0 joe
rewrite: ruleset 3 input: joe
rewrite: ruleset 96 input: joe
rewrite: ruleset 96 returns: joe
rewrite: ruleset 3 returns: joe
rewrite: ruleset 0 input: joe
rewrite: ruleset 199 input: joe
rewrite: ruleset 199 returns: joe
rewrite: ruleset 98 input: joe
rewrite: ruleset 98 returns: joe
rewrite: ruleset 198 input: joe
rewrite: ruleset 198 returns: $# local $: joe
rewrite: ruleset 0 returns: $# local $: joe
>
```

Rulesets can internally call other rulesets. In our example, Rulesets 3 and 0 both call other rulesets. The important information for this example is what Ruleset 3 and 0 return. Ruleset 3 returns joe, which is what you want for a local user. Ruleset 0 returns only two pieces of information: The delivery agent of local and the user joe. Since this is a local delivery, there is no requirement for a host. This output indicates that your sendmail.cf file is configured correctly for local deliveries.

The second example tests a remote recipient address. Listing 9.5 contains the output from Rulesets 3 and 0.
