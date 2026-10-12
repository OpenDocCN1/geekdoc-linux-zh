```
/* Function to compute the square root of a number.
If a negative argument is passed, then a message
is displayed and -1.0 is returned.
*/

float squareRoot (float x)
{
const float epsilon = .00001;
float guess = 1.0;
float absoluteValue (float x);

if ( x < 0 )
{
printf ("Negative argument to squareRoot.\n");
return -1.0;
}

while ( absoluteValue (guess * guess - x) >= epsilon )
guess = ( x / guess + guess ) / 2.0;

return guess;
}
```