```
cout << "E : Meters to feet"      << endl;
cout << "F : Feet to meters"      << endl;
cout << "I : Inches to centimeters" << endl;
cout << "K : Kilometers to miles"   << endl;
cout << "M : Miles to kilometers"   << endl;
cout << "Q : Quit"                  << endl;
}

// Prompt for user command
void getCommand(char &command)
{
    cout << "Command? ";
    cin >> command;
}

// Prompt for input value
void getValue(double &value)
{
    cout << "Value to convert? ";
    cin >> value;
}

// Convert inches to centimeters
void inchesToCentimeters()
{
    double value;  // Local variables
    double result;

    cout << "Inches to Centimeters" << endl;
    getValue(value);
    result = value * 2.54;
    cout << value << " inches == ";
    cout << result << " centimeters" << endl;
}
```

Compile and run the program using the usual commands. Select a menu choice and enter a value to convert (to save space here, only the Inches to Centimeters command is finished).

Enter the following commands to try the program:

```
$ g++ metrics.cpp
$ ./a.out
Metrics Converter : Menu
I : Inches to centimeters
...
Q : Quit
Command? i
Inches to Centimeters
Value to convert? 12
12 inches == 30.48 centimeters
```

The program's listing shows a common use for reference parameters—prompting for and initializing variables. The program prototypes two such functions:

```
void getCommand(char &command);
void getValue(double &value);
```