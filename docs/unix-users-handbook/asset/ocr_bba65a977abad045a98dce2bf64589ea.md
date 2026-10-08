```
```
martyp $ history -20
116    history 128
117    history 128 | more
118    history 200
119    alias
120    history 1
121    inv
122    env
123    env | more
124    history 1
125    more .profile
126    env | grep HIS
127    exit
128    env
129    env | grep HIS
130    more .profile
131    history
132    history 0
133    history
134    history -n
135    history 100
136    history -20
martyp $
```
```

The **-20** goes back from the current command a full 20 commands. In this case, **history** is using the current command as the default place to begin producing the list. You can list the last 20 commands *preceding* the current command by specifying the range *-1 -20*, as shown in the following example:

```
```
martyp $ history -1 -20
136    history -20
135    history 100
134    history -n
133    history
132    history 0
131    history
130    more .profile
129    env | grep HIS
128    env
127    exit
126    env | grep HIS
125    more .profile
124    history 1
123    env | more
```
```