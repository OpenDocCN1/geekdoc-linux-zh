One thing to note is that you're seeing layers upon layers of the same settings here. There are multiple places, for example, that you can set traceoptions. The most local version of this setting is the one that takes hold. If you've set traceoptions for a specific neighbor, then that's the setting used even if the overall egp statement says differently.

# BGP Configuration

Another potential border routing protocol is appropriately named the Border Gateway Protocol (BGP), which you should be familiar with from Chapter 3. If you would rather run a BGP border router than an EGP, gated can still do the job. You activate this capability by creating a bgp statement starting with:

`bgp on {`

The main substatements available in the bgp statement are listed in Table 5.20. You will notice that much of the meat in the setup is not this set of statements, but is instead in the child statements within substatements.

Table 5.20 Options Available Within the bgp Statement in gated

| Option | Purpose | Format | Value(s) |
|---|---|---|---|
| defaultmetric | Sets the BGP cost assigned to routes this border router advertises to neighbors. | defaultmetric cost; | An optional value that can add a cost to routes advertised from this border router. |
| group type | Enables you to create a group of like BGP peers. Use more than one group type statement to make more than one grouping. | group type details { allow { options }; peer options; } | This is a very simplified version of what a group type statement looks like. See the chapter text for a more detailed discussion. |
| preference | Sets how important gated sees routes learned from RIP. | preference value; | The lower the value, the more important these routes are to gated when utilizing BGP. Default is 170. |
| traceoptions | Sets how gated logs data for this specific BGP router. | traceoptions settings; | Options available to all protocols are listed in Table 5.11, and options available specifically in the bgp statement are listed in Table 5.21. |