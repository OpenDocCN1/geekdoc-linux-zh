
# Configuring a Usenet News Service

## In this chapter

- Understanding Usenet 338
- Configuring a Local News Server 338
- Reading News 342
- Troubleshooting 343

## Understanding Usenet

The Internet was created as a medium of exchange. Computers use it to connect to each other and exchange data and information. The transfer of information across the Internet takes different forms. Information can be exchanged via the HTTP protocol to your browser, via email messages, and so on. One of the earliest forms of communication over the Internet was news.

News is a form of communication in which people can post and read articles and messages in one common place. A special program, called a *news client*, is used to connect to that common place—known as a *news server*—and browse all the articles and messages on it. Articles and messages are sorted into categories, which span almost all aspects of discussion. These categories include programming, cooking, guitar playing, music, books, art, and others that are too numerous to mention.

*Newsgroups*, formally known as *Usenet*, are one of the most efficient forms of communication on the Internet. Many projects have been designed and built by groups of people who communicated using newsgroups. Linux itself was built this way, as was most of the software that runs on it.

To read news, you must have a news client and access to a news server. Access to a news server is obtained from your ISP. You can set up your own local news server for offline reading. A local news server can automatically fetch all the articles on the news groups in which you are interested and store them locally on your hard drive. You then can browse them at your own convenience instead of staying online to read them.

Configuring a local news server for offline browsing is not difficult with SuSE Linux. This server can be used as a small news server for a small network, as well.

## Configuring a Local News Server

To set up your machine as a small news server for offline browsing, you must install the news server, which is called `leafnode`. Please note that you will need a large amount of empty hard disk space to run a news server because hundreds of articles will be stored on your hard drive. The amount of space you need depends on how many newsgroups you will be reading.

### Installing `leafnode`

The package requirements for `leafnode` are as follows.

**Package requirements:**

- Series n:
  - leafnode

After you have installed the required package, you will use YaST to set up the first part of the news server. Just follow these steps:

1. Log in as root.
2. Run YaST.
3. Navigate to System Administration, Change Configuration File and press Enter.
4. A dialog pops up in which you can set up all the system variables required to enable/disable the system's services.
5. Press F4 to search for the variable you want to change. A small dialog pops up; type `NNTP SERVER` and press Enter.
6. YaST will locate the correct system variable for you, which is `NNTP SERVER`. Press Enter to change its value—you should enter localhost if you have a standalone machine. If you are in a networked environment, you must enter your real hostname here. Your setup should look similar to Figure 17.1.

FIGURE 17.1  
Setting up the news server with YaST.

![](img/659f91d9da7b29976c0625e2e9628511_364_0.png)

7. Press F10 to exit and save.
8. Exit YaST.

Next, you should configure `leafnode`.

### Configuring `leafnode`

You now need to set up `leafnode` itself. `leafnode` uses a text configuration file, `/etc/leafnode/config`. Open the file using your favorite editor. You will need to configure some common parameters for `leafnode`.

The first parameter is the most important one—the server parameter. This is the news server from which `leafnode` will read the news. If you connect to the Internet via a dial-up connection, you should ask your ISP about their news server. If you are on a local network, check with your administrator about a news server that you can use.

另一个参数 `expire` 告诉 `leafnode` 在删除未读讨论线程前应等待的天数。该参数的默认值为 20 天。此参数必须存在。

某些新闻服务器要求您使用用户名和密码登录。如果您的新闻服务器需要此操作，您可以使用 `username` 和 `password` 参数像这样指定用户名和密码：

## Troubleshooting

*I cannot log in to the NetWare version 4.x server as was described in this chapter. The `ncp_mount` command always fails. What's wrong?*

Try passing the `-b` argument to the `ncp_mount` command.
