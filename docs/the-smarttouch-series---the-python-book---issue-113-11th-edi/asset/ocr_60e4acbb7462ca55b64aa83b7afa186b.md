![](bbox=[0.014, 0.06, 0.77, 0.45])

# # Part one: Program a Space Invaders clone

Write your own RasPi shooter in 300 lines of Python

# ## Resources

+   * **Raspbian:** www.raspberrypi.org/downloads
* **Python:** www.python.org/doc
* **Pygame:** www.pygame.org/docs

When you're learning to program in a new language or trying to master a new module, experimenting with a familiar and relatively simple project is a very useful exercise to help expand your understanding of the tools you're using. Our Space Invaders clone is one such example that lends itself perfectly to Python and the Pygame module - it's a simple game with almost universally understood rules and logic. While the Invaders meander their way down the screen towards you, it's your job to pick them off while dodging their random fire. When one wave is conquered, another faster, more aggressive wave appears. We've tried to use many features of Pygame, which is designed to make the creation of games and interactive applications

easier. We've extensively used the Sprite class, which saves dozens of lines of extra code in making collision detection simple and updating the screen and its many actors a single-line command.

We hope you agree that this is an exciting game to play and a great tool to learn more about Python and Pygame, but our sensory system is far from overloaded here. Don't worry, as that will be covered in the next tutorial, adding animation and sound effects to our game to give it the spit and polish any self-respecting Space Invaders-inspired shooter demands...

# 01 **Setting up dependencies**

If you're looking to get a better understanding of programming games with Python and Pygame, we strongly recommend you copy the Pivaders code in this tutorial into your own program. It's great practice and gives you a chance to tweak elements of the game to suit you, be it a different ship image, changing the difficulty or the ways the alien waves behave. If you just want to play the game, that's easily

achieved too, though. Either way, the game's only dependency is Pygame, which (if it isn't already) can be installed from the terminal by typing:

```
`sudo apt-get install python-pygame`
```

# 02 **Downloading the project**

For Pivaders we've used Git, a brilliant form of version control used to safely store the game files and retain historical versions of your code. Git should already be installed on your Pi; if not, you can acquire it by typing:

```
`sudo apt-get install git`
```

As well as acting as caretaker for your code, Git enables you to clone copies of other people's projects so you can work on them, or just use them. To clone Pivaders, go to your home folder in the terminal (**cd ~**), make a directory for the project (**mkdir pivaders**), enter the directory (**cd pivaders**) and type:

```
`git pull https://github.com/russb88/pivaders.git`
```