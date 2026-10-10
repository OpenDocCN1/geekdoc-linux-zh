# OPTIONS

—no-checkout

Do not checkout the new working tree at each iteration of the bisection process. Instead just update a special reference named $BISECT$\_$HEAD$ to make it point to the commit that should be tested.

This option may be useful when the test you would perform in each step does not require a checked out tree.

If the repository is bare, —no-checkout is assumed.