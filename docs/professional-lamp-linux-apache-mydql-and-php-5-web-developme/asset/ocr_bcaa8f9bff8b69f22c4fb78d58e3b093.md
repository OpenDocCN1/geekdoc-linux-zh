experiments to determine the best approach for something before implementing it *for real*, and *profiling* covers experiments you conduct on the real thing to see just how well it actually performs. Clearly, there is quite a lot of overlap between the two; many of the techniques and the tools are the same (because the tools don't necessarily *care* whether the code you're using them on is natural or synthetic). Tools exist to aid you in these at both OS and PHP levels.

# PEAR Benchmark

You've already seen examples of benchmarking in the previous section. They were constructed ad-hoc, but the basic ideas they have in common are common enough to warrant being abstracted into a separate class:

+   1. Start a timer (noting the current time).
+   2. Do something.
+   3. Stop the timer (again noting the current time).
+   4. Compare the stopping time with the starting time to determine the elapsed duration.
+   5. Repeat steps 1--4 a lot, accumulating the durations.
+   6. Have a look at the results.

An obvious enhancement to this would be to label the timers, so that several could be started and stopped independently. Also nice would be if timers could also contain information about the time spent in specific sections of the code they're covering. The PEAR Benchmarking class provides all this functionality. Installation of PEAR and PEAR packages is covered in Chapter 8; so you've already taken care of that, and you're ready to proceed with using it.

To repeat the initial string-building experiment using the Benchmarking class, you could write the following:

```
`<?php
require 'Benchmark/Timer.php';
$variable = 'string';
$timer = new Benchmark_Timer();
$timer->start();
for($i=0; $i<1000000; ++$i)
{
    $string = "this string has a $variable embedded into it";
}
$timer->setMarker('lapt ime');
for($i=0; $i<1000000; ++$i)
{
    $string = "this string has a " . $variable ." inserted into it";
}
$timer->setMarker('finish');
echo "Variable interpolation required "$timer->timeElapsed('Start','lapt ime',"`
```