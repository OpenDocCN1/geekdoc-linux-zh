
personal computer. Use the -r flag in order to copy directories.

- `curl` allows you to send HTTP requests to other servers. Use the `-o` flag to download files with `curl`.
- `ps -A` lists all of the programs running in the background of your computer.
- `cron` allows you to schedule when programs are run. Use `crontab -e` in order to edit the cron table.

## Exercises

1. Write a bash script that takes a file path as an argument and copies that file to a designated folder on your server.
2. Find a file online that changes periodically, then write a program to download that file every time it changes.
3. Try creating your own Twitter or GitHub bot with the Twitter API⁴³ or the GitHub API⁴⁴.

## Shutting Down a Server

In order to avoid using more DigitalOcean credits than we have to, or being charged for using the service, make sure to **destroy** any DigitalOcean droplets that you started. When you destroy a droplet, all files on the droplet are gone forever, so please be sure that you don't have any important information on a droplet before you destroy it. If there are files you want to save on your droplet, use `scp` in order to copy them to your local machine.

Let’s walk through destroying a droplet. Go back to DigitalOcean⁴⁵ and log in. You should then see a listing of all of your droplets:

![](img/a67f2d2ba01c2569ec78ab34ae6c3c5a_241_0.png)

Click on More on the right side of the screen and a menu should appear. Click Destroy at the bottom of this menu. Then this screen should appear:

Click the **Destroy** button and then click **Confirm** in the menu that pops up. Your droplet should now be destroyed. If you have no active droplets, then the main droplets page should look like this:

![](img/a67f2d2ba01c2569ec78ab34ae6c3c5a_242_0.png)

## Start Building

### Next Steps

We’ve reached the end of this book, which means that you now have a formidable foundation in using Unix. Congratulations! As the title of this book suggests, Unix serves mostly as a workbench—a set of tools for building amazing digital creations. However, what you can create with Unix is usually not made out of Unix’s constituent parts. You might use a hammer and saw to build a good birdhouse, but the birdhouse itself isn’t made out of hammers. Working knowledge of Unix is best complemented by knowing at least one other programming language. Here are a few suggestions about how you can continue your computing and programming education.

Python⁴⁶ is an approachable and essential language for anyone interested in computing. If you don’t have any programming experience outside of this book, I very highly recommend learning Python. My favorite book on the subject is Learn Python the Hard Way⁴⁷ by Zed Shaw. Philip Guo’s Python Tutor⁴⁸ allows you to visualize how Python is working under-the-hood, which allows you to develop a better intuition about the code you’re writing. The pairing of those two resources is currently the best way to learn how to write software outside of formal university or corporate training. Once you have some Python experience, you can try building your own HTTP API with Flask⁴⁹.

R⁵⁰ is a general purpose programming language designed for folks who are interested in data science, analysis, modeling, and visualization. R is also fantastic for making digital documents: this book was created with R! If you want to get started with R, I recommend the book R Programming for Data Science⁵¹, the Swirl⁵² software package, and the interactive R tutorial website called DataCamp⁵³.

JavaScript⁵⁴ is the main language that powers the internet and it forms the backbone of web application programming. The Mozilla Developer Network has wonderful tutorials⁵⁵ about HTML, CSS, and JavaScript. Usually you use JavaScript to manipulate HTML and CSS, so learning about all three is important! I also recommend NodeSchool⁵⁶ for purely learning about JavaScript with Unix.

### Giving Feedback

Thank you so much for reading this book! If you’d like to discuss the book or you have any feedback, I would love to hear from you. The best way to contact me is on Twitter⁵⁷.
