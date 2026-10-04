# Introduction

With all the security hype you there focusing on Internet Information Server (IIS) worms, Trojan e-mail attachments, cross-site scripting, and Web site deface-ments, it might never occur to the average person that most corporate jewels do not lie on Web servers or desktops. Customer data, credit cards, passwords, and corporate secrets usually exist safely within the warm confines of your database systems—not the ephemeral systems that appear to be constantly under attack. But, just how is your database system anyway? Is it possible that someone defacing your Web site might be one hop away from the corporate jackpot? You betcha.

In this chapter, we discuss the security of one of the most popular database products for Web-based development: Microsoft’s SQL Server 2000. We begin by briefly examining the history of SQL Server and investigating the different editions that are available. Next, we delve into an overview of the entire SQL server architecture and how the pieces work together.

After covering the background, we investigate how attackers identify, penetrate, and escalate privileges in a SQL Server environment. We identify all of the tools and techniques that potential attackers may use in order to turn your servers into theirs. Next, we turn the tables on the attacker and look at what you can do to defend yourself against the same techniques. Again, we look at defensive weapons and how to leverage them against your adversaries now and in the future.

Finally, we analyze how good SQL Server security can be undermined by poor application development. SQL injection techniques and SQL Server’s own special weaknesses are discussed in detail. However, these weaknesses can be addressed, so we wrap the chapter with discussions of how to make sure your applications don’t inadvertently destroy all you have tried to accomplish.

# The Evolution of SQL Server

Before we dive into SQL Server’s security mechanisms, it is important to understand where SQL Server came from and how it evolved. This is vital for a variety of reasons—one being that it will shed some light as how the SQL Server security model evolved, and also, why its evolution did not fully free it from the mistakes of the past. Second, it helps to understand how SQL Server evolved into a multiple set of editions and what the security implications are for each incarnation.