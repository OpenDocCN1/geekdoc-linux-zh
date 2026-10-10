
Note, too, that Application B doesn't allow the use of pipes between its functions, while Application A probably relies heavily on them. This eliminates the necessity of having to relink the entire application whenever one function changes. It also speeds up development and testing, since programmers who maintain Application A can work on smaller components that are much easier to manage.

One less obvious advantage of Application A is that it facilitates working in parallel by several developers. When programmers know that they are dealing with separate programs that must communicate with each other, they will place considerable emphasis on getting the interfaces between the modules right. This helps to eliminate lots of "spaghetti code."

You may be wondering how the user interacts with the components of Application A. One solution is for Application A to incorporate a separate user interface module. Since Application A's modules are designed to be interchangeable, it would then be possible to adapt the application for different kinds of users by changing its user interface module. The X Window System is a practical example of this. It enables the user to select a user interface from a wide range of choices in a what-you-see-is-what-you-get fashion.

![](img/b25e7c0c327bab571582b25f020f3286_164_0.png)

![](img/b25e7c0c327bab571582b25f020f3286_164_1.png)

## 7.8 Look for the 90-percent solution

When overnight delivery services like Federal Express first appeared on the American landscape, people marveled at their efficiency. Imagine a pony express that would get your package to someone across the country not in a month or a week, but overnight. To many it was a dream come true. This service revolutionized the way we do business today.

The rapid ascent of Federal Express and other overnight delivery services raised a serious question: Why couldn't the U.S. Postal Service provide this service? As we all know, the U.S. Postal Service can and does provide overnight delivery today. Still, many people believe that the commercial package delivery services do a better job. Why? It's because the commercial services implement the 90-percent solution.

Doing 90 percent of anything is always easier than doing 100 percent. In Federal Express's case, they do not provide the same level of service out in the hinterlands as they do for an area near a major city. In major U.S. cities, it seems as though Federal Express pickup boxes are on nearly every other street corner. But try to find one in a remote town in the hills of Montana. It simply isn't profitable for Federal Express, so it isn't done. The U.S. Postal Service, being a U.S. government organization, must provide equal service to all U.S. citizens. Therefore, you will find mailboxes on street corners in virtually every small town across the U.S.

By government fiat, the U.S. Postal Service must carry out the 100-percent solution. Meanwhile, operating as an independent carrier, Federal Express can focus on the highly profitable and much easier to optimize 90-percent solution. The result? Federal Express delivers packages the next day (and even sometimes on the same day) at a low cost to businesses and consumers. The U.S. Postal Service, for all its inefficiencies, does about as reasonable a job as one could expect from an organization that must do it all for everyone.

The 90-percent solution is one that results from deliberately ignoring those aspects of the problem that are costly, time-consuming, or difficult to implement. You can readily solve most problems in the world if you are given the opportunity to discard the toughest 10 percent of them.

When fast-track Unix and Linux software developers design an application program, they strive for the solution that will give them the biggest bang for their buck, so to speak. This means eliminating those functions that few people use and that are costly to implement. They ruthlessly cut such functions from the product requirements, often with the attitude of if someone needs this capability badly enough, they can do it themselves.

Obviously, there are some situations, such as heart transplants, where a 90-percent solution won't suffice. These are rare in the computer world, though. Remember that most software is a compromise in that it is never finished, only released. If, by definition, software can never be finished, one can never develop software that offers a 100-percent implementation. By recognizing the 90-percent solution as a reasonable measure of completeness, it becomes easy to write applications that appeal to most of the user population.

That is part of the reason for Unix's success. While it avoids trying to be everything to everyone, it meets the needs of most. The rest can write their own operating systems.

## 7.9 Worse is better

Anyone who has ever been in the military knows that there is the right way, the wrong way, and the military way.

The "right way" is the way that I know is right, you know is right, and every normal person knows is right. It is what we consider correct-in every aspect. It is undeniably proper. The shoe fits. It works.

The "wrong way" stands as the inverse of the right way. Blatantly incorrect, it is wrong, dead wrong, no matter who looks at it. Your mother and father know it's wrong, your kid brother agrees, and your broker guarantees it.

The most enigmatic, the "military way" is by far the most interesting of the three. While the right way and the wrong way coexist in an inverse relationship, the military way surrounds itself in a cloud that is neither black nor white. It is the way in which those things that ought to work mysteriously fail, and-better yet-those things that should fail miserably unwittingly achieve unprecedented success.

The "Unix way" is akin to the military way. If you listen to the purists, Unix should have withered and died 20 years ago. Yet, here it is in its entire parasitic splendor, feeding off the criticisms leveled at it by its critics and growing stronger every day.

Ingrained within the Unix way is the paradoxical notion that "worse is better." Many claim that Unix is not nearly as good as such-and-such system because its user interface is terrible or that Unix is too simple to be considered a serious operating system. Linux, too, once received its share of criticism because it lacked a reasonable GUI, it was difficult to install, and it lacked a viable office application software package.

Yet, if Unix is worse than most other systems in so many ways, then it only proves that "worse" has a better chance of survival than that which is either "right" or "wrong." For Unix and Linux have shown a remarkable ability to persist in a world where new technologies continually render existing technologies obsolete.

There exists a school of thought in the computer world that says that all proper designs should have four characteristics: simplicity, correctness, consistency, and completeness. Designs should be simple, correct (bug-free) in all observable aspects, consistent throughout, and complete in that they must cover all cases one can reasonably expect.

Most Unix programmers will agree that applications and systems should be simple, correct, consistent, and complete. The key is how they prioritize those characteristics. Although the proper system designer strives for completeness at the expense of simplicity, Unix developers elevate simplicity to the primary priority. So the proper system designer levels criticism at Unix, not so much because it is improper, but because its priorities are reversed. In that sense, it is worse than the proper system.

Unix aficionados, on the other hand, point to the survival characteristics of worse and say that worse is better. Look at the VHS videotape format, they say. VHS tapes are big and "clunky" compared to Sony's Beta tapes. They do not record nearly as well. They are hardly as much for archival disks. Yet VHS tapes...
