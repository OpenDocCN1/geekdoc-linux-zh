# IN-DEPTH

# Programming Snapshot – Go and R

Figure 6 shows an excerpt from this in-termediated result. Based on this, ZZ Top was played exactly once at 19.00 hours, while no fewer than 11 entries with Linkin Pop pop up at 20.00 hours. There are several different ways to filter out only the top performers from this view (e.g., Linkin Park at 20.00 hours). One method that relies entirely on R’s stan-dard functions is as follows: Sort the

```
```
$ hourly.r
        artistName     hour   x
19          Rainbow    0     4
28          Sparkys    1     9
30          Sparkys    2    10
31          Sparkys    3    14
32          Sparkys    4     7
33      The Killers    6     1
36  Eros Ramazzotti    7     7
40 Adriano Celentano    8     1
48  Eros Ramazzotti    9     4
56          Alice   10     1
59     Ace of Base   11     1
64     Ace of Base   12     1
68     Amy Winehouse  13     3
72    Foster The People 14     4
75        The Monkees  15     2
76     Ace of Base   16     3
111  Eros Ramazzotti  17     5
161         Falco   18     7
243        Guster   19     7
349   Linkin Park   20    11
460       Jan Delay  21     9
596       Jan Delay  22    10
782   Element of Crime  23    12
```
```

# Figure 7: Which artists are played back most frequently at what time?

![](bbox=[0.06, 0.61, 0.62, 0.78])

# Figure 8: Spotify – incorrectly – considers the author to be a light-beer drinker.

dataframe by hour (ascending) and the number of events (descending). Using deduplication, the algorithm then only keeps the first entry per each hour value and discards the rest. The top perform-ers for each hour value remain.

Line 10 sorts the previously generated agg dataframe, according to the order( ) function specified in the square brackets. Its first parameter is the (positive) field name for the hour value; the second is the (negative) value for the counter de-termined by the length function. In R, the newly created column by the aggre-gation function goes by the name of x and contains the number of results in this case.

Line 11 runs a recode statement over the dataframe now named winners and uses ldup1|cat(d winners[2]) to specify that the second field (i.e., the hour value; R arrays always start with an index of 1, not 0) must be present once only in the result. Consequently, the function will only keep the previously forward sorted highest result for hour values with the associated artist and will discard all others.

That takes care of the list with the most popular bands, as a function of the time of day at Perlmeister Studios! Fig-ure 7 shows the output of the hourly.r program (Listing 4). After midnight, it’s

either embarrassing oldies from the 1980s (Rainbow; as, I vaguely recall, once from 1:00am to 4:00am, every sin-gle track by the band Sparks), after de-veloping a Netflix documentary featuring the band and proceeding to play back their songs for four hours. The next day at work was terrible, of course, but you only live once.

From experience, users can spend days tinkering with R to find the right data structure and methods that will often implement exactly what they want in just three lines. The reasons for this probably include the age of the lan-guage, which comes with a sort of anti-Python mindset (“Waddya mean, there’s only one way to do this?”), and the many packages that have been released in an uncoordinated fashion over the de-cades since the original release. A Google search for a particular problem will often reveal three or four different approaches to solve the same issue. The training book by Robert I. Kabaoff [1] does a good job of explaining some basic procedures, but it is by no means an ex-tensive reference.

# More Secrets

If you rummage further in the Spotify dossier’s ZIP file, you are likely to un-earth a few more data treasures. For example, Spotify’s Inferences.json file contains ascertained facts about the user – presumably to help Spotify serve up appropriate ads that the lis-tener will also respond to.

In my case, Spotify assumed I had a preference for “Light Beer” (Figure 8), which is a joke and totally wrong – as anyone who knows me can attest to if it came to a pinch! This is a likely explana-tion of Bud Light ads start popping up on my screen.

# Info

+   1. Kabaoff, Robert I. *R in Action, Second Edition*. Manning, May 2015: [https://www.manning.com/books/r-in-action-second-edition](https://www.manning.com/books/r-in-action-second-edition)