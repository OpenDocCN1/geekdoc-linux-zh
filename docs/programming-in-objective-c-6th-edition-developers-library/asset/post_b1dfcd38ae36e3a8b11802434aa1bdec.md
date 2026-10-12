
So, the 1 array can also be set to the letters of the alphabet by writing:

```text
"c"
```

Finally, the three `p` calls:

```text
p
p
p
```

all pass a *single* argument to `p` because the compiler concatenates the strings together in the second and third calls.

# Character Strings, Structures, and Arrays

You can combine the basic elements of the C programming language to form very powerful programming constructs in many ways. In Chapter 8, "Working with Structures," for example, you saw how you could easily define an array of structures. Program 9.9 further illustrates the notion of arrays of structures, combined with the variable-length character string.

Suppose you want to write a computer program that acts like a dictionary. If you had such a program, you could use it whenever you came across a word whose meaning was not clear. You could type the word into the program, and the program could then automatically "look up" the word inside the dictionary and tell you its definition.

If you contemplate developing such a program, one of the first thoughts that comes to mind is the representation of the word and its definition inside the computer. Obviously, because the word and its definition are logically related, the notion of a structure comes immediately to mind. You can define a structure called `dictEntry`, for example, to hold the word and its definition:

```c
typedef struct {
    char word[15];
    char def[50];
} dictEntry;
```

In the preceding structure definition, you have defined enough space for a 14-letter word (remember, you are dealing with variable-length character strings, so you need to leave room for the null character) plus a 49-character definition. The following is an example of a variable defined to be of type `dictEntry` that is initialized to contain the word "blob" and its definition.

```c
dictEntry entry = {"blob", "a small rounded mass"};
```

Because you want to provide for many words inside your dictionary, it seems logical to define an array of `dictEntry` structures, such as in:

```c
dictEntry dict[100];
```

which allows for a dictionary of 100 words. Obviously, this is far from sufficient if you are interested in setting up an English language dictionary, which requires at least 100,000 entries to be of any value. In that case, you would probably adopt a more sophisticated approach, one that would typically involve storing the dictionary on the computer’s disk, as opposed to storing its entire contents in memory.

Having defined the structure of your dictionary, you should now think a bit about its organization. Most dictionaries are organized alphabetically. It makes sense to organize yours the same way. For now, assume that this is because it makes the dictionary easier to read. Later, you see the real motivation for such an organization.

Now, it’s time to think about the development of the program. It is convenient to define a function to look up a word inside the dictionary. If the word is found, the function could return the entry number of the word inside the dictionary; otherwise, the function could return $-1$ to indicate that the word was not found in the dictionary. So, a typical call to this function, which you can call `lookupWord`, might appear as follows:

```c
lookupWord(word, dict, nDict)
```

In this case, the `lookupWord` function searches `dict` for the word as contained in the character string `word`. The third argument, `nDict`, represents the number of entries in the dictionary. The function searches the dictionary for the specified word and returns the entry number in the dictionary if the word is found, or returns $-1$ if the word is not found.

In Program 9.9, the `lookupWord` function uses the `entryExists` function defined in Program 9.4 to determine if the specified word matches an entry in the dictionary.

# Program 9.9 Using the Dictionary Lookup Program

```c
#include <stdio.h>
#include <string.h>

typedef struct {
    char word[15];
    char def[50];
} dictEntry;

int entryExists(char *word, dictEntry *dict, int n);

int main() {
    char word[15];
    dictEntry dict[] = {
        {"accede", "to enter"},
        {"acumen", "intellect"},
        {"agate", "stone"},
        {"blob", "a small rounded mass"},
        {"clod", "lump"}
    };
    int n = sizeof(dict)/sizeof(dict[0]);
    int i;
    int status;

    printf("Enter a word: ");
    scanf("%s", word);
    i = lookupWord(word, dict, n);
    if (i >= 0)
        printf("Definition: %s\n", dict[i].def);
    else
        printf("Word not found.\n");
    return 0;
}

int lookupWord(char *word, dictEntry *dict, int n) {
    int i;
    for (i = 0; i < n; i++) {
        if (strcmp(word, dict[i].word) == 0)
            return i;
    }
    return -1;
}
```

Program 9.9 Output

```text
Enter a word: agate
Definition: stone
```

Program 9.9 Output (Rerun)

```text
Enter a word: accede
Definition: to enter
```

The `lookupWord` function sequences through each entry in the dictionary. For each such entry, the function calls the `entryExists` function (or uses `strcmp` directly in this implementation) to determine if the character string matches the word member of the particular dictionary entry. If it does match, the function returns the value of the variable `i`, which is the entry number of the word that was found in the dictionary. The function is exited immediately upon execution of the `return` statement, despite the fact that the function is in the middle of executing a `for` loop.

If the `lookupWord` function exhausts all the entries in the dictionary without finding a match, the `return` statement after the `for` loop is executed to return the “not found” indication (-1) back to the caller.

# A Better Search Method

The method used by the `lookupWord` function to search for a particular word in the dictionary is straightforward enough; the function simply performs a sequential search through all the entries in the dictionary until either a match is made or the end of the dictionary is reached. For a small-sized dictionary like the one in your program, this approach is perfectly fine. However, if you start dealing with large dictionaries containing hundreds or perhaps even thousands of entries, this approach might no longer be sufficient because of the time it takes to sequentially search through all of the entries.

The time required can be considerable—even though considerable in this case could mean only a fraction of a second. One of the prime considerations that must be given to any sort of information retrieval program is that of speed. Because the searching process is one that is so frequently used in computer applications, much attention has been given by computer scientists to developing efficient algorithms for searching (about as much attention as has been given to the process of sorting).

You can make use of the fact that your dictionary is in alphabetical order to develop a more efficient `lookupWord` function. The first obvious optimization that comes to mind is in the case that the word you are looking for does not exist in the dictionary. You can make your `lookupWord` function “intelligent” enough to recognize when it has gone too far in its search. For example, if you look up the word “active” in the dictionary defined in Program 9.9, as soon as you reach the word “acumen,” you can conclude that “active” is not there because, if it was, it would have appeared in the dictionary before the word “acumen.”

As was mentioned, the preceding optimization strategy does help to reduce your search time somewhat, but only when a particular word is not present in the dictionary. What you are really looking for is an algorithm that reduces the search time in most cases, not just in one particular case. Such an algorithm exists under the name of the binary search.

The strategy behind the binary search is relatively simple to understand. To illustrate how this algorithm works, take an analogous situation of a simple guessing game. Suppose I pick a number from 1 to 99 and then tell you to try to guess the number in the fewest number of guesses. For each guess that you make, I can tell you if you are too low, too high, or if your guess is correct. After a few tries at the game, you will probably realize that a good way to narrow in on the answer is by using a halving process. For example, if you take 50 as your first guess, an answer of either “too high” or “too low” narrows the possibilities down from 100 to 49. If the answer was “too high,” the number must be from 1 to 49, inclusive; if the answer was “too low,” the number must be from 51 to 99, inclusive.

You can now repeat the halving process with the remaining 49 numbers. So if the first answer was “too low,” the next guess should be halfway between 51 and 99, which is 75. This process can be continued until you finally narrow in on the answer. On the average, this procedure takes far less time to arrive at the answer than any other search method.

The preceding discussion describes precisely how the binary search algorithm works. The following provides a formal description of the algorithm. In this algorithm, you are looking for an element $x$ inside an array $M$, which contains $n$ elements. The algorithm assumes that the array $M$ is sorted in ascending order.
