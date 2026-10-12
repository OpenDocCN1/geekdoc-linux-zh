# # Chapter 5

The next method you encounter is `checkConfigAccess()`. This method checks to see if the XML configuration file actually exists on the filesystem, and if it does, it checks then to see if it is readable. If the file does not exist or is not readable, an error message is added to the `message` property. Note that `clearstatcache()` is called at the end of the method. The results of `file_exists()` and `is_readable()` are cached by PHP, so it’s a good idea to clear the result cache when you are finished, to prevent erratic results later on:

```
```php
private function checkConfigAccess()
{
    $returnValue = false;

    // Check to see if config file exists and is readable
    if (file_exists($this->xmlfile) and
        is_readable($this->xmlfile))
    {
        $returnValue = true;
    }
    else
    {
        $this->message .= "Warning: " .
                          "Could not access config file.\n";
    }

    // Clear cached filesystem lookups
    clearstatcache();

    return $returnValue;
}
```
```

Next up, `checkDeps()`. As the name implies, this method checks dependencies of the class itself. For `XMLConfigProcessor`, the only non-standard PHP requirement is availability of the SimpleXML extension. If you decided later to modify this class to use the XML Parser functions or DOM XML extension, for example, you would add the requisite checks to this method.

To check for SimpleXML, you simply use the `extension_loaded()` function covered earlier in this chapter. If SimpleXML is not available, add another error message to the pile:

```
```php
private function checkDeps()
{
    $returnValue = true;

    // Check for SimpleXML
    if (!extension_loaded('SimpleXML'))
    {
        $returnValue = false;
        $this->message .= "Warning: " .
                          "SimpleXML extension not available.\n";
    }

    return $returnValue;
}
```
```