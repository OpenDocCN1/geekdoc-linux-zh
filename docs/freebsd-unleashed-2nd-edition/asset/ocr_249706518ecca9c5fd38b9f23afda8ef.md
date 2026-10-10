either nothing happens or the statements inside `else`, if present, are executed. Listing 12.6 uses much of what you have learned up to this point, including `if`, `elif`, and `else` to play a simple number-guessing game. Note that line 10 uses `jot`, a little command-line random-number-generating tool. The arguments in this case to its `-r` option are the number of results to return (1), the lower bound (1), and the upper bound (`$up_limit`).

# LISTING 12.6 A Simple Number-Guessing Game

```
```bash
1. #!/bin/sh
2. # Number guessing game
3. clear
4. guess_count=1 # Initialize the guess counter to 1
5. echo
6. echo "Number guessing game written in bourne shell script."
7. echo
8. echo -n "Enter upper limit for guess: "
9. read up_limit
10. rnd_number=`jot -r 1 1 $up_limit` # Get a random number
11. echo
12. echo "I've thought of a number between 1 and $up_limit."
13. echo
14. echo -n "Please guess a number between 1 and $up_limit: "
15. read guess
16. # Check the guess against the random number.
17. while true
18. do
19. if [ $guess -gt $rnd_number ]
20. then
21. echo
22. echo "Your guess was too high. Please try again."
23. guess_count=`expr $guess_count + 1`
24. echo -n "Please guess a number between 1 and $up_limit: "
25. read guess
26. elif [ $guess -lt $rnd_number ]
27. then
28. echo
29. echo "Your guess was too low. Please try again."
30. guess_count=`expr $guess_count + 1`
31. echo -n "Please guess a number between 1 and $up_limit: "
32. read guess
33. else
34. break
35. fi
```
```