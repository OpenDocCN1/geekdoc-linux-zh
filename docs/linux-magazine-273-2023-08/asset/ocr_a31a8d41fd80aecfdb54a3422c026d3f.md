# Algorithm-driven team building
Team
Spirit

Instead of the coach determining the team lineup, an algorithm selects the players based on their strengths for Mike Schilli's amateur soccer team. **By Mike Schilli**

![](bbox=[0.44, 0.06, 0.77, 0.31])

![](bbox=[0.63, 0.0, 0.96, 0.17])

![](bbox=[0.55, 0.18, 0.96, 0.48])

A t the weekly pickup soccer game in my adopted hometown of San Francisco, with 16 players signed up for an eight-on-eight match, there is always the question of who is going to compete against whom on match day. Preparing the team sheet is usually something taken care of by experienced players, but it is time-consuming and it leads to endless discussions about whether the eight players on one side are simply too skilled for the other eight players, leading to a lopsided game that is no fun to play. To resolve this, I've developed an algorithm to generate the team lineup. This allows me to take an interesting excursion into the world of combinatorics and explore the development of suitable algorithms in this month's column.

How many ways are there to assign 16 players to two teams of eight players each? If one team is fixed, the opponent's team is automatically derived from the remaining participants; this means that the result is written in combinatorics style as “8 over 16,” which you compute as
(16*15*…\*10*9)/(8*7*...\*2*1)
with a result of 12,870. Any home computer can churn through that many combinations effortlessly. Even if your task was to assign 22 players to two teams of 11 each, it's in the same league with 705,432 possibilities.

courses, “You can't manage what you can't measure.” However, before you can determine the quality of a team, an expert has to grade the strength of the individual players on a few criteria, and then an algorithm can assign the teammates to teams and compare their cumulative strengths.

# Brute Force

In small event spaces like this, it is definitely an option to simply try out all the combinations, call an evaluation function on each pass, store the best scores, and output the top result at the end.

Using this brute force method for a larger event space would simply not work, because combinations can easily spiral out of control exponentially. It would make more sense to first choose a non-perfect but reasonable solution as a starting point and then change it incrementally to see if the results improve or get worse. Simulated annealing is the technical term for this process [1].

Before moving on to find better solutions, you first need a metrics function to grade the quality of each team. This metric can then be used to compare different constellations and select the best one. Like the mantra of all management

# Listing 1: teams.yaml

```
01 players:
02 - name: joe
03 skills:
04 offense: 3
05 - name: tony
06 skills:
07 defense: 2
08 goalie: 3
09 - name: fred
10 skills:
11 defense: 2
12 - name: mike
13 skills:
14 offense: 9
15 - name: manuel
16 skills:
17 goalie: 9
18 - name: mark
19 skills:
20 defense: 9
```

**Author**

Mike Schilli works as a software engineer in the San Francisco Bay Area, California. Each month in his column, which has been running since 1997, he researches practical applications of various programming languages. If you email him at msc hilli @ perlmeister.com he will gladly answer any questions.

![](bbox=[0.24, 0.78, 0.33, 0.87])