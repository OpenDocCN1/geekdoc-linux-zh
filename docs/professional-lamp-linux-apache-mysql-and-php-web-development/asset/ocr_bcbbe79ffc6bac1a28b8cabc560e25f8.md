```
public function __sleep()
{
echo 'zzzzz';

return array('radius','origin');
}

public function __akeup()
{
echo 'good morning!';
}

echo 'Rise and shine.....';

$c = unserialize($_SESSION['c']);

echo '<br />The contents of our Circlie object are:<br />';
echo 'Radius: ' . $c->radius . '<br />';
echo 'Origin: (' . $c->origin['x'] . ',' . $c->origin['y'] . ')';
?>
```

Load the first page, page1.php, into your browser, and you should see something similar to Figure 2.1.

![](bbox=[0.17, 0.5, 0.94, 0.91])

**Figure 2.1**