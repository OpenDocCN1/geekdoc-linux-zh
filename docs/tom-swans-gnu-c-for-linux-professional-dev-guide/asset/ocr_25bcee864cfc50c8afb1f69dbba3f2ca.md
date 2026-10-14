# LISTING 12.4 CONTINUED

```
dt_day = day;
dt_year = year;
}
void display();
};

int main()
{
    TDate t1;
    TDate t2 = TDate(12, 31, 1999);  // Requires default ctor
    TDate t3(1, 1, 2000);             // Impractical, but allowed
    TDate t4(t3);                     // Uses parameterized ctor
    TDate t4(t3);                     // Makes t4 a copy of t3
    TDate t5 = t4;                    // Copies t4 into t5

    t1.Display();  // Call member function for each object
    t2.Display();
    t3.Display();
    t4.Display();
    t5.Display();

    return 0;
}

// The TDate class Display member function
void TDate::Display()
{
    cout << dt_month << "/" << dt_day << "/" << dt_year << endl;
}
```

The modified TDate class’s default constructor is declared and implemented directly in the class:

```
public:
    TDate() { dt_month = 0; dt_day = 0; dt_year = 0; }
```

This format might seem strange at first, but it is merely a shorthand version of C++ source code that you could write in long form like this:

```
public:
    TDate()
    {
        dt_month = 0;
        dt_day = 0;
        dt_year = 0;
    }   // No semicolon here!
```

Compare both versions character for character and you’ll see they are identical (except for the comment). Notice especially the placement of semicolons, which as always, terminate statements, and never follow a compound statement block’s closing brace.