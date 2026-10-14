```
cout << endl;

// Use predicate function to count negative values
//
int count = 0;
vector<long>::iterator p;
p = find_if(v.begin(), v.end(), isMinus);
while (p != v.end()) {
    count++;
    p = find_if(p + 1, v.end(), isMinus);
}
cout << "Number of values: " << VSIZE << endl;
cout << "Negative values : " << count << endl;
}

return 0;
}

// Set ri to a signed integer value
void initialize(long &ri)
{
    ri = ( random() - (RAND_MAX / 2) );
    // ri = random();
}

// Display value of ri
void show(const long &ri)
{
    cout << ri << " ";
}

// Returns true if ri is less than 0
bool isMinus(const long &ri)
{
    return (ri < 0);
}
```

Compile and run the test program to display a series of signed integer values selected at random and then count the number of negative values. Although this is an arbitrary action, it might be part of a test for a random number generator's distribution. Enter these commands (the program's output is shortened to save room here):

```
$ g++ findif.cpp
$ ./a.out
Vector of signed long integers
-242086306 -674155175 267974268 -447339946 438491145
Number of values: 24
Negative values : 15
```

The program defines a vector of long integers using the following directive and statement:

```
#define VSIZE 24    // Size of vector
vector<long> v(VSIZE);  // Vector object
```