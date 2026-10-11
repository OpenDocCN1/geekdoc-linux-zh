```
```
af_1px.c:            SOCK_DEBUG(sk,
af_1px.c:                "SOCK_DEBUG: %s: %s: bind failed because port %X in use.\n",
af_1px.c:                SOCK_DEBUG(sk, "IPX: bound socket 0x%04X.\n");
af_1px.c:            if(sock->type == SOCK_DGRAM )
af_1px.c:                case SOCK_SEGPACKET:
af_1px.c:            if(sock->type != SOCK_SEGPACKET)
af_1px.c:            if(sock->type != SOCK_SEGPACKET)
af_1px.c: /* route socket(PF_IPX,SOCK_SEGPACKET) calls through spx_create() */
$   ```
```

From the grep output shown in Listing 4.2, you can immediately see that socket types SOCK_DGRAM and SOCK_STREAM are probably supported (to be certain, you need to examine the logic of the code, however). Toward the end, there also appears to be a reference to SOCK_SEGPACKET, suggesting that it, too, might be supported.

The other item of interest is that you know that you probably want to peruse the file af_1px.c for notes and comments. Sometimes, the comments can be useful to find out what is supported and what is not.

# ## What's Next

In this chapter, you have taken a careful look at the socket(2) function call. The extra level of theory and detail in this chapter was necessary for you to cover because much hinges upon the choices you make in the socket(2) call. With this working knowledge of the socket(2) function, you are well on your way to putting sockets to work.

The next chapter will turn your attention primarily to the bind(2) function call. This function is important because it enables you to assign addresses to the sockets that you have learned how to create in this chapter.