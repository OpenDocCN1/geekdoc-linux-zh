```
% git config section.key value '[!]'
```

To add a new proxy, without altering any of the existing ones, use

```
% git config --add core.gitproxy '"proxy-command" for example.com'
```

An example to use customized color from the configuration in your script:

```
#!/bin/sh WS=$(git config --get-color color.diff.whitespace "blue
reverse") RESET=$(git config --get-color "" "reset") echo "${WS}your
whitespace color or blue reverse${RESET}"
```

For URLs in http.sslVerify is set to false, while it is set to true for all others:

```
% git config --bool --get-urlmatch http.sslverify true
% git config --bool --get-urlmatch http.sslverify false
% git config --get-urlmatch http http.cookieFile /tmp/cookie.txt
http.sslverify false
```