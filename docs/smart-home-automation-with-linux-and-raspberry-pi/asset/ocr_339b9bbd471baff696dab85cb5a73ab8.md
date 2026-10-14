Unfortunately, that would require a lot of work to know which state parameter would be overridden later by the command parameters. You can simplify this by writing a refresh function that describes the current state and that every other applet will indirectly call when it requests a URL from the applet manager:

```
function getRefreshParams(&$appMan)
{
    return
        $appMan->getArgument($this, "user", $this->_viewuser)."&".
        $appMan->getArgument($this, "sort", $this->_sortlist);
}
```

You next add links that contain command parameters, which are similar to those you’ve seen already:

```
$html = "Show: ";
$html .= $appMan->getAppletLink($this, "dosort", "0", "Chronologically")." ";
$html .= $appMan->getAppletLink($this, "dosort", "1", "Alphabetically");

$html .= "    For: ";
$html .= $appMan->getAppletLink($this, "douser", $user, $user)." ";
$html .= $appMan->getAppletLink($this, "douser", "public", "Public");
```

These parameters, by convention, are prefixed with do, indicating that they should change the refresh state. That is, new state = old state + do changes. The applet manager generates a suitable link by gathering the refresh parameters from every applet present on the current page and appending these do links to the end.

When the page is loaded, a new state is built based on these parameters and done in two stages. The first is to retrieve the refresh arguments:

```
$this->_sortlist = $appMan->queryParameter($this, "sort", false);
$this->_viewuser = $appMan->queryParameter($this, "user", "public");
```

The second is to look for any do parameters to change this state:

```
$this->_sortlist = $appMan->queryParameter($this, "dosort", $this->_sortlist);
$this->_viewuser = $appMan->queryParameter($this, "douser", $this->_viewuser);
```

In both cases, you’re using a default argument to queryParameter that covers the case when the applet is first used and no parameters at all are available and for when there are no command parameters.

You can then flex your creative muscles in displaying the output from the Bearskin command to do (remember writing that all those pages ago?!) and write the list into the HTML:

```
exec("/usr/local/minerva/bin/do list ".$this->_viewuser, $todolist);

if ($this->_sortlist) {
    sort($todolist);
}

$html .= "<ul>";
foreach($todolist AS $item) {
    $html .= "<li>$item</li>";
}
$html .= "</ul>";
```

To add a layer of polish to these, you could move the exec call into Zinc, but that can be left for another day!