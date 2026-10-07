# Chapter 13: Maintaining Statistical Data for Your Site

People on the Web have been talking about “hits” for years, though most who use the term realize it's not a good indicator. At my office, the Web site receives 80,000 hits per day but only about 14,000 unique user visits per day. The design of your site influences your hit rate tremendously because of the way transfers are recorded in the access log.

The statistics programs described in this chapter are mostly free tools. They do have some sophisticated features but not enough to track a single user through a 30-minute session to see how many unique html pages are downloaded. Those transfers are spread throughout the access log. But such analysis is possible.

There are simpler ways to make accurate judgments of your Web site's popularity. For a given time period (daily, weekly, monthly):

+   * Look at the number of accesses recorded for your main page (usually the index.html file) or other important file, like your company profile.
* Look at the number of unique requesting files from your server.

So using Web statistics can be a little hit and miss (pardon the pun). The important thing is to realize the true value of statistics you get: where they are truly valid and where they are a wide guess, where they can influence your decisions and where they are just a nice boost to morale. After all, if you know your home page has 30 icons on it, it's still nice to be able to tell people you get 10,000 hits per day.

Now that I've listed the dangers and downsides of statistics, let's see what use can be made of them.

# Deciding What You Want to Know

While it's fun to install a statistics program on your Web server and start poking around the resulting graphs and lists of numbers, making any real use of Web statistics starts determining what you want to accomplish with them. The following examples may make you start thinking. Most of the questions below can be answered by the statistics programs described later in this chapter.

# WHAT IS THE SLOWEST TIME OF THE DAY AND WEEK?

This question is answered by comparing the total number of bytes sent by the Web server during each hour of the day and during each day of the week. Even if your Site is accessed by users around the world, it will probably have a clear