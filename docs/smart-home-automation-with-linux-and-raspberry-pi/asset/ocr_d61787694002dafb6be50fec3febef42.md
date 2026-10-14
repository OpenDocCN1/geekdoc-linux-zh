All other protocols, such as soap, are handled by external commands located in `$MINBASE/bin/xmit/ [protocol name]/cmd`. This combines the new protocol information (IP address and port) with all the parameters from the original command, with the remote device name (column 4) in place of the original one, and passes it to the appropriate cmd script. Here it is in geek parlance:

```
```bash
$MARPLEPROTOCOL/cmd ${DEVARRAY[2]} ${DEVARRAY[3]} $COMMAND ${DEVARRAY[4]} $ALARGS
```
```

This command can then issue an appropriate network packet to the server listed. In the case of SOAP, a call is made to minerva/marple/cmd.php where the arguments are extracted, and a brand new Bearskin command is formulated like this:

```
```php
<?php

function getCommand($cmd, $args) {

    # in case someone tries exec'ing other programs, in different directories
    # we'll strip and stop them.
    $cmd = str_replace("/", " ", $cmd);
    $cmd = str_replace("..", " ", $cmd);

    $minervaPath = "/usr/local/minerva";
    $fullCommand = "$minervaPath/bin/$cmd $args";

    return $fullCommand;
}

function marple($cmd, $args) {
    $fullCommand = getCommand($cmd, $args);
    $result = array();

    exec($fullCommand, $result);

    $rts = "";
    foreach ($result as $v) {
        $rts .= "$v\n";
    }
    return $rts;
}

$server = new SoapServer(null, array('uri' => "urn://www.minervahome.net/marple"));
$server->addFunction("marple");
$server->handle();
?>
```
```

Note that the only commands available are under the `/usr/local/minerva` hierarchy, with all instances of pruned out to stop malicious code from being run.

> **Note** If you add your own protocols but they’re not addressed by an IP/port pair, then you can reappropriate the two columns to your desires, provided your `$MARPLEPROTOCOL/cmd` script can understand them.