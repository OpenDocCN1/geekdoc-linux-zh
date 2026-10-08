# Advanced vi Tricks, Tools, and Techniques

# A Tale of Two Cities
Preface

Chuck, here are my current files:

+   > When I was acting, with my children and friends, in Mr Wilkie Collins's
> drama of The Frozen Deep, I first conceived the main idea of this
> story. A strong desire was upon me then, to
> embody it in my own person;
> and I traced out in my fancy, the state of which it would
> necessitate the presentation
> to an observant spectator, with particular
> care and interest.

As the idea became familiar to me, it gradually shaped itself into its
present form. Throughout its execution, it had complete possession
of me; I have so verified what
done and suffered in these pages.
as that I have certainly done and suffered all myself.

Whenever any reference (however slight) is made here to the condition
of the French people before or during the Revolution, it is truly made,
Ied "s/"" /

+   4. I hope you're excited to see this in command! It's a powerful way to interact
with UNIX while vi.

I will provide several examples of ways to interact with UNIX within vi.
First, I don't really want the prefix to each line, I'm going to use u to undo the line
change.

Instead, I would rather have the system actually tighten the line, ensuring that
a reasonable number of words occur on each line and no lines are too long. On
the majority of systems, there is a command called fmt or adjust to accom-
ish. To figure out which works on your system, simply use the :t command,
and feed a word or to the fmt command to see what happens:

![](bbox=[0.863, 0.573, 0.996, 0.713])

> Whenever any reference (however slight) is made here to the condition
of the French people before or during the Revolution

In this case, fmt did what I hoped, so I can be sure that the command exists on
system. If your response was command unknown, adjust is a likely synonym. If
ither exists, complain to your vendor!