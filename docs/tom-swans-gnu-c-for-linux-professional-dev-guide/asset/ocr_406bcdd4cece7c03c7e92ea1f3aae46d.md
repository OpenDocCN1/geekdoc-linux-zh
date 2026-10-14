Listing 9.7, ascii.cpp, demonstrates how to use a for loop to display the ASCII character set of char values from 32 to 127, the usual range of common alphanumeric and punctuation characters available on most consoles.

# LISTING 9.7 ASCII.CPP

```
#include <iostream.h>

#define NUMCOLS 18  // Number of columns

unsigned char ch;
unsigned int columns;

int main()
{
    for (ch = 32; ch < 128; ch++) {
        if ( (columns++ % NUMCOLS) == 0 )
            cout << endl;  // Start a new line
        cout << ' ' << ch;
    }
    cout << endl;  // End with a new line
    return 0;
}
```

Compile and run ascii.cpp using the following commands. As shown here, the program displays the ASCII character set neatly arranged into rows and columns:

```
$ g++ ascii.cpp
$ ./a.out
  # $ % & ' ( ) * + , - . / 0 1
2 3 4 5 6 7 8 9 : ; < = > ? @ A B C
D E F G H I J K L M N O P Q R S T U
V W X Y Z [ \ ] ^ _ ` a b c d e f g
h i j k l m n o p q r s t u v w x y
z { | } ~
```

Take a look at the program's for loop. Minus its statements, the loop is written as follows:

```
for (ch = 32; ch < 128; ch++) {
    ...
}
```

The first expression in parentheses executes once before the loop begins—it initializes ch to 32, the ASCII value for a blank character. The second expression is the condition that continues or ends the loop. In this case, the expression (ch < 128) is true so long as ch's value is less than 128. When ch equals 128, the loop ends. To ensure that this happens, the third expression increments ch using the ++ operator.