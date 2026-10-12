There is a constant need to generate random numbers in programming. Not only is it crucial for computer games that need some variation between play periods, but it is also vital in cryptography and secure communications.

PHP has two ways of generating random numbers: fast and more predictable, and slow and less predictable. It is important to remember that true randomness is very difficult to achieve with computers, so many people refer to random number generators as *pseudo-random*, meaning they appear to be random but are not truly random.

The basic random generator is the *rand()* function, which takes two numbers as its two parameters: the lowest random number you want and the highest. So, using *rand(1, 10)* could return 1, 10, or any whole number in between. The “more random” random number generator uses the Mersenne Twister algorithm and so is called *mt_rand()*. If all you are doing is printing a different greeting to your website visitors each time they come to your front page, *rand()* is more than enough!

Listing 31.7 demonstrates a script demonstrating the *rand()* function, but you can switch to the Mersenne Twister algorithm by swapping *rand()* for *mt_rand()*.

# LISTING 31.7 Varying Greeting Messages to Your Visitors

```
```php
<?php
    switch (rand(1,4)) {
        case 1:
            echo "Hello!";
            break;
        case 2:
            echo "Welcome!";
            break;
        case 3:
            echo "Greetings!";
            break;
        case 4:
            echo "Salutations!";
            break;
    }
?>
```
```

# Arrays

Working with arrays is no easy task, but PHP makes it easier by providing a selection of functions that can sort, shuffle, intersect, and filter them. As with other functions, there is only space here to choose a selection; this is by no means a definitive reference to PHP’s array functions.

The easiest function to use is *array_unique()*, which takes an array as its only parameter and returns the same array with all duplicate values removed. Also in the realm of “so easy you do not need a code example” is the *shuffle()* function, which takes an array as