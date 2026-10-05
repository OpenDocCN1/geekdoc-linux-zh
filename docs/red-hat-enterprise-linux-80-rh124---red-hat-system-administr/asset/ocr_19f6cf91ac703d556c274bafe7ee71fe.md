CHAPTER 7 | Configuring and Securing SSH

logout

7.8. From the first terminal, exit the production1 user's shell on both serverb and servera.

```
[production1@serverb ~]$ exit
logout
Connection to serverb closed.
[production1@servera ~]$ exit
logout
[student@servera ~]$
```

7.9. Log out of servera and return to the student user's shell on workstation.

```
[student@servera ~]$ exit
logout
Connection to servera closed.
[student@workstation ~]$
```

# Evaluation

On workstation, run the lab ssh-review grade command to confirm success of this exercise.

```
[student@workstation ~]$ lab ssh-review grade
```

# Finish

On workstation, run lab ssh-review finish to complete this lab.

```
[student@workstation ~]$ lab ssh-review finish
```

This concludes the lab.

RH124-RHEL8.0-en-1-20190507

343