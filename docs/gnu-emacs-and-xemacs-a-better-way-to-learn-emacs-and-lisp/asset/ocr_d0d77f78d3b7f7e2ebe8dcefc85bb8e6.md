Here is how you use this mode: The first step is to “conx” either a buffer or a region by pressing M-x and typing

```
conx-buffer
```

or

```
conx-region
```

You can switch buffers and repeat the command as often as you like. Each reiteration of the command adds more to the word-frequency tree. After you have accumulated enough text (how much is enough? experiment), this command opens a Conx buffer and generates new text. Press Ctrl-g when you are done with it.

Generating a word-frequency tree takes a while on a large buffer, such as an entire novel. You can save the Conx data in a file for later use by pressing M-x and typing

```
conx-save
```

You can load the saved file later by pressing M-x and typing

```
conx-load
```

Figure 21.2 is an example of a Conx session using as input Austen's *Mansfield Park* and the Joseph Conrad story “Youth”. Compare this output with Figure 21.1, the output from Docciated Press run on *Mansfield Park* alone.

![](bbox=[0.05, 0.62, 0.85, 0.94])

# Figure 21.2
Austen and Conrad Conx ed