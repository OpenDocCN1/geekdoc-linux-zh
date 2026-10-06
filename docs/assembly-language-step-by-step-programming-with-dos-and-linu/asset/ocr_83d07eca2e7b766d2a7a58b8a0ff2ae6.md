# Dividing and Conquerng 269

+   - Put on your robe.
- Let the dogs out.
- Make breakfast.
- Brush your teeth.
- Shave.
- Shower.
- Get dressed.

Brushing your tooth is on the list, but within the activity you call “brushing your teeth” is a whole list of smaller actions, as listed previously. The same can be said for most of the activities shown in the preceding list. How many individual actions, for example, does it take to put a reasonable breakfast together? And yet in one small, if sweeping, phrase, “getting up in the morning,” you embrace that whole host of small and even smaller actions without having to laboriously trace through each one.

What I am describing is the “Chinese boxes” method of fighting complexity. Getting up in the morning involves hundreds of little actions, so we divide the mass into coherent chunks and set the chunks into little conceptual boxes. “Making breakfast” is in one box, “brushing teeth” is in another, and so on. Closer inspection of any box shows that its contents can also be divided into numerous boxes, and those smaller boxes into even smaller boxes.

This process doesn’t (and can’t) go on forever, but it should go as long as it needs to order to satisfy this criterion: The contents of any one box should be understandable with only a little scrutiny. No single box should contain anything so subtle or large that it takes hours of hair-pulling to figure it out.

# Procedures as Boxes for Code

The mistake I made in writing my APL text formatter is that I threw the whole collection of 600 lines of APL code into one huge box marked “text formatter.”

While I was writing it, I should have been keeping my eyes open for sequences of code statements that worked together as some identifiable task. When I spotted such sequences, I should have set them off as pro-