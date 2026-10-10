```
#file handling operations
# writing to a new file hello.txt
f = open('hello.txt', 'w', encoding = 'utf-8')
f.write("Hello Python Developers!")
f.write("Welcome to Python World")
mylist = ["Apple," "Orange," "Banana"]
# writelines() is used to write multiple lines into the file
f.writelines(mylist)
f.flush()
f.close()
```

The example above is a good one to use when you want to make a few changes to a file that you worked on before because you just need to add in one new line. This example wouldn't need to use that third line because it just has some simple words, but you can add in anything that you want to the program, just use the syntax above and change it up for what you need.

# Can I Create a Binary File?

We are going to take a little bit of a detour here and explore for a minute what we are able to do with binary files in Python. This is going to be a bit different, but it is simple and can make a difference in some of the codes that we are writing. You can complete this process in Python because you just take the data that you are working with and then make sure that it turns into a sound or an image file, rather than writing it out as a text file like before.

You can change any of the text files that we write out in this language over to a binary file if that is easiest. In fact, it doesn't matter what kind of file you are working with, whether it is a picture, sound, or text file. The most important thing that we have to remember when we are changing things into binary files is that we need to supply our data inside of the object to make it easier to expose a bit later on. We can then use the syntax below to help us get our files turned into binary files:

```
# write binary data to a file
# writing the file hello.dat write binary mode
F = open('hello.dat', 'wb')
# writing as byte strings
f.write(b" I am writing data in binary file!\n")
f.write(b" Let's write another list!\n")
f.close()
```

# How to Open a File