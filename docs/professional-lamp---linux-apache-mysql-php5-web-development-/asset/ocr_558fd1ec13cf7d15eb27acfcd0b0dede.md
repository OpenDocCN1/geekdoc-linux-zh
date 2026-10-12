# Chapter 9

```
```
seconds for one million iterations.\n";
echo "Variable concatenation required ".$timer->timeElapsed('laptimer','finish')."
seconds for one million iterations.\n";

$timer->stop();
$timer->display();
?>
```
```

Benchmark_Iterate subclasses Benchmark_Timer, and provides a run() method to which you pass the name of the function you wish to test. Two matters to keep in mind when choosing one over the other. One is that the calling a function itself takes a bit of time. The other is that Benchmark_Iterate retains its timings for each individual experiment. Doing a lot of experiments means a big array, which is why the following code runs only ten thousand experiments instead of a million:

```
```
<?php
require 'Benchmark_Iterate.php';

$variable = 'string';

function interpolate($variable)
{
    $string = "this string has a $variable embedded into it";
}

function concatenate($variable)
{
    $string = "this string has a ".$variable." inserted into it";
}

$interpolation_benchmark = new Benchmark_Iterate;
$concatenation_benchmark = new Benchmark_Iterate;

$interpolation_benchmark->run(10000, 'interpolate', 'string');
$concatenation_benchmark->run(10000, 'concatenate', 'string');

$interpolation_result = $interpolation_benchmark->get();
$concatenation_result = $concatenation_benchmark->get();
?>
```
```

The two result variables are arrays: $interpolation_result['iterations'] records the number of times the test ran, and $interpolation_result['mean'] records the average (the Benchmark class uses the bench functions if they're available to maintain accuracy when calculating this). Unsetting these two elements leaves you with a numerically-indexed array that contains all of the individual times for each iteration so that you can carry out any other statistical tests you feel are relevant.

# top and ab

The NT4/Access report generator anecdote earlier came from the Windows world, and mentioned the use of its Task Manager. The process monitor utility that ships with Unix-type operating systems is named top, and is much richer in the amount of information it provides. Meanwhile, the Apache distribution includes the ab ApacheBench program, which tests the sharp end of your site: just how fast can