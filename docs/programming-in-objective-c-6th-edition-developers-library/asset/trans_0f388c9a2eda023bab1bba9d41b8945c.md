
输入你的文本。  
完成后，按“RETURN”键。

温迪抬头望向天花板，那里一堆千层面正像斑驳的山脉一样悬垂着。几秒钟内，她头上就戴上了由瑞可塔奶酪做成的卷发和番茄酱王冠。牛肉块在她额头上形成了肉疙瘩。随着第二次撞击，她的烹饪加冕仪式完成了。

返回

上面的文本共有 48 个单词。

```c
printf ("\aSYSTEM SHUT DOWN IN 5 MINUTES!\n");
```

```c
printf("%i\t%i\t%i\n", a, b, c);
```

```c
printf("\\t is the horizontal tab character.\n");
```

\t 是水平制表符。

```c
printf ("\"Hello,\" he said.\n");
```

```c
char letters[] =
   { "abcdefghijklmnopqrstuvwxyz
ABCDEFGHIJKLMNOPQRSTUVWXYZ" };
```

```text
char letters[] =
{ "abcdefghijklmnopqrstuvwxyz
ABCDEFGHIJKLMNOPQRSTUVWXYZ" };
```

"abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ"

```c
char letters[] =
    { "abcdefghijklmnopqrstuvwxyz"
      "ABCDEFGHIJKLMNOPQRSTUVWXYZ" };
```

```c
printf ("Programming in C is fun\n");
printf ("Programming" " in C is fun\n");
printf ("Programming" " in C" " is fun\n");
```

```c
struct entry word1 = { "blob", "an amorphous mass" };
```

```c
struct entry dictionary[100];
```

```c
entry = lookup (dictionary, word, entries);
```

```c
// Program to use the dictionary lookup program

#include <stdio.h>
#include <stdbool.h>

struct entry
{
   char word[15];
   char definition[50];
};

bool equalStrings (const char s1[], const char s2[])
{
   int i = 0;
   bool areEqual;

   while ( s1[i] == s2[i] &&
            s1[i] != '\0' && s2[i] != '\0' )
      ++i;

   if ( s1[i] == '\0' && s2[i] == '\0' )
      areEqual = true;
   else
      areEqual = false;

   return areEqual;
}
```

```c
// function to look up a word inside a dictionary

int lookup (const struct entry dictionary[], const char search[],
            const int entries)
{
    int i;
    bool equalStrings (const char s1[], const char s2[]);

    for ( i = 0; i < entries; ++i )
        if ( equalStrings (search, dictionary[i].word) )
            return i;

    return -1;
}

int main (void)
{
    const struct entry dictionary[100] =
    { { "aardvark", "a burrowing African mammal" },
      { "abyss",    "a bottomless pit" },
      { "acumen",   "mentally sharp; keen" },
      { "addle",    "to become confused" },
      { "aerie",    "a high nest" },
      { "affix",    "to append; attach" },
      { "agar",     "a jelly made from seaweed" },
      { "ahoy",     "a nautical call of greeting" },
      { "aigrette",  "an ornamental cluster of feathers" },
      { "ajar",     "partially opened" } };

    char word[10];
    int entries = 10;
    int entry;
    int lookup (const struct entry dictionary[], const char search[],
                const int entries);

    printf ("Enter word: ");
    scanf ("%14s", word);
    entry = lookup (dictionary, word, entries);

    if ( entry != -1 )
        printf ("%s\n", dictionary[entry].definition);
    else
        printf ("Sorry, the word %s is not in my dictionary.\n", word);

    return 0;
}
```

输入单词：**agar**

一种由海藻制成的果冻

输入单词：accede

很抱歉，单词 accede 不在我的词典中。

```c
compareStrings ("alpha", "altered")
```

```c
compareStrings ("zoot", "yucca");
```

```c
// Dictionary lookup program
#include <stdio.h>
struct entry
{
	char word[15];
	char definition[50];
};

// Function to compare two character strings
int compareStrings (const char s1[], const char s2[])
{
	int i = 0, answer;

	while ( s1[i] == s2[i] && s1[i] != '\0' && s2[i] != '\0' )
		++i;

	if ( s1[i] < s2[i] )
		answer = -1; 			/* s1 < s2 */
	else if ( s1[i] == s2[i] )
		answer = 0; 			/* s1 == s2 */
	else
		answer = 1; 			/* s1 > s2 */

	return answer;
}
```

```c
// Function to look up a word inside a dictionary
int lookup (const struct entry dictionary[], const char search[],
         const int entries)
{
int low = 0;
int high = entries - 1;
int mid, result;
int compareStrings (const char s1[], const char s2[]);
while ( low <= high )
{
mid = (low + high) / 2;
result = compareStrings (dictionary[mid].word, search);
if ( result == -1 )
low = mid + 1;
else if ( result == 1 )
high = mid - 1;
else
return mid;   /* found it */
}
return -1;            /* not found */
}
int main (void)
{
const struct entry dictionary[100] =
{ { "aardvark", "a burrowing African mammal"             },
{ "abyss",    "a bottomless pit"                       },
{ "acumen",   "mentally sharp; keen"                    },
```

```c
{ "addle", "to become confused" },
{ "aerie", "a high nest" },
{ "affix", "to append; attach" },
{ "agar", "a jelly made from seaweed" },
{ "ahoy", "a nautical call of greeting" },
{ "aigrette", "an ornamental cluster of feathers" },
{ "ajar", "partially opened" } };

int entries = 10;
char word[15];
int entry;
int lookup (const struct entry dictionary[], const char search[],
const int entries);

printf ("Enter word: ");
scanf ("%14s", word);

entry = lookup (dictionary, word, entries);

if ( entry != -1 )
printf ("%s\n", dictionary[entry].definition);
else
printf ("Sorry, the word %s is not in my dictionary.\n", word);

return 0;
}
```

输入单词：**aigrette**

一种装饰性的羽毛簇

输入单词：**acerb**

很抱歉，该单词不在我的词典中。

```c
// Function to convert a string to an integer

#include <stdio.h>

int strToInt (const char string[]) 
{
    int i, intValue, result = 0;

    for ( i = 0; string[i] >= '0' && string[i] <= '9'; ++i ) 
    { 
        intValue = string[i] - '0';
        result = result * 10 + intValue;
    }

    return result;
}

int main (void)
{
    int strToInt (const char string[]);

    printf ("%i\n", strToInt("245"));
    printf ("%i\n", strToInt("100") + 25);
    printf ("%i\n", strToInt("13x5"));

    return 0;
}
```

```c
while( s1[i] == s2[i] && s1[i] != '\0' )
```

```c
substring ("character", 4, 3, result);
```

```c
substring("two words", 4, 20, result);
```

```c
index = findString ("a chatterbox", "hat");
```

```c
insertString (text, "per", 10);
```

```c
replaceString (source, s1, s2);
```

```c
replaceString (text, "1", "one");
```

```c
replaceString(text, "*", "");
```

```c
do
   stillFound = replaceString (text, " ", "");
while ( stillFound );
```

```c
#include <stdio.h>

int main (void)
{
    int    count = 10, x;
    int    *int_pointer;

    int_pointer = &count;
    x = *int_pointer;

    printf ("count = %i, x = %i\n", count, x);

    return 0;
}
```

```c
int count = 10, x, *int_pointer;
```

```c
#include <stdio.h>
int main (void)
{
    char  c = 'Q';
    char  *char_pointer = &c;

    printf ("%c %c\n", c, *char_pointer);

    c = '/';
    printf ("%c %c\n", c, *char_pointer);

    *char_pointer = '(';
    printf ("%c %c\n", c, *char_pointer);

    return 0;
}
```

```c
// More on pointers
#include <stdio.h>

int main (void)
{
    int i1, i2;
    int *p1, *p2;

    i1 = 5;
    p1 = &i1;
    i2 = *p1 / 2 + 10;
    p2 = p1;

    printf ("i1 = %i, i2 = %i, *p1 = %i, *p2 = %i\n", i1, i2, *p1, *p2);

    return 0;
}
```

i1 = 5, i2 = 12, *p1 = 5, *p2 = 5

```c
if ( (*datePtr).month == 12 )
```

```c
// Program to illustrate structure pointers
#include <stdio.h>

int main (void)
{
    struct date
    {
        int month;
        int day;
        int year;
    };

    struct date  today, *datePtr;

    datePtr = &today;

    datePtr->month = 9;
    datePtr->day = 25;
    datePtr->year = 2015;

    printf ("Today's date is %i/%i/%.2i.\n",
            datePtr->month, datePtr->day, datePtr->year % 100);

    return 0;
}
```

