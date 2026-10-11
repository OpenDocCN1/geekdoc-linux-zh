# IN-DEPTH

Programming Snapshot – Go Geolocation Game

![](bbox=[0.55, 0.04, 0.96, 0.35])

# Photo location guessing game in Go
# Treasure Hunt

A geolocation guessing game based on the popular Worldle evaluates a player’s guesses based on the distance from and direction to the target location. Mike Schilli turns this concept into a desktop game in Go using the photos from his private collection. By Mike Schilli

After the resounding success of the Worldle [1] word guessing game, it didn’t take long for the first look-alikes to rear their heads. One of the best is the entertaining Worldle [2] geography game, where the goal is to guess a country based on its shape. After each unsuccessful guess, Worldle helps the player with information about how far the guessed country’s location is from the target and in which direction the target country lies.

Not recognizing the outline of the country in Figure 1, a player’s first guess is the Principality of Liechtenstein. The Worldle server promptly tells the player that the target location is 5,371 kilometers away from and to the east of this tiny European state. The player’s second guess is Belarus, but according to the Worldle server, from Belarus you’d have to travel 4,203 kilometers southeast to get to the target. Mongolia, the third attempt, overshoots the mark, because from there you’d have to go 3,476 kilometers to the southwest to arrive at the secret destination.

Slowly but surely, the player realizes that the secret country must be somewhere near India. And then, on the fourth try, Pakistan turns out to be correct! Worldle is a lot of fun, with a new country posted for guessing every day.

# ## Private Snapshots

Now, instead of guessing countries, I thought it would be fun to randomly select a handful of photos from my vast cell phone photo collection, which has grown wildly over the years. Analyzing each photo’s GPS data, the game engine makes sure the photos in one round were taken a great distance from one another. Initially, the computer selects a random photo from the set as a solution. It keeps this a secret, of course, and then shows the player a randomly selected photo, along with details of how many kilometers lie between the place where the random photo was taken and the target location, along with the compass direction in which the player has to move across the world to get there.

Armed with this information, the player now has to guess which picture from the remaining selection is the secret photo. The player clicks on the

![](bbox=[0.49, 0.62, 0.9, 0.94])

**Author**
Mike Schilli works as a software engineer in the San Francisco Bay Area, California. Each month in his column, which has been running since 1997, he researches practical applications of various programming languages. If you email him at mschilli@perlmeister.com he will gladly answer any questions.