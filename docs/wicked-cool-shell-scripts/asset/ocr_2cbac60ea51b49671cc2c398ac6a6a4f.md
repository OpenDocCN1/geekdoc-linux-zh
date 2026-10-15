+   services.amazon.com
+   www.6pm.com
+   www.abebooks.com
+   www.acx.com
+   www.afterschool.com
+   www.alexa.com

Amazon doesn't tend to point outside its own site, but there are some partner links that creep onto the home page. Other sites are different, of course.

What if we split the links on the Amazon page into relative and absolute links?

```
$ getlinks -a http://www.amazon.com/ | wc -l
51
$ getlinks -r http://www.amazon.com/ | wc -l
222
```

As you might have expected, Amazon has four times more relative links pointing inside its own site than it has absolute links, which would lead to a different website. Gotta keep those customers on your own page!

# Hacking the Script

You can see where getlinks could be quite useful as a site analysis tool. For a way to enhance the script, stay tuned: Script #69 on page 217 complements this script nicely, allowing us to quickly check that all hypertext references on a site are valid.

# #55 Getting GitHub User Information

GitHub has grown to be a huge boon to the open source industry and open collaboration across the world. Many system administrators and developers have visited GitHub to pull down some source code or report an issue to an open source project. Because GitHub is essentially a social platform for developers, getting to know a user's basic information quickly can be useful. The script in Listing 7-6 prints some information about a given GitHub user, and it gives a good introduction to the very powerful GitHub API.

# The Code

```
#!/bin/bash
# githubuser--Given a GitHub username, pulls information about the user

if [ $# -ne 1 ]; then
    echo "Usage: $0 <username>"
    exit 1
fi
```