# Generating Random Numbers

As our next jump on this quick tour of Unix library calls from assembly, let's get seriously random. (Or modestly pseudorandom, at least.) The standard C library has a pair of functions that allow programs to generate pseudorandom numbers. The pseudo is significant here. Research indicates that there is no provable way to generate a truly random number strictly from software. In fact, the whole notion of what random really means is a spooky thing that keeps a lot of mathematicians off the streets these days. Theoretically you'd need to obtain triggers from some sort of quantum phenomenon (radioactivity is the most often mentioned) to achieve true randomness. L a nuclear-powered random-number generator, we'll have to fall back on pseudorandom and learn to live with it.

A simplified definition of pseudorandom-number generator would run something like this: A pseudorandom-number generator yields a sequence of numbers with no recognizable pattern, but the sequence can be repeated by passing the same seed value to the generator. A seed value is simply a whole number that acts as an input value to an arcane algorithm that creates the sequence of pseudorandom numbers. Pass the same seed to the generator, and you get the same sequence. However, within the sequence, the distribution of numbers within the generator's range is reasonably scattered.

The standard C library contains two functions relating to pseudorandom numbers:

+   * The rand function passes a new seed value to the random-number generator. This value must be a 32-bit integer. If no seed value is passed, the value defaults to 1.

+   * The rand function returns a 31-bit pseudorandom number. The high bit is always 0 and thus the value is always positive if treated as a 32-bit signed integer.

Once you understand how they work, using them is close to trivial.