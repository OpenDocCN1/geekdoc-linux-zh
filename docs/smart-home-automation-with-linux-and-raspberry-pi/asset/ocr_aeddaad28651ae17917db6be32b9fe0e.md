# Currency Conversion

Although there are many conversion sites available, they are highly variable in their offerings. Some require signup and an application ID. Some introduce adverts into the data stream, and some just plain don’t work! Because Google provides conversion functionality for free as part of its search engine, there’s no reason to be using anything else. So, we can extract the data from a request such as:

http://www.google.com/ig/calculator?hl=en&q=100EUR=USD

which returns a JSON literal in the form of:

```
{"lhs": "100 Euros", "rhs": "134.14 U.S. dollars", "error": "", "icc": true}
```

It is therefore easy to see how an app can be built to provide a handy conversion chart, in both directions.

```
```php
<?php

$amount = "1";
$fromCurrency = "GBP";
$toCurrency = "EUR";

$url = "http://www.google.com/ig/calculator?hl=en&q=$amount{$fromCurrency}=?$toCurrency";

$rawdata = file_get_contents($url);

$data = explode('"', $rawdata);
$data = explode(' ', $data[3]);

$conversionRate = $data[0];

for($i=1; $i<20; ++$i) {
    print "$i $fromCurrency\t" . number_format($i * $conversionRate, 2) . " $toCurrency \t";
    print "$i $toCurrency\t" . number_format($i / $conversionRate, 2) . " $fromCurrency \t";
    print "\n";
}

?>
```
```

Of course, you may not be as lazy as I am in using the explode method, and you may prefer to formally decode the JSON!

With the rates at the time of writing, this produces:

+   1. 1 GBP = 1.16 EUR			1 EUR = 0.86 GBP
+   2. 2 GBP = 2.32 EUR			2 EUR = 1.72 GBP
+   3. 3 GBP = 3.48 EUR			3 EUR = 2.59 GBP
+   4. 4 GBP = 4.64 EUR			4 EUR = 3.45 GBP
+   5. 5 GBP = 5.80 EUR			5 EUR = 4.31 GBP
+   6. 6 GBP = 6.96 EUR			6 EUR = 5.17 GBP
+   7. 7 GBP = 8.12 EUR			7 EUR = 6.03 GBP
+   8. 8 GBP = 9.28 EUR			8 EUR = 6.89 GBP
+   9. 9 GBP = 10.44 EUR			9 EUR = 7.76 GBP