# Changing Your zsh Prompt

Your default prompt (the text on the screen in front of the place you type commands) may vary a bit, depending on your Unix system; you might see just a dollar sign ($), a dollar sign and date, or other information as outlined in the Setting Your zsh Prompt Promptly sidebar. You can set your prompt to include information that's handy for you.

You actually have multiple prompts:

+   - The main prompt that you usually think of as the shell prompt. This prompt is called PS1 or just PROMPT.
+   - A secondary prompt that you see when the system requires additional information to complete a command. Logically, this prompt is called PS2.

You can change either of these prompts using the following steps. You start by finding your prompt statement (Code Listing 8.8), then modifying it in your editor (Figure 8.2).

![](bbox=[0.08, 0.1, 0.42, 0.48])

```
jdoe@sulley ~ $ grep -i PROMPT ~/.z* ; grep -i PS1 ~/.z*
/home/jdoe/.zshrc:# configuration for keys umask PROMPT and variable
/home/jdoe/.zshrc:# Set prompts
/home/jdoe/.zshrc:PROMPT="%n%m %3- %(!.#.$) "  # default prompt
/home/jdoe/.zshrc:# configuration for keys umask PROMPT and variable
/home/jdoe/.zshrc:# Set prompts
/home/jdoe/.zshrc:PROMPT="%n%m %3- %(!.#.$) "  # default prompt
jdoe@sulley ~ $
```

Code Listing 8.8 Use grep to search your configuration files for a zsh prompt statement.