```
bank_acct checking, savings;
double checking_balance;

checking_balance = checking.retrieve_balance();
```

This will retrieve the account balance for the checking object only.

# Constructor

It is common for some part of an object to require initialization at the time it is created. In the bank_acct class, the acct_balance should be set to 0.0. This is done with a *constructor function*. If a constructor function is not provided, the compiler will supply a default constructor. The object for the class is created in a constructor, which is all the default constructor will do.

A constructor function is a special function that is a member of a class and has the same name as a class. When the object is created, the object's constructor is called. An example of a constructor function for the class *bank_acct* is:

```
// Constructor function
bank_acct::bank_acct()
{
    acct_balance = 0.0;
}
```

For global objects, the constructor is called before the main() function. For local objects, the constructor is called each time an object declaration is encountered.

A constructor can also accept parameters. It would look as follows:

```
// This creates a class for a bank account
class bank_acct {
```