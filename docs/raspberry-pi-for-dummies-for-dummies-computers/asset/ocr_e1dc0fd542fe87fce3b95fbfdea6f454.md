```
LISTING 17-6: (continued)
main()
    except KeyboardInterrupt:
        pass
    turn off all LEDs
    leds.replaceAll((0,0,0))
    leds.show()
```

Again like the previous program, the main structure of the code can be found in the two while loops in the main function. One issue that needs to be addressed is that the push button could be held down so that would register as pressed all time— and always keeps the ball at the right. To prevent this from happening, you have to implement a state-change detector on the button— involves looking at the current state of the push button and comparing it with the previous read value. If only the previous value equals Pushed does the program recognize that the button has just pushed. We say this is an edge detection because, rather than at the simple state of the push button, we can detect when the state changes. (If this is a drawn on a diagram, this transition looks like an)

For each successful kick, you can add points to score, just like in the game. The nextBallMove variable is the time the ball moves next. By subtracting the current time from this, you can tell how quickly the kick has been detected in the period allotted to make a successful kick. This is used to speed up or restore the speed of the ball movement.

If you want to make things further, one thing you do is make the strip longer. The game was designed for an 8-LED strip, but by changing the stripLength variable at the start of the code and adding a longer strip, you can make the ball go higher. You can get much longer strips than the simple Blink! 8-LED strips, as you shall see.

![](bbox=[0.169, 0.589, 0.226, 0.668])

# LEDs Galore

The great thing about LEDs like the APA102C is that you can control lots of LEDs with just the two connections, "almost" without limit. So, before you consider projects that involve hundreds of LEDs, let's look at some of those limits, and some ways round them.