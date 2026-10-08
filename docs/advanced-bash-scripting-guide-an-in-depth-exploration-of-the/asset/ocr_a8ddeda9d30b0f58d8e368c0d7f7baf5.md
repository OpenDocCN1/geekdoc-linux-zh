# Advanced Bash-Scripting Guide

```
# The following statement checks $OUTFILE (whois.txt) for
#+ the presence of "BR" (Brasil) in the country field.
# If it is found, the query is re-run against whois.registry.br.

if grep -E "country:\|BR*" "$OUTFILE"
then
    echo "Searching for $IPADDR in whois.registry.br"
    whois -h whois.registry.br "$IPADDR" >> $OUTFILE
fi
```

```
RIPEquery() {
    echo "Searching for $IPADDR in whois.ripe.net"
    whois -h whois.ripe.net "$IPADDR" > $OUTFILE
}
```

+   * Initialize a few variables.
* slash8 is the most significant octet
* slash16 consists of the two most significant octets
* octet2 is the most significant octet

```
slash8=$(echo $IPADDR | cut -d. -f 1)
if [ -z "$slash8" ]; then # Another sanity check.
then
    echo "Undefined error!"
    exit $E_UNDEF
fi
slash16=$(echo $IPADDR | cut -d. -f 1-2)
# Period specified as 'cut' delimiter
if [ -z "$slash16" ]; then
then
    echo "Undefined error!"
    exit $E_UNDEF
fi\octet2=$(echo $slash16 | cut -d. -f 2)
if [ -z "$octet2" ]; then
then
    echo "Undefined error!"
    exit $E_UNDEF
fi
```

+   * Check for various odds and ends of reserved space.
* There is no point in querying for those addresses.

```
if [ $slash8 == 0 ]; then
    echo $IPADDR = "This Network" space\; not querying
elif [ $slash8 == 10 ]; then
    echo $IPADDR = "RFC1918" space\; not querying
elif [ $slash8 == 14 ]; then
    echo $IPADDR = "Public Data Network" space\; not querying
if [ $slash8 == 127 ]; then
    echo $IPADDR = loopback space; not querying
elif [ $slash8 == 169 ]; then
    echo $IPADDR = link-local space\; not querying
if [ $slash8 == 172 ]; then
    if [ $octet2 -ge 16 ] && [ $octet2 -le 31 ]; then
        fi
    echo $IPADDR = "RFC1918" space\; not querying
```

Appendix A. Contributed Scripts