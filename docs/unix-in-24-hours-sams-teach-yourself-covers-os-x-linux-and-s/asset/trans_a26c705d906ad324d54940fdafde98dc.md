

ordering is affected globally by the following options, one
or more of which may appear.

    b   Ignore leading blanks (spaces and tabs) in field com-

```
$ ls -sF | sort -b | head -4
  1 Archives/
  1 InfoWorld/
  1 Mail/
  1 News/
  1 OWL/
```

## A Tale of Two Cities
## Preface

When I was acting, with my children and friends, in Mr Wilkie Collins's drama of The Frozen Deep, I first conceived the main idea of this story. A strong desire came upon me then, to embody it in my own person; and I traced out in my fancy, the state of mind of which it would necessitate the presentation to an observant spectator, with particular care and interest.

As the idea became familiar to me, it gradually shaped itself into its present form. Throughout its execution, it has had complete possession of me; I have so far verified what is done and suffered in these pages, as that I have certainly done and suffered it all myself.

Whenever any reference (however slight) is made here to the condition of the Danish people before or during the Revolution, it is truly made, on the faith of the most trustworthy witnesses. It has been one of my hopes to add something to the popular and picturesque means of "dickens.note" 28 lines, 1123 characters

witnesses. It has been one of my hopes to add
something to the popular and picturesque means of
"dickens.note" 28 lines, 1123 characters

## A Tale of Two Cities
## Preface

When I was acting, with my children and friends, in Mr Wilkie Collins's drama of The Frozen Deep, I first conceived the main idea of this story. A strong desire came upon me then, to embody it in my own person; and I traced out in my fancy, the state of mind of which it would necessitate the presentation to an observant spectator, with particular care and interest.

As the idea became familiar to me, it gradually shaped itself into its present form. Throughout its execution, it has had complete possession of me; I have so far verified what is done and suffered in these pages, as that I have certainly done and suffered it all myself.

Whenever any reference (however slight) is made here to the condition of the Danish people before or during the Revolution, it is truly made, on the faith of the most trustworthy witnesses. It has been one of my hopes to add something to the popular and picturesque means of

```
$ awk -F: '{print $1" = "$5}' < /etc/passwd | \
awk -F, '{print $1}'| \
awk '{ if (NF > 2) print $0 }' | \
sort > who.is.who
```

```
$ alias lookup='grep -i \!* who.is.who'
$ who | head
root      console Dec  6 18:02
maritanj  ttyAa   Dec  8 21:20
efb       ttyAb   Dec  8 12:12
wifey     ttyAc   Dec  8 19:41
phamtu    ttyAe   Dec  8 21:14
curts     ttyAf   Dec  8 21:14
seifert   ttyAg   Dec  8 21:11
taylor    ttyAh   Dec  8 21:09
halcyon   ttyAi   Dec  8 18:34
jamilrr   ttyAj   Dec  8 20:25
Broken pipe
$ lookup maritanj
maritanj = Jorge Maritan
$ lookup efb
efb = Edward F. Billiard
$
```

```
$ !awk
awk -F: '{print $1" = "$5}' < /etc/passwd | awk -F, '{print $1}' | awk '{ if (NF > 2) print $0 }' | sort > who.is.who
Stopped
$
```

```
$ bg
[1]    awk -F: {print $1" = "$5} < /etc/passwd | awk -F, {print $1}
→ | awk { if (NF > 2) print $0 } | sort > who.is.who &
$
```

```
$
[1]     Done                    awk -F:
{print $1" = "$5} < /etc/passwd | awk -F,
{print $1} | awk { if (NF > 2) print $0 } | sort > who.is.who
$
```

```
$ !awk &
awk -F: '{print $1" = "$5}' </etc/passwd | awk -F, '{print $1}'
→ | awk '{ if (NF > 2) print $0 }' | sort > ! who.is.who &
[1] 27556 27557 27558 27559
$
```

