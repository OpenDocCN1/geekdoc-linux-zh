| Field | Description |
| --- | --- |
| group ID (GID) | A unique number that identifies the user's group (for file permissions) |
| comment | Usually the user's real name, but sometimes phone numbers, departments, and so on |
| home directory | The directory in which the user is placed when they log in |
| login command | The command executed when the user logs in, normally a shell |

Let’s look at each field in a little more detail. You should know what each field does and how it is used by other programs on your Linux system. Note that this type of user file is used with almost every UNIX system in the world, so once you know it for Linux, you know it for most UNIX versions.

# ## Usernames

The username is a single string, usually eight characters or less, that uniquely identifies each user. Since the username is the basis of most communications between users and other machines, the username you use (or assign to others) should be simple and obvious. Usually, this means a permutation of the user's real name. A typical username may be a combination of the user's first and last names, such as `tparker` or `timp`. The former example, composed of the first initial and last name, is fairly common in large networks.

Note that the characters in these examples are all lowercase. Case is important in Linux (as with all UNIX versions), so `tparker` and `Tparkers` are two different logins. Since most Linux commands are lowercase, convention is to also keep usernames lowercase. Underscores, periods, numbers, and some special characters are allowed, but should be avoided.

Small systems, such as on a single machine, may use more familiar names, such as the user's first name only. A small system may have users with the names `tim`, `bill`, `yvon`, and so on. If two users have the same name, then there must be some method found to differentiate between the two (such as `bill` and `billy`).

A few users like to create cryptic usernames that reflect their hobbies, nicknames, pets, lifestyle, or personality. You may find usernames such as `vader`, `grumpy`, `wizard`, and `hoops`. This type of naming is fine on small systems that are used by one or two users, but quickly becomes awkward on larger systems where other users may not know their coworkers' usernames. On the whole, if your system is used by more than a couple of people, discourage this type of username.