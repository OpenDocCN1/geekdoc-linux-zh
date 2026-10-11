Suppose that you type the following text in a document and then save the document in a file that you name letter:

```
Dear Mary,
We had a go time Saturday. Let's do it again soon.
```

Use the following command to have spell take a look at the file:

```
spell letter
```

The following lines then appear on-screen:

```
nab
goo
```

Using the spell utility has a few drawbacks, however, as I describe in the following list:

+   The spell utility catches any word that it doesn't find in its dictionary file, but the word may not necessarily be a misspelling. The spell utility really compares the words in your document against those that the programmer entered into the spell utility's dictionary. In an address where the town is Ridgefield Park, for example, the spell utility reports that Ridgefield is an incorrect spelling. In fact, Ridgefield is correct but just doesn't appear in the spell utility's dictionary.
+   The spell utility lists misspelled words — but because it doesn't show you where they appear in the document, you must find them yourself.

# Sorting Stuff in Your Files: sort

Your programs can produce a list of names, but someone who uses your program may want you to sort the list. You can spend many evenings researching ways to write a program to sort the list, or you can simply use the sort utility.

Suppose that you place some names in a file that you call names. You can type the following line to sort the list:

```
sort names
```

The sort utility rearranges a list in ascending order (where the As come before the Bs and the 1s come before the 2s) and places a lowercase letter ahead of its equivalent uppercase letter. You also can change the utility to sort in descending order (where the Bs come before the As and the 2s come before the 1s) by using the -r option, as follows:

```
sort -r names
```