Then accept the defaults. A symlink exists in `/usr/local/bin` to the script that loads the game. When using the KDE desktop, we had difficulty with sound because of a conflict with the KDE sound daemon `artsd`. The fix prepended a line to the `et` script that read `killall artsd`.

# ## Battle for Wesnoth

Of course, games for Fedora are not all first-person shooters like those described in the previous sections. For the more cunning among you, there exists a strategy game called Battle for Wesnoth (see Figure 9.6). In this classic turn-based strategy game, you set out to conquer your foes through a set of increasingly complex scenarios. If you have played the Windows game Age of Empires, you will feel instantly at home with Wesnoth.

Battle for Wesnoth is simple to install. All you have to do is enter the following command:

```
`# yum install wesnoth`
```

Fedora takes care of the rest. A new entry will appear in Applications, Games that will enable you to launch Battle for Wesnoth.

![](bbox=[0.08, 0.59, 0.92, 0.81])

FIGURE 9.6 Flex your strategic brain by playing Battle for Wesnoth, a rich and bountiful land of fantasy and adventure.