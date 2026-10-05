# Adding the timer

Pygame Zero includes the ability to schedule a function to run regularly, which you can use to run a timer. You've already set the timer variable to 10 at the start of the program. You just need to create a function to decrease it by 1 each time it runs, and then schedule it to run every second. Here's what code looks like: You need to add it to the end of your program:

```
def countdown():
    global timer
    timer -= 1
    if timer == 0:
        clock.unschedule(countdown)
        sounds.whoops.play()
```

clock.schedule_interval(countdown, 1)

The line at end isn't part of any function. You can tell it because the clock isn't indented. As a result, this instruction runs when the game begins. clock.schedule_interval() sets another function to run at regular intervals. In our case, we're running the countdown() every 1 second. Note that we don't use brackets after countdown here. We have to put this clock.schedule_interval(countdown, 1) line after the function because it can only be used to schedule a function that has been defined earlier in the program.

The countdown() function itself reduces the global timer variable by each time it runs. If the timer is now 0, it uses clock.unschedule to stop countdown() from running regularly and plays the Game Over music.

When you run the game, you will now see the timer counting in the top right. When the timer runs out, no new clouds will appear on the screen, although those that are already there will drift off the top in the usual way. When the time is up, your score will be shown large in the middle of the window.

# Adjusting the game difficulty

There are several things you can do to adjust the game and its difficulty:

+   Change the size or shape of the window by changing the WIDTH and HEIGHT variables at the start. A wider window makes them harder to catch, but a taller window gives you more time.