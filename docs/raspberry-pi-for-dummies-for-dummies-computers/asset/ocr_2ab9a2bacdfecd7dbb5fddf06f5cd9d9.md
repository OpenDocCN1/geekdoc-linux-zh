For other projects you work on, it's worth knowing that lists include numbers as well as strings, and can even include a mixture of strings and numbers.

For example, here's a list of answers to quiz questions:

```
my_quiz_answers = ["Isambard Kingdom Brunel", 
1945, 2012, "Suffragettes", 
7500, "Danny Boyle"]
```

A list can have any items in order. Python doesn't understand what the list means or how they are organized. To make sense of it, you need to write a program that interprets the list.

# Using lists to make a random chat program

After you've mastered the list structure, you can create a simple chat program. For this first version, you take some input from the user, display a random response, and then replace random response with whatever the user types.

Here's the program that does that. It introduces a few new ideas, but we will talk through them shortly:

+   * Chatbot – random-only version
* Example program from Raspberry Pi For Dummies

```
import random

random_replies = ["Oh really?",
"Are you sure about that?",
"Hmmmmm",
"Interesting...",
"I'm not sure I agree with that...",
"Definitely!",
"Maybe!",
"So what are you saying, exactly?",
"Meaning what?",
"You're probably right.",
"Rubbish! Absolute nonsense",
"Anyway, what are your plans for tomorrow?",
"I was just thinking exactly the same.",
"That seems to be a popular viewpoint.",
"A lot of people have been telling me."]
```