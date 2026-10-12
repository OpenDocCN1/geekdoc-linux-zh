
Is it all worth it? How long would it have taken you to write the operation as a multiplication, and how long as a bit shift? How long to verify that what you wrote is correct? How long to fix any bugs that resulted from things like the different behavior in extreme cases, or forgetting the difference in precedence? What about time spent altering the code (say, to multiply by 9 instead of 8) in the future? (You can't just search for instances of 8; you have to search for instances of 3 as well, and why aren't you using named constants?) How many times will that operation have to be executed to save you the same amount of time you spent making sure that you were using the faster option — a nanosecond here, a nanosecond there? And how long would it be before the operation has been executed that many times?

The point is that *your* time is more valuable than the *computer's*. The online time that is more valuable than yours is that of the visitors to your site. So don't waste your time trying to trim a few nanoseconds off the page's processing time: site visitors won't notice the difference even under exceptionally heavy use.

## Comparing the Speed of Strings — A Benchmarking Example

PHP has several ways of combining literal strings and variables, and three methods of quoting strings. The three methods of quoting are to use single quotes, double quotes, and heredoc syntax. Inserting variables into strings can be achieved by using the concatenation operator, variable interpolation in double- and heredoc-quoted strings, and C-style string formatting functions. Every now and then, a curious programmer asks which method is "better." *Better* can be defined in more than one way: Is it faster? Does it make the source code more readable? Is it simpler and less prone to bugs? As far as readability and simplicity go, the debate is fairly evenly split: if one were *clearly* superior to the others, then natural selection would see experienced developers on large-scale applications using the superior method to the exclusion of all others. The fact that no such selection appears to have taken place over the years suggests that the differences are not significant enough to appear in an industry-wide Best Practices document or coding standard.

Whether single-quoted strings are *faster* than double-quoted ones is much more quantifiable. If you're forced to give a yes or no answer, then the safest would be to say "yes," but in reality things are more complicated than that.

Like any question about the real world, it cannot be answered without first obtaining some facts. As an initial experiment you could write the following:

```php
$variable = 'string';

$start = microtime(true);
for($i=0; $i<1000000; ++$i) {
    $string = "this string has a $variable embedded into it";
}
$elapsed = microtime(true);
for($i=0; $i<1000000; ++$i) {
    $string = "this string has a "."$variable." inserted into it";
}
$finish = microtime(true);

echo "Variable interpolation required ",$finish-$start," seconds for one million iterations.\n";
echo "Variable concatenation required ",$finish-$1sttime," seconds for one million iterations.\n";
```

The first time I run this script, the times I get for interpolation and concatenation are, respectively, 6.81 and 1.72 seconds. The second time, however, I get times of 6.58 and 1.71 seconds. The variability is due to the fact that the computer I am running on is doing more than simply running the script. It has other demands on its time, and the time it spends on those other demands gets included in how long it takes for this script to complete. When the script was run for the first time, the operating system would have had to organize space in memory for PHP, the script, and its data, with some of that organization occurring while the script was running (most of it would have occurred before the script began executing, however, so it wouldn't appear in the timings). But the second run, immediately afterwards, would be in an environment where there was already a suitable block of free space, and so it started up much faster.

The upshot of this is that you can't trust the results of just one run; there are too many ways for the timings to fluctuate, and many of them are out of your control. What is necessary is to run the script — from start to finish — several times, and take averages of the result. For interpolation, the times over 10 runs ranged from 6.57 to 6.86 seconds with an average of 6.77; and for concatenation, the range was 1.65 to 1.71 with an average of 1.70. You can throw more statistical firepower at the data if you like, but it does seem clear that concatenation is about four times faster than interpolation.

But that isn't the whole story. What if the times depend on how long the string is, or how many variables are being concatenated or interpolated? Should we not test for variations in those as well?

What follows is a command-line PHP program to run tests of this sort. Rather than time itself as it concatenates or interpolates variables, it instead writes a separate PHP script, and then calls it via the command line, thus not only timing the script itself, but also the time spent starting PHP, loading the script and shutting down. It does this for a range of initial string sizes (64 to 26176 characters, in steps of 512), and number of interpolations/concatenations (0 to 100). It carries out each experiment five times, and writes the average run times to a single log file. If twenty-five thousand separate experiments is too many (it can take somewhere in the vicinity of four hours) then the ranges can be reduced to taste, but testing each size/number combination several times and averaging the result should be kept. As written, it times variable interpolation — uncommenting line 59 and commenting line 58 (ie, the str_replace() calls) changes it to timing concatenation:

```php
<?php
function generate_test($string)
{
    $code = '<?php
$interpolated="badgers!";

for($i=0; $i<100; ++$i)
    $string = "".$string."";
?>';
    $temp_file = tempnam('', 'xx_test');
    $fp = fopen($temp_file, 'wb');
    fwrite($fp, $code);
    fclose($fp);
    return $temp_file;
}

function run($file)
{
    $average_runtime = 0;
    for($runs=0; $runs<5; ++$runs)
    {
        $start = microtime(true);
        shell_exec("php -f $file"); // If necessary, supply path information here
        $end = microtime(true);
        $average_runtime += $end-$start;
    }
    return $average_runtime/5;
}

$log = fopen('logfile.txt','wb');
for($string_size=1<<6; $string_size<=26176; $string_size+=512)
{
    $generic_string = str_repeat("wibble splunge!\n", $string_size);
    $real_string_size = 16*$string_size;
    $all_positions = range(0,$real_string_size-1);
    for($num_variable_interpolations=0; $num_variable_interpolations<=100;
        ++$num_variable_interpolations)
    {
        echo $string_size,"\t",$num_variable_interpolations,"\n";
        $string = $generic_string;
        if($num_variable_interpolations==0)
            $positions = array();
        else
            $positions = array_rand($all_positions,$num_variable_interpolations);
        if(count($positions)==1) $positions = array($positions);
        foreach($positions as $position)
        {
            $string = substr($string,0,$position).'${'.substr($string,$position);
        }
        $string = str_replace('${','${interpolated}', $string);
        $string = str_replace('$','*.interpolated.*', $string);
        $file = generate_test($string);
        $runtime = run($file);
        unlink($file);
        fwrite($log,
            $string_size,"\t",$num_variable_interpolations,"\t",$runtime,"\n");
    }
}
fclose($log);
?>
```

From the last `fwrite()` in the code you can deduce the format of the saved data: one line per experiment, consisting of the size of the string (before variable insertion), the number of variables being inserted, and the number of seconds. You can then read this data into your preferred data analysis or plotting software for exploration.
