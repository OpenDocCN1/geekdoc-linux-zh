```
random_replies = ["Oh really?",
    "Are you sure about that?",
    "Perhaps..."]
```

# Following dictionary is also heavily abbreviated chat_dict = {"happy": "I'm happy today too!", "sad": "Cheer up, mate!", "computer": "Computers will take over the world!" You already talking to you}

```
def dictionary_check(message):
    message = message.lower()
    user_words = message.split()
    smart_replies = []
    for each_word in user_words:
        if each_word in chat_dict:
            answer = chat_dict[each_word]
            smart_replies.append(answer)
    if smart_replies:
        reply_chosen = random.randint(1, len(smart_replies)) - 1
        return smart_replies[reply_chosen]
    else:
        return ""
```

```
print("What would you like to talk about today?")
```

```
user_says = ""
while user_says != "bye":
    user_says = ""
    while user_says == "":
        user_says = input("Talk to me: ")
```

```
smart_response = dictionary_check(user_says)
if smart_response:
    print(smart_response)
else:
    reply_chosen = random.randint(1, len(random_replies)) - 1
    print(random_replies[reply_chosen])
    random_replies[reply_chosen] = user_says
```

```
print("Goodbye. Thanks for chatting today. Drop in again soon!")
```