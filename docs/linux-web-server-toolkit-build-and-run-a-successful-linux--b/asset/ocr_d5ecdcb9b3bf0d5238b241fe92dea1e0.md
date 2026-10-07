# Chapter 12: FastTrack Configuration and Administration

# 325

and then send a response back, you should also check the CGI checkbox next to the filename that you configure for that error.

# Configuring Access Control

One of the most useful features of a Web server is its ability to control access to documents with a distinct username and password. You can require that a valid username and password be entered before any document is transferred to a browser. Although this is not a totally secure system, because the username and password cross the Internet as plaintext, it provides a very useful feature for many occasions when "unbreakable" security is not needed.

An example of using access control on a Web server would be a company producing materials for a client. The company can place samples or drafts on their Web site in an area set aside for the client. Only the client can access that part of the Web server because only the client is given the username and password that protects it.

![](bbox=[0.037, 0.483, 0.138, 0.558])

> The access control described in this section is a per-file or per-directory access control that is administered by the Web server (almost all Web servers offer this feature). It is completely different from other security features such as secure connections using SSL or HTTP.

Unfortunately, access control is sometimes one of the least used features of a Web server, simply because it seems hard to set up and manage. FastTrack takes the questions out of access control and makes it easy to use.

# Users and Groups

The first thing to know about access control is that it's based on users and groups. On Linux, you have a small database of users (actually a file with one line for each user, containing relevant facts) and a small database of groups (actually another file listing a group name and which users belong to the group).

Access control for your Web server is managed by a similar list of users and groups. You use the Access Control of the FastTrack Server to manage the lists of users and groups, and to specify which files they have access to.

Of course, if you don't use access control features, access to specific files and directories on your Web server is not controlled on a per-user basis at all. Instead, access is granted based on the rules for which host a user is accessing the data, and from similar security rules that don't require that someone know a valid username and password.