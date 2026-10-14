```
cin >> fp; // Read input into fp
test();
cout << "Value entered is: " << fp << endl;
cout << "Enter an integer value: ";
cin >> k;    // Read input into k
test();
cout << "Value entered is: " << k << endl;
return 0;
}

void test(void)
{
    if (!cin.good()) {
        cout << "*** Input error detected\n";
        exit(1);
    }
}
```

Compile and run getval.cpp. The program prompts you for a floating point value and then for an integer. It echoes back each value you type, as shown in this sample run:

```
$ g++ getval.cpp
$ ./a.out
Enter a floating point value: 3.14159
Value entered is: 3.14159
Enter an integer value: 1234
Value entered is: 1234
```

Run the program again, but this time, enter an illegal character when prompted for a floating point value:

```
./a.out
Enter a floating point value: xyz
*** Input error detected
```

The program detects the error, prints an error message, and halts. In the source code, function test() handles this error condition. (For more about functions, see Chapter 10, "Creating and Calling Functions.") To read a floating point value and test whether an error occurred, the program executes the statements

```
cin >> fp;
test();
```

Function test() checks whether cin.good() returns true. If not, an error occurred during the most recent input to cin. In that case, the program prints the error message and then calls exit():

```
if (!cin.good()) {
    cout << "*** Input error detected\n";
    exit(1);
}
```

Rather than halt the program upon detecting an error, you can clear it and continue. To clear errors reported by cin.good() and allow future I/O to continue normally, execute the statement

```
cin.clear();
```