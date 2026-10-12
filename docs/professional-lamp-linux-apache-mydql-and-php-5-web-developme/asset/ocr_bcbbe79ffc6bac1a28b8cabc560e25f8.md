# PHP5 OOP

```
```
public function __sleep()
{
	echo 'zzzzz';

	return array('radius','origin');
}

public function __wakeup()
{
	echo 'good morning!';
}

echo 'Rise and shine....';
$C = unserialize($_SESSION['c']);

echo '<br />The contents of our Circle object are:<br />';
echo 'Radius: ' . $C->radius . '<br />'; 
echo 'Origin: (' . $C->origin['x'] . ',' . $C->origin['y'] . ')';
?>
```
```

Load the first page, page1.php, into your browser, and you should see something similar to Figure 2.1.

![](bbox=[0.16, 0.5, 0.93, 0.94])