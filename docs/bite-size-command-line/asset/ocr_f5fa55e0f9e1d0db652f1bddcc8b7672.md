# top

15

# top

a live-updating summary of the top users of your system's resources

> who's using all memory

> chrome obv

let's explain some numbers in top!

# load average

3 numbers that roughly reflect demand for your CPUs on the system in the last 1, 5, and 15 minutes

if it's higher than the * of CPUs you have, that's often bad

# memory

4 numbers:

total / free / used / cached

One perhaps unexpected thing: total is not free + used!

total = free + used + cached filesystem cache

# % CPU

![](bbox=[0.065, 0.655, 0.295, 0.765])

this column is given as of % of a single core. If you have 4 cores, this can go up to 400 %!

# RES

this column is the "resident set size" aka how much RAM your process is using.

SHR is how much of the RES is shared with other processes

# htop

a prettier & more interactive version of top ★

```
1 [## ] 10% 
2 [#### ] 20% 
3 [### ] 5% 
4 [##### ] used cached 5% 
mem [####################] 4176
swp [##] 2/256
```