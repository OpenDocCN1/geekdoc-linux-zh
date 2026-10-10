824  Chapter 14

# Putting It All Together

Now that you’ve learned what goes on behind the scenes in most simple games, why not try your hand at creating one yourself? Perhaps you could start by reprogramming an old classic for SVGAlib. I find that it’s a lot easier to code if you know exactly how you want the finished product to look. Obviously, if your intention is to duplicate an existing game, then that won’t be a problem. Figure 14.2 shows Breakout, an old favorite from Atari that many budding programmers clone as they “cut their teeth.”

> **Note:**
> Did you know that *Breakout* was created by Steve Jobs and Steve Wozniak, while Jobs worked at Atari?

Another fairly easy one that still involves timing is Tetris. Hey, you might think it’s dull, but the chicks love it.

# Conclusion

It’s hoped that the basic techniques presented in this chapter will help you develop the games you’ve always wanted to code but never knew how. Of course, SVGAlib is ideal for gaming on Linux because it’s always had integral full-screen access, not to mention the fastest drawing functions this side of the Pecos. It’s kind of amazing how everything fits together now, isn’t it?

Using the drawing primitives from Chapter 3 and 4, font handling from Chapter 7, graphic file input from Chapter 9, and animation from Chapter 10, you should now be able to put together a game that can stand its own against many others.

# Summary Of Functions Introduced In This Chapter

Here is a summary of the functions covered in this chapter:

+   - void gl\_putboxmask(int x, int y, int w, int h, void \*dp)
+   - void gl\_copybox(int x1, int y1, int w, int h, int x2, int y2)

![](bbox=[0.14, 0.77, 0.96, 0.97])