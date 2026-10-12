
## Chapter 9

The resulting plots of time versus length of string and number of variables look very different for concatenation (see Figure 9.1) and interpolation (see Figure 9.2).

![](img/cacdd24f2926f10ee3219256ad732604_229_0.png)

![](img/cacdd24f2926f10ee3219256ad732604_229_1.png)

Probably the first thing you can see in these plots is that when interpolating in double-quoted strings, the number of variables is all but irrelevant. There are hints that processing is especially slow when the number of variables is a multiple of 32. Because changing the number of variables was carried out by the inner loop, the experiments for a *given* number of variables were performed at widely spaced points during the run, ruling out all but suspiciously well-timed transient delays from external sources.

### Code Efficiency

Comparing the two graphs when the number of variables is very small, it’s first unusual to see that the speed of concatenation *drops* initially, and second that interpolation *rises* very sharply indeed. Closer inspection reveals that when the number of variables is 0, double-quoted and single-quoted strings are equally fast, with double-quoted strings only slowing down once there are variables to be interpolated. This is because double-quoted strings are scanned for variables while the program is being loaded, during lexical analysis. This is a one-off expense that is even less than you might at first expect: the contents of both single-quoted and double-quoted strings have to be scanned *anyway*, to locate escape sequences and the actual end of the string. The only real difference is that scanning double-quoted strings generates several tokens in sequence when variables are present.

Overall, the shapes of the two charts are distinctive. The difference can be formalized by using “big-O notation,” used in program analysis to describe the “size” or “speed” of an algorithm in terms of the *size* of the problem given. While it can be given a precise technical definition, it’s enough to think of *O(*f(*n*)*)* as meaning that the graph of the algorithm’s behavior is “looking like” the graph of *f(*n*)* as *n* gets *larger and larger*:

```
O(f(n)) = the set of functions g(n) such that there exist positive constants c and n0
          such that 0 ≤ g(n) ≤ cf(n) for all n ≥ n0.
```

In this case, the graph of double-quoted interpolation doesn’t vary with *v*, the number of variables being interpolated, and only linearly with *l*, the length of the string (that is to say, it’s twice as slow when the string is twice as long). In big-O notation this would be described as O(*l*). The graph for single-quoted concatenation is more complex. If you fix the length of the string and look at a single slice of the graph as the number of variables changes (such a slice is shown in Figure 9.1 at the top edge of the graph from the left to the peak), it looks fairly linear in *v*. Fixing the number of variables and allowing the length of the string to vary (the ridge crest leading from the peak down to the right) curves it in such a way as to suggest a parabola. Overall, these two influences appear to be multiplied, giving a big-O description of O(*fv²*).

In the *long run*, I increases more slowly than *fv*, and in fact for long strings with many variables, interpolation is *faster* than concatenation. For shorter strings, however, or fewer variables, concatenation still wins out.

Big-O notation only concerns itself with what happens in the program in the long run as the size of the problem gets larger, ignoring features that appear only for small instances of the problem. You’ll recall that when there are no variables involved, the two methods are equally quick (since both consist of a single string), but that single-quoted concatenation speeds up slightly before slowing again, while double-quoted interpolation slows sharply as soon as a single variable is introduced, and never recovers. Big-O says that in the *long run*, variable interpolation is faster than concatenation, but you would need to have multi-kilobyte strings with dozens of variables to actually see it happen.

You can see that even in this very simple example, with only two factors to consider, there is the potential for a lot of subtlety when aiming for a definitive answer of what is “best.” You could make deeper investigations even in this comparatively trivial example, and with more complicated problems you would probably have to before reaching any conclusions. But here is a good place to end the example, except to note that the slowest time recorded in all of the charted experiments is 3.7 seconds.

### Unintuitive Results

Unlike C, which is converted into machine code that really isn’t too different from what you actually write (the language has been described as “Assembler with delusions of grandeur”), your PHP program is being run by a virtual machine simulated by the PHP engine. When it comes to performance tuning, this can make for difficulties because it becomes that much harder to predict what will work well and what will not. This will be examined later, but for now you may wish to meditate on the results of the following test code:

```php
<?php
$j=0;
$start_test_1 = microtime(true);
for($i=0; $i<1000000; $i++) $j++;
$end_test_1 = microtime(true);

$j=0;
$start_test_2 = microtime(true);
for($i=0; $i<1000000; $i++) ++$j;
$end_test_2 = microtime(true);

$j=0;
$start_test_3 = microtime(true);
for($i=0; $i<1000000; ++$i) $j++;
$end_test_3 = microtime(true);

$j=0;
$start_test_4 = microtime(true);
for($i=0; $i<1000000; ++$i) ++$j;
$end_test_4 = microtime(true);

$test_1 = $end_test_1 - $start_test_1;
$test_2 = $end_test_2 - $start_test_2;
$test_3 = $end_test_3 - $start_test_3;
$test_4 = $end_test_4 - $start_test_4;

echo "Postincrementing I and J one million times: ";
$test_1, " seconds.\n";
echo "Postincrementing I and preincrementing J one million times: ";
$test_2, " seconds.\n";
echo "Preincrementing I and postincrementing J one million times: ";
$test_3, " seconds.\n";
echo "Preincrementing I and J one million times: ";
$test_4, " seconds.\n";
?>
```

### Benchmarking and Profiling

There are many techniques and utilities for estimating the speed of a program, and they should be used before, during, and after embarking on any mission to speed up your site, so that you don’t waste time making changes without any appreciable difference or, worse, slowing your site down. Broadly speaking, they can be divided into two main categories: benchmarking is what you do when you conduct experiments to determine the best approach for something before implementing it for real, and *profiling* covers experiments you conduct on the real thing to see just how well it actually performs. Clearly, there is quite a lot of overlap between the two; many of the techniques and the tools are the same (because the tools don’t necessarily *care* whether the code you’re using them on is natural or synthetic). Tools exist to aid you in these at both OS and PHP levels.

### PEAR Benchmark

You’ve already seen examples of benchmarking in the previous section. They were constructed ad-hoc, but the basic ideas they have in common are common enough to warrant being abstracted into a separate class:

- 1. Start a timer (noting the current time).
- 2. Do something.
- 3. Stop the timer (again noting the current time).
- 4. Compare the stopping time with the starting time to determine the elapsed duration.
- 5. Repeat steps 1–4 a lot, accumulating the durations.
- 6. Have a look at the results.

An obvious enhancement to this would be to label the timers, so that several could be started and stopped independently. Also nice would be if timers could also contain information about the time spent in specific sections of the code they’re covering. The PEAR Benchmarking class provides all this functionality. Installation of PEAR and PEAR packages is covered in Chapter 8; so you’ve already taken care of that, and you’re ready to proceed with using it.

To repeat the initial string-building experiment using the Benchmarking class, you could write the following:

```php
<?php
require 'Benchmark/Timer.php';

$variable = 'string';

$timer = new Benchmark_Timer();

$timer->start();
for($i=0; $i<1000000; ++$i)
{
    $string = "this string has a $variable embedded into it";
}
$timer->setMarker('laptimе');
for($i=0; $i<100000; ++$i)
{
    $string = "this string has a "$variable." inserted into it";
}
$timer->setMarker('finish');

echo "Variable interpolation required "$timer->timeElapsed('start','laptimе')." 
```
