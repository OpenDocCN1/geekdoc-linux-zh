```
#include <iostream>

class Fraction
{
  private:
    int numerator;
    int denominator;

  public:
    void setNumerator (int num);
    void setDenominator (int denom);
    int  Numerator (void);
    int  Denominator (void);
    void print (Fraction f);
};

void Fraction::setNumerator (int num)
{
    numerator = num;
}

void Fraction::setDenominator (int denom)
{
    denominator = denom;
}

int Fraction::Numerator (void)
{

```