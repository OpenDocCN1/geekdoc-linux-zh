SOMECOMPANYTHATDOESNOTEXIST.ORG
SOMECOMPANYZZZZ.ORG

To single out one record, look it up with "xxx", where xxx is one of the records displayed in the preceding listing. If the records are the same, look them up with "=xxx" to receive a full display for each record.

>> Last update of whois database: Sat, 11 Jan 2003 18:00:01 EST

# Querying Domain Registrar Records by Handle

Individuals listed on whois servers have a handle associated with them. You can query a particular handle to find related contact information:

```
```
[bash]$ whois -h whois.somewhoisserver.com "handle SOMEHANDLE"
[whois.somewhoisserver.com]
NOTICE AND WARNING BANNER HERE
```
```

Lastname, Firstname (SOMEHANDLE)  username@somecompanyasanexample.com
1234 Some St.
Somecity, SOMESTATE 99999
SOME COUNTRY

Database last updated on 12-Jan-2003 03:44:29 EST.

# Querying Domain Registrar Records by E-Mail

Individuals listed on whois servers usually have an associated e-mail address. It is possible to search for users by providing their complete e-mail address or a part of it. Therefore, the query

```
```
whois -h whois.somewhoisserver.com "@somecompanyasanexample.com"
```
```

will return names of individuals on record whose e-mail addresses contain the domain @somecompanyasanexample.com.

# Prevent Exposures Due to Domain Registrar Records

Ensure that e-mail addresses listed on whois records end with a domain different from your organization’s name. This will make it difficult for others to query your records via an e-mail query. In addition, some domain registrars offer to place their contact information on the whois records instead of your personal contact information. It is a good idea to take advantage of this option to prevent your personal contact information from being exposed to potential intruders.

Domain Registrars