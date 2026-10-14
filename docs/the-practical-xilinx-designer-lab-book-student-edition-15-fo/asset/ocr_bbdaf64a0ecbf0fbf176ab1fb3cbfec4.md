# Figure 1.5 The fastest routes between each pair of cities.

Highway 3 will be taken if you travel on the fastest route between Hooterville and Siler City or Mayberry and Siler City.

We can begin replacing pieces of this sentence with language that uses Boolean operations:

(Highway 3 is taken) IF
(one end of the route is Hooterville AND
the other end is Siler City)

Route: Hooterville -> Hwy1 -> Mayberry
time = 3

Route: Hooterville -> Hwy3 -> Siler City
time = 5

Route: Hooterville -> Hwy2 -> Mt. Pilot
time = 3

Route: Mayberry -> Hwy1 -> Hwy2 -> Siler City
time = 3 + 5 = 8

Route: Mayberry -> Hwy1 -> Hwy2 -> Mt. Pilot
time = 3 + 3 = 6

Route: Mt. Pilot -> Hwy6 -> Siler City
time = 3