![](bbox=[0.05, 0.17, 0.33, 0.43])

with respect to more desktop-type issues) and the professional (which I am, with respect to the development and server issues).

In summary, I have never, in ten years of sub-
scription, been so happy with the diversity,
scope, depth and accuracy of *Linux Journal*.
Keep up the excellent work.

–
Sean C. McCord

# What's a Few Zeros
between Friends?

Quote from Linux for Suits, February 2007.
"The 15Mbps they reserve for their Internet
service is less than 1% of that capacity."
15 kilobits per second really is pathetic.

–
Ian Stirling

# What's a Few Letters
between Friends?

In “White Box Phone” (February 2007), you
said that the OpenMoko phone came from
Funambol. I think you meant to say FiC.

Funambol is the company behind SyncML
and push mobile e-mail.

–
Bill Weinberger

# Someone Else May Have to
Decipher Your Code Someday

I’ve already made comments about Dave
Taylor’s column, and you know I’m behind his
doing this column and what it teaches. My
comment is not a criticism of that column but
what I hope is viewed as an addendum to it.

The urge to put an entire sequence of opera-
tions on “one line” (chained together via
pipes) is noble and quite understandable
when one is “in a hurry” or doing something
“quick and dirty.” It isn’t the wisest of choic-
es for beginners or “semi-production” work.

Yes, this is arguable, but I’d like to reference
something else in your magazine, page 14,
"They Said It" (February 2007), the third
quotation, “Coding up the simplest thing…”

Over time, I’ve learned that as “The next

guy", trying to read and understand code
written by “the guy before me”, that break-
ing a sequence of steps like this down into
the constituent parts makes maintainability
and supportability significantly easier.

While the original state is “easy enough” to
work with, especially for a demonstration, in
the work place, we should encourage everyone
to remember “the next guy” (and there will
always be a next guy) when we write scripts.

I would, in an environment where this might be
used by someone else and not run every five
minutes, rewrite this script with these additions:

```
# Comment this line out for debugging.
trap '/bin/rm -f $tmp1 $tmp2 $tmp3 $tmp4' EXIT
```

```
tmp1=/tmp/tmp.1.5
tmp2=/tmp/tmp.2.5
tmp3=/tmp/tmp.3.5
tmp4=/tmp/tmp.4.5
```

```
grep 'google.com/search' $ACCESSLOG | \ 
awk '{print $11}' > $tmp1
```

```
< $tmp1 cut -d':' -f2 | cut -d':' -f1
> $tmp2
sed 's/\*/ /g;s/N\*/2/g;s/q//s//`' < $tmp2
> $tmp3
```

```
sort $tmp3 | uniq -c > $tmp4
sort -rn $tmp4 | head -5
```

Yes, this seems wasteful. (I mention the five
minutes above to point out that if run more
than, say every half hour on a moderately busy
box, the methods may need to be adjusted.)
Many people will point out a number of issues
with this method of operation, and one of them
is going to be “writing to disk so much
tastes a lot of time.” Yes, it does. I’ve never
been a member of the “save the PID” crowd
or the “make it hard to troubleshoot for job
security” group either. Writing to disk a lot is
much cheaper than the rate I get paid. If it
takes an extra 20% to run, who cares as long
as it gives the right answer reliably?

Using the sequence of steps I show above,

# Regarding the Golden Age
of *Linux Journal*

After having seen in the past few issues of *LI*
readers who are disillusioned with the maga-
nine’s content, I feel I must give counterpoint.

Much like Mr. Silverton’s setup in the January
2007 issue, I began using Linux in 1995, failing
first to install Red Hat and settling in on the
astounding Slackware distribution from untold
numbers of hit-or-miss floppies. Likewise, I used
Linux in a rather amateur fashion for a number
of years. At that time, I subscribed to *Linux*
*Journal* but found only one or two articles that
grab my attention. Later, I started a Linux-based
company, designing Linux-based solutions for a
number of types of businesses. Even after
becoming a Linux “professional,” I was no more
drawn to the overall quality of *Linux Journal*.

For many months now, however, I have been
simply astonished by the quality of most
every article. I now read the magazine cover
to cover. Even the articles that are “beneath”
me often have a gem of information that I
may find intriguing.

Even more appealing is the uncanny timeli-
ness of recent issue themes. I have never real-
ly been reading edge. After all, it is a
monthly publication. Recently, though, I have
had several issues in a row that have matched
very closely my personal contemporary inter-
esta, and I have been delighted by the
breadth of your coverage. You cover amply
the needs of both the amateur (which I am,