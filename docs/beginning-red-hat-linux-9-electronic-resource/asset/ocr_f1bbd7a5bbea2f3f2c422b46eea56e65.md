this chapter. However, we will look at three that are widely used:

+   - The GNU General Public License (GPL)
+   - The GNU Lesser General Public License (LGPL)
+   - The original BSD License

In order to comprehend the requirements imposed by these licenses, we need to have a better understanding of what is really meant by the term *open source*. An **open source** software application or utility is one that typically provides the user complete access to its source code, and the right to produce derived works and to distribute them without restriction.

# The GNU GPL and GNU LGPL Licenses

Both the GNU GPL and the GNU LGPL fall into the category of **copyleft** licenses. These licenses permit unrestricted modification and redistribution, on condition that either all or portions of derivative works retain the same terms as the original license. These licenses were created to assure developers that any software they develop and distribute would always remain "free" and open source (here, "free" refers to rights rather than to financial matters).

Let's consider the *Battleship* example for a moment. Suppose you did go looking for a *Battleship* application, and that you found an application that is licensed under the GNU GPL. Having found it, we can certainly play the game as much as we want; we can also distribute it to our friends, and even burn it on to a CD-ROM and sell it; the license entitles you to charge enough to reasonably cover your packaging and distribution costs.

Here's the crux, though. Supposing we want to *change* the application (say, by adding some interesting artificial intelligence algorithms) and distribute the new version only in compiled form, so that our algorithms remain closed, or proprietary. If we did that, we would be in violation of the GPL, since we tried to redistribute the modified application without making the source code available. Remember, we can change the application, but if we do then we must release the *entire* source code, including the code that we added or modified, under the terms of the original license. This ensures that the *Battleship* game always remains open source, even as developers add and modify its feature set.

The GNU LGPL has one exception to this. We can use any code libraries licensed under the LGPL within our own proprietary code, and we're not obliged to release our *entire* software under the original license. For example, suppose the *Battleship* game contains a set of libraries, licensed under the LGPL, that display the game board and accept input from the user. Under the LGPL, we can incorporate these into our own version of the *Battleship* game (thereby saving time and money), but we would not be required to release our *entire* application under the terms of the LGPL.