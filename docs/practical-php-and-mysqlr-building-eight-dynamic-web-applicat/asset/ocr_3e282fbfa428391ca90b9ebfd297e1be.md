Determine if the final result is a 0.5 figure (such as 7.5, as opposed to 8):

```
```
else {
  $a = (round($avgrow['avg'] * 2) / 2) ."<br>";

  $a *= 10;

  if($a%5 == 0 && $a%10 != 0) {
    $range = ($a / 10) - 0.5;
  } else {
    $range = $a / 10;
  }
}
```
```

To calculate if we have .5 value in $a (such as 6.5), first multiply the value of $a by 10 ($a *= 10), and then inside the brackets of the `if` statement check if $a can be divided by five. If it does, $a is divided by 10 to get to its original value, and 0.5 is subtracted. The resulting `$range` variable indicates the number of full images to display.

Create a `for` loop to display each image:

```
```
$range = $a / 10;
}

for($i=1;$i<=$range;$i++) {
  echo "<img src=" . $config_basedir . "siteimages/rating_full.png>";
}
```
```

The `for` loops between 1 and the value inside `$range` and then displays *rating_full.png* each time.

Check if the average is a float again, to see if the half-on image should be added:

```
```
  echo "<img src=" . $config_basedir . "siteimages/rating_full.png>";
}

if($a%5 == 0 && $a%10 != 0) {
  echo "<img src=" . $config_basedir . "siteimages/rating_half.png>";
}

$a = $a / 10;
```
```

Calculate how many off images should be displayed by removing the rounded average from 10: