# **Problem Statement**

It is always a good practice to state the problem before a solution is presented. So, here is the problem that you are going to solve in this chapter.

You have a small company office of full- or part-time day traders. Your office is small, cheap, or both, so obtaining quotes without fees is important. Additionally, you are concerned about network traffic between your host and your Internet provider because you need the available bandwidth for other purposes. Meanwhile, your office staff insists on obtaining the best free quote service possible.

# **Solving the Quote Service Problem**

It is clear from the problem statement that it is desirable to get one set of quotes from the quote provider. There is no point in having all your office workers using separate TCP/IP connections to the same quote server, for the same information. This would use up valuable bandwidth to your Internet service provider. From the free quotation provider’s point of view, this is also less than desirable.

One local server program could continually fetch updated stock market quotes for everyone. This information could then be broadcast to the local network for all interested parties. This is the solution that you will apply in this chapter. This application will also give you the chance to review the use of both stream sockets and datagram sockets.

# **Obtaining Stock Market Quotes**

The data source that you’ll use for market quotations will be the fine service at `finance.yahoo.com`. In this section, you’ll learn how the program manages to fetch the quotation information from `finance.yahoo.com`.

# **NOTE**

> The programs being presented in this chapter worked at the time of writing. It is possible, however, that the Internet service being used might have changed by the time you read this. Notes are provided later in this chapter to help you adjust these programs should this become necessary.

To determine how to obtain stock quotes, you can use your Web browser to visit `http://finance.yahoo.com` (Netscape will be assumed here). There, you will be presented with a page that lets you enter a ticker symbol and press the Get Quotes button. Entering `RHAT` and pressing the button leads you to another page giving you the details about Red Hat Inc. Underneath the quote information, you will find a link that reads Download Spreadsheet Format. This is the gold mine!