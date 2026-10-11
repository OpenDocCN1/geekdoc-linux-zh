![](bbox=[0.02, 0.01, 0.22, 0.05])

# Programming Snapshot – Go Algorithms

(i.e., the one with the lowest value) in bestTeams and bestOff.

When storing the best results, though, it is important to avoid a hidden stumbling block: If you thought you could just keep the values of the t1 and t2 variables with the teams in a safe place, think again. Because the Go runtime modifies the teams referenced by t1 and t2 in the underlying array, you end up with garbled lineups. An array slice in Go is always just a pointer to a real array (Figure 2). If you only save the pointer, you will inevitably see arbitrary changes to the underlying array.

Lines 11 to 14 avoid this trap by duplicating the teams, once found, using Go’s built-in copy() function. It is also important to make sure that the target array slice (the first argument for copy()) is the same length as the original that you want to copy. If the length of the former is zero, copy() will simply copy zero bytes, leaving the user pulling their hair out in frustration.

So how does Listing 7 find all possible team constitutions? To do this, Listing 7 calls the perm() function from Listing 8 in line 7; the function expects an array slice of available players and a callback function that it calls exactly once for each combination it finds. With each individual datapoint, as shown in Listing 7 starting in line 7, the program can then unleash actions on the two teams, such as rating them and keeping the best results found so far.

# Help from ChatGPT

Because I was lazy, I didn’t wrack my brain to come up with the permutation algorithm in Listing 8 myself, but relied on the assistance of the all-singing, all- dancing electronic brain on ChatGPT. I simply asked ChatGPT in plain English for a method that could split an array of N players into all possible combinations of two teams. It came back with a solution within 10 seconds (Figure 3) – a live-saver for overworked programmers!

All that remained to be done was to adapt the code to the Player array element data structure used for the teams, and Listing 8 was ready. This definitely puts the fun back in programming! What you need to know, however, is that the solutions presented by Chat- GPT are often not 100-percent correct. In fact, the first result it gave me had an off-by-one bug. However, as soon as I pointed it out, the AI apologized and

![](bbox=[0.06, 0.37, 0.62, 0.95])

[] – [ ]
[a] – [ ]
[a b] – [ ]
[a b c] – [ ]
[a b c d] – [ ]
[a b c] – [d]
[a b] – [c]
[a b d] – [c]
[a b] – [c d]
[a] – [b]
[a c] – [b]
[a c d] – [b]
[a c] – [b d]
[a] – [b c]
[a d] – [b c]
[a] – [b c d]
[ ] – [a]
[b] – [a]
[b c] – [a]
[b c d] – [a]
[b c] – [a d]
[b] – [a c]
[b d] – [a c]
[b] – [a c d]
[ ] – [a b]
[c] – [a b]
[c d] – [a b]
[c] – [a b d]
[ ] – [a b c]
[d] – [a b c]
[ ] – [a b c d]

Figure 4: Valid two-by-two lineups for four players.