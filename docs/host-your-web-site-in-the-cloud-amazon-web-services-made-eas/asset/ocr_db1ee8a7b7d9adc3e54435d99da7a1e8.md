```
{
    exit("Usage:\n"
        $argv[0] . " -f\n" .
        $argv[0] . " -q\n");
}

switch ($argv[1])
{
    case '-f':
        $doFile = true;
        break;

    case '-q':
        $doQueue = true;
        break;
}
```

The program will access SimpleDB and SQS, so we'll need to create access objects for both services:

```
**chaptter_08/rss.process.php (excerpt)**

$$db = new AmazonSDB();
$$qs = new AmazonSQS();
```

After each feed has been parsed, we'll store the most interesting fields. Here they are at the item and feed levels:

```
**chaptter_08/rss.process.php (excerpt)**

$$feedFields = array('link',
    'title',
    'pubdate',
    'tagline',
    'language',
    'generator',
    'description');

$$itemFields = array('guid',
    'link',
    'title',
    'description');
```