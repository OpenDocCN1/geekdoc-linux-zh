```
set
{
    denominator = value;
}
}

public void print ()
{
    Console.WriteLine("The value of the fraction is {0}/{1}",
        numerator, denominator);
}
}

class example
{
    public static void Main()
    {
        Fraction myFract = new Fraction();

        myFract.Numerator = 1;
        myFract.Denominator = 3;

        myFract.print ();
    }
}
```