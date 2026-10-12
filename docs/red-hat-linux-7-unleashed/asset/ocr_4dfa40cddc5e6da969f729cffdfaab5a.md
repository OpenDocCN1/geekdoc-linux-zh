```
Listing 7.1 continued

```
ON -"SERVER_NOTICE "%\*\*\*\*\* Notice -- Received KILL*" {
    IF ( nkp.srv{S12} > -1 )
    {
        { nkp.msg S8 S10 }
        { nkp.msg S8 $10 S10 }:}
        "ASSIGN nkp.path S8 -
    }
}

# Function to strip the less significant part of an internet hostname
alias userdomain {
    @ function_return = LEFT($INDEX(@ $0) #0/#{@}MID(S{1+INDEX(. $0)) 99 $0)
}

# Who is that ?
alias * { echo * @ho * $0|\${userdmain/\${userhost()}} * S1 -

# /w [nickname>] get info on someone
# /q [nickname>] query someone
# /m <nickname> <text> send a message
# /n <nickname> <text> send a notice
# /r <text> reply to last message I got
# /a <text> followup on my last message

alias w whois
alias q query
alias m msg
alias n notice
alias r msg $.
alias a msg $.

# /j <channel> join a channel
# /l <channel> list people in a channel
# /ll list in the current channel
# /i <nickname> [ <channel>] invite someone
# /hop leave the current channel

alias j join
alias i who
alias ll who *
alias i invite
alias hop part SC

# /o <nickname> [ <nickname> <nickname>] give channel op status
# /d <nickname> [ <nickname> <nickname>] remove channel op status
# /k <nickname> kick someone
# /mo [+|-|:<modechans> change current channel mode

alias o mode SC +ooo
alias d mode SC -ooo
alias k kick SC
alias mo mode SC
```
```