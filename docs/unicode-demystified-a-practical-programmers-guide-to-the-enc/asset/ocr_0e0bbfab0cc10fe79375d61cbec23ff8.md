# Controlling the Prompt

The default Z Shell prompt is your system hostname followed by a percent sign (%) or when you are running as Superuser, a pound sign (#). When you run zsh as your root shell, which you normally do not, you may have a different prompt. To change your prompt, set the PS1 variable in the Bourne Again Shell. The first example that changes the prompt to the default prompt, adding a SPACE between the hostname and pound sign. The second example changes the prompt to the time followed by the name of the user. The third example changes the prompt to the one used in this chapter:

```
% PS1='%m %#'
bravo % PS1='%t %n'
10:24PM alex: PS1='%zsh #'
zsh % '
```

Table 15-6 describes the symbols used in these examples. Search for PROMPT EXPANSION in the zsh man page for a complete (and lengthy) list of symbols.

| Symbol | Display in Prompt | Table 15-6 |
|---|---|---|
| %# | A# if this is a Superuser shell; otherwise, a %. |
| %% | Always a %. |
| %~ | Pathname of the working directory. |
| %. | Working directory tail (no pathname). |
| %%! | Current event number, as in tcsh. |
| %%b | Stop printing in boldface. |
| %%B | Start printing in boldface. |
| %%D | Date in yy-mm-dd format. |
| %%m | Machine hostname, without the domain. |
| %%M | Full machine hostname, including the domain. |
| %%n | Value of USERNAME variable. |
| %n(x.true-text.false) | The n is a number (default is zero). The x is a test character from the following list. If x and n relate as true, replace this special symbol with true-text, otherwise, replace it with false-text. See the following examples.