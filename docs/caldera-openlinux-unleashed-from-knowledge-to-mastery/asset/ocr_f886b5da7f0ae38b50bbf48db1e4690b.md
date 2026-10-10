H7M?Message-Id: <$t.$i$>

############## REWRITING RULES ##############

### Ruleset 3 -- Name Canonicalization ###

S3

# handle null input (translate to <@> special case),

R0$

$ <@>

# strip group: syntax (not inside angle brackets!) and trailing semicolon

RS* $ : S1 <@> mark addressees

RS* < S* > S* <@> : S1 < S2 > $3 unmark <addr>

R0 S* <@> $ : <@> unmark @host:

RS* : : S* <@> $ S1 : : S2 unmark node:addr

R :include$ S* <@> $ : include$ S1 unmark :include:. .

RS* [ S* | S* ] <@> $ : S1 [ S2 ] S3 unmark IPv6 addr

RS* : S* [ S* ] S1 : S2 [ S3 ] <@> remark # leading colon

RS* ; S* <@> S : S2 strip colon if marked

RS* <@> S : S1 unmark

RS* ; $1 strip trailing semi

RS* < S* ; > S1 < S2 > bogus bracketed semi

# null input now results from list; ; syntax

R0$ $ ; ; <@>

# strip angle brackets -- note RFC733 heuristic to get innermost item

RS* S : S1 <1> housekeeping <>

RS* < S* > < S2 > strip excess on left

R< S* > $* < $1 > strip excess on right

R<> $ < @ > MAIL FROM:<@> case

R< S* > $ : S1 remove housekeeping <>

# make sure <@,ea,bq,ec:u|er|eR@> syntax is easy to parse -- undone later

Re S*, S* < $1 : S2 change all "|" to "+"

# localzize and dispose of route-based addresses

Re S* : S* $ S0 S>96 < $1 > : S2 handle <route-addr>

# find focus for list syntax

R S* : S* ; $ $* S0 S>96 $1 : S2 ; < $3 > list syntax