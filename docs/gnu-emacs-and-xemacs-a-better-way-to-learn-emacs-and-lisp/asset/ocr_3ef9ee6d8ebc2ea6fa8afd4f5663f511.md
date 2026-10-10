possible permutations. Nevertheless, a little experimentation might provide you with the exact command you need. You might want to type up a cheat sheet containing your favorite score-command permutations or create simpler keybindings for them.

These commands can also be initiated from the menus, but you are prompted for the sequence of code letters. It is easier (for me, at least) to work up a few effective formulae and type them in directly as commands.

After your main groups have been affected by a score file, you can filter the Summary buffer with scores using these commands:

+   * `V m` You are prompted for a numerical score. All articles with a score less than the one you entered are marked as already read.
+   * `V x` This time, the *score you enter* at the minibuffer prompt is used to expunge or delete all articles with a lesser score by making an entry in the group score file.

# ### Adaptive Scoring

If the explanation of score commands led you to reflect on our brief tenure upon this earth, you might be interested in letting Gnus do the scoring for you based on the articles you delete, read, and save. This is a transparent, behind-the-scenes technique of scoring with no direct user interaction. To enable adaptive scoring, you need to change the `nil` value of the variable `gnus-use-adaptive-scoring` to `t`. You can do this with a `setq` statement in your `/.gnus` file:

```
(setq gnus-use-adaptive-scoring t)
```

You can be more specific in this statement. In place of `t`, you can use either `word` or `line`. The former uses individual words in the subject header for scoring, and the latter uses several of the header lines in addition to the subject line. The `line` choice is probably more useful in most cases.

You can also use Customize to change the value. Press `M-x` and type `customize-group`

When prompted, type `gnus-score-adapt`

A Customize buffer appears, containing numerous changeable variables related to adaptive scoring, as shown in Figure 18.5. The first one is the toggle for adaptive