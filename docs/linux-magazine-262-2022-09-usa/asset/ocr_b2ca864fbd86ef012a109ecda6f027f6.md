# Gopher browser
Gophie

Despite the fact that many people think the Internet is synonymous with the World Wide Web, the two are distinct from one another. The Internet is primarily a transport layer, responsible for connecting computers to each other. The World Wide Web is a protocol with associated software, the web server and web browser, serving content as web pages to create a vast interconnected web of, well, everything. We know you know this, but it’s sometimes good to remind yourself that there’s an Internet beyond the terrible distractions of the web. And one of the oldest is Gopher. The Gopher protocol is actually a contemporary of HTTP, created in 1990, and shares many of the same characteristics of the early web. It uses a server and

![](bbox=[0.36, 0.08, 0.48, 0.15])

client arrangement to allow access to a simple content system that could link to various online resources, including Telnet services, FTP sites, and other Gopher servers (all of which became known as Gopherspace).

Gopher’s content pages were incapable of the rich multimedia experience that HTML allowed, which held it back at the time but is now a refreshing change from the world of pop-up ads and tracking cookies. And remarkably, the world of Gopher is still available. All you need is a modern Gopher client for your Linux desktop and that’s exactly what Gophie is. Gophie is a desktop shell around the Gopher Text environment that fully supports the original specificity, including search functionality, integrated binary file

![](bbox=[0.57, 0.08, 0.98, 0.28])

> Browse the Internet like it’s 1999 with Gophie, a modern Gopher client.

downloader, Telnet sessions, and linked text documents. It’s also completely customizable. While the main window does only contain raw text of Gopher output, you can still change the colors, style, and background to suit your environment. But the best thing about it is that using Gopher is a refreshing change. There are still plenty of sites out there, and they’re typically of a higher quality than the average web page, especially without the onslaught of automated robots playing videos and sound.

Project Website
https://gophie.org

# Command line training
GameShell

Now that more people than ever are using the command line, it has become even more painfully apparent that we don’t have a good way to help people get started. The main problem is that, while many of us would consider the terminal easy to use, a beginner’s initial forays into typing commands can be terrifying. It can feel like a typo will destroy your whole environment, or worse, the environments of everyone connected to your network. This is true to a certain extent, but not when running normal, everyday commands. The solution to this fear is familiarity and experience, but then we have the classic chicken and egg problem. To gain familiarity and experience, you need to use the command line. GameShell, however, is another option.

GameShell was originally written to help university students familiarize themselves with the terminal. It does this by turning the learning experience into a text-based adventure game, much like Colossal Cave Adventure or Zork. The only difference is that instead of entering the verb and noun couplet of traditional interactive fiction, you instead construct every input from a genuine Bash command. cd will change your location. 1s will list the items in your location, and cat will show the contents of any descriptive files you find. The magic behind this is that it’s a trick. You are not really entering commands into an interpreter, but instead into your real terminal, navigating through a genuine filesystem created by the game. The exception to this is a custom

![](bbox=[0.57, 0.53, 0.98, 0.75])

> The only danger with GameShell is that it doesn’t restrict access to any commands, including rm.

gsh command which gives you goals (“Go to the top of the main tower of the castle”) and tracks your progress. It’s a really clever concept, and one that’s sure to fill any player with confidence. When the truth is revealed that you’ve actually been issuing real commands, it should give you exactly the kind of primer needed to explore further, when you take their commands into the wild.

Project Website
https://github.com/pyher/GameShell