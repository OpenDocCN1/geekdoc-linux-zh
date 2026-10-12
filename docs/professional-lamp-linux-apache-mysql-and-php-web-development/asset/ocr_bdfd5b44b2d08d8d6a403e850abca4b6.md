# ## Chapter 5

The first property, `configFile`, holds the name of the configuration file you’re going to use. The default value for this configuration file is set to `reqs.xml`, so you don’t need to explicitly set this property unless you use a different filename. The `configType` property is where the type of configuration is specified. In this case, a default value of `xml` is provided to indicate your configuration is in XML format. The last property, `errors`, is simply a placeholder for any error messages encountered during processing later on.

Next follows the constructor method for the class:

```
```php
public function __construct($configFile = null, $configtype = null)
{
    if ($configFile)
    {
        $this->configfile = $configfile;
    }
    if ($configtype)
    {
        $this->configtype = $configtype;
    }
}
```
```

While nothing truly amazing happens in this constructor, it does allow provisions for passing a configuration file and type when the object is created, and uses those values to set the corresponding properties.

The final method in ConfigManager is where all the magic happens:

```
```php
public function processConfig()
{
    switch ($this->configtype)
    {
        case 'xml':
            require_once 'class.XMLConfigProcessor.php';
            $proc = new XMLConfigProcessor($this->configfile);
            $this->errors = $proc->process();
            break;
    }

    echo nl2br($this->errors);
}
?>
```
```

The `processConfig()` method first determines the type of configuration, and then calls the necessary code and utilizes component objects based on the configuration type. Currently, there is only one type specified in `processConfig`, one that handles XML configuration files. Any number of additional cases can be added as new configuration processor types are created. If you wanted to store your configuration in a database, you could devise your own database-configuration-processing object, and then add a case to this `switch` that calls any processing methods in your new class.

Notice the class file for `XMLConfigProcessor` is included at this point instead of at the beginning of the file, or earlier in the class. This way, the class file is only parsed if and when needed, to help cut down on extraneous processing if a different configuration type is used. To use `XMLConfigProcessor`, it’s a