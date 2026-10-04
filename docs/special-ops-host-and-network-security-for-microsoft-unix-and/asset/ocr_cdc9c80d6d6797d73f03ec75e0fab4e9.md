# Notes from the Underground...

# Shooting from the Hip

Following a methodology makes sense to a security expert, whereas a hacker will often look for a quick kill instead. A typical hacker is not necessarily interested in finding every single vulnerability in your application; he is usually looking for one little mistake that will yield a high return on his investment. The burden of this battle lies on the shoulders of the creators and defenders. The good guys must identify and secure all possible avenues of attack. This is why a methodology is worth its weight in gold to a security expert.

# Using the Source

As trivial as it sounds, viewing the source of a custom-built Web application sometimes gives enough information to a potential attacker for a quick kill. All programmers are taught to comment their code, and this practice is often carried into custom Web applications. Comments that a programmer makes within compiled EXEs are vastly different, however, to comments that are openly exported to the world.

HTML for example makes use of the following convention for author comments:

```
<-- Comment goes here -->
```

Comments placed within code are normally intended for use by the authors of an application; an attacker who has this information has some insight into the thinking of the code. Comments placed within ASP or other dynamic content delivery mechanisms (PHP, SSI, and so on) are not (directly) visible to end users, but comments placed within standard HTML are (see Figure 11.1). Even simple things as author name or release dates provide decent possibilities for later attempts at username/password guessing attacks.

“Cleanse” code is valid to ensure the end user that you are not giving too much away. Viewing the source of an application allows you not only to hunt for revealing comments, but also to take a quick look under the hood, to get a slightly better understanding of what is going on.