![](bbox=[0.125, 0.073, 0.875, 0.396])

# # The project

When doing any project, no matter how small, it pays to take one step at a time and test you go. So, the first thing to do is to test your hardware before you get into anything fancy. You can simply extend the LED blink program to blink all the LEDs or, if you're not up to that, simply take the LED blink program and change the GPIO number to one you're using here. Run and see if the correct LED flashes, then stop the program and change to another number. Repeat until all the LEDs (as well as the push button) have been tested.

The project splits up into two parts: Generate the random number between 1 and 6 and then display it.

# # The numbers

There are two ways to generate the random numbers: Use the computer's random-number generator or use some random event. The problem with the random-number generator is that it's not really a random-number generator. It's a pseudo random-number generator — the sequence of numbers is fixed and will repeat every time you run the program, unless you use it by picking a random starting point in this sequence. Because the sequence is very long, this approach will appear to be a random number. (The Python random-number generator uses as the seed the length of time the system has been powered on.)

However, a better way is to use something that is by its nature random: In this case, we use the length of time the user has pressed the button, indicating a