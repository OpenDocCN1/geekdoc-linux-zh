```
srandom( time(NULL) ); // Seed random generator
for_each(v.begin(), v.end(), initialize);
cout << "Vector before multiply" << endl;
for_each(v.begin(), v.end(), show);
for_each(v.begin(), v.end(), multiply);
cout << endl;
cout << "Vector after multiplying * 10" << endl;
for_each(v.begin(), v.end(), show);
cout << endl;
return 0;
}

// Set rd to a floating point value between 0 and 1.0
void initialize(double &rd)
{
    rd = ( 1.0 * random() / RAND_MAX );
}

// Display the value of rd
void show(const double &rd)
{
    cout << rd << ' ';
}

// Multiply rd by 10
void multiply(double & rd)
{
    rd *= 10;
}
```

Compile and run the program to display a small vector of floating point double values between 0 and 1.0 selected at random. Enter these commands:

```
$ g++ foreach.cpp
$ ./a.out
Vector before multiply
0.5629 0.197134 0.484129 0.00931074 0.237529
Vector after multiplying * 10
5.629 1.97134 4.84129 0.0931074 2.37529
```

The program uses functions instead of explicit loops to initialize the vector, display its values, multiply them by 10, and display the final results. This demonstrates how, using functions and algorithms, you can perform any actions you want on all or some objects in a container. The program constructs a vector<double> container, simply named v, as a global variable:

```
vector<double> v(5);
```

To perform operations on the container's values, the program prototypes three functions: initialize(), show(), and multiply(). Each function declares one parameter of the same type as the objects in the container. Although that type is double in this example, it can be any type of object including a class. To perform the function on all contained objects, the program calls the STL for_each() algorithm using the following statement:

```
for_each(v.begin(), v.end(), initialize);
```