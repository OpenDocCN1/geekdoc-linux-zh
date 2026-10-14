```
```text
SCRIPT b1 on :: /usr/local/minerva/bin/yaks control b1 on
SCRIPT b1 off :: /usr/local/minerva/bin/yaks control b1 off
# etc
```
```

> > **Note**  If you use mashmodes to upload new /etc/x10.conf files to system, remember to include these lines in each configuration, or cat a template to each version before it is uploaded to the CM11.

# ## Living Modes

The mode system in Mineva is called Mash, and is short for “Minerva Automated Smart Home” (no, really!) and is a way of placing the entire house into a particular state. Your house can only exist in one state at a time, and so each mode is mutually exclusive. Some examples of a mashmode are:

+   - Being on holiday
+   - Being at work
+   - Being at home, normal
+   - Being at home, working
+   - Being at home, while sick

Therefore, it is simple to issue the command:

```
```text
mashmode set holiday
```
```

and, whether triggered by a script, text message, e-mail, MTS (time-based messaging) or web interface, can put your house into a state of readiness for your holiday. Think of it as an e-mail auto-responder for home automation. This might include:

+   - Changing the automatic lighting schedule
+   - Randomly playing music and TV channels during the hours of 18:00–23:00
+   - Send an SMS to your milkman to cancel the milk
+   - E-mail a holiday reminder to your family

> > **Note**  Regardless of your security arrangements, there is no benefit in publicly announcing the fact that you’re holiday. Although the reports of burglars monitoring twitter feeds to time their breakins are largely apocryphal (there are easier ways to determine if someone’s home) there’s no point being blasé.

Setting up a mashmode is very simple as they consist of two directories containing scripts, one when the mode is begun, and another when another mode supplants it. Note that there is no differentiation if the holiday mode is replaced by “work” or “work from home”. Begin by creating a new profile:

```
```text
mashmode create holiday
```
```