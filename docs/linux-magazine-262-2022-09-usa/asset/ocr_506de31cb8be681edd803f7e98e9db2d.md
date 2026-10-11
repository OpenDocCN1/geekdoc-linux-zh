# IN-DEPTH

# Bash Web Scraping

such as curl [2] with the html2text [3] utility. This technique definitely works, but I found that using the Lynx browser offers a one-step solution with a slightly cleaner text output.

To install Lynx on Raspian/Debian/Ubuntu, use:

```
```
sudo apt install lynx
```
```

The Lynx -dump option will output a web page to text with HTML tags, HTML encoding, and JavaScript removed. Figure 2 shows that a Lynx dump can greatly clean up the original web page and make searching considerably easier. Sometimes a simple Bash grep search might be all that you need. However, there are many cases where some text

manipulation is required. The good news is that Bash has a nice selection of line and string manipulation tools.

The example shown in Figure 3 uses line manipulation to find the current weather in Key West, Florida. A grep search is done on the string "As of", and the option -B 3 is used to return the requested line of data with an additional three lines. You can remove the "As of" line with the tail command if required. It's important to note that what you see on a web page may not match the Lynx outputted text, and some trial and error testing might be required.

Figure 4 uses string manipulation to find the new snow at Sunshine Ski

![](bbox=[0.07, 0.23, 0.65, 0.5])

# Listing 1: Extracting Parts of a String

```
```
01  newson='\%5.8cm2.0'?
02  # Get the part before 'cm'
03  echo "${newson\%\*cm}"
04  5.2
05  # Get the part after 'cm'
06  echo "${newson#\*cm}"
07  2.0
```
```

# IT Highlights at a Glance

![](bbox=[0.0, 0.58, 0.98, 0.94])

Too busy to wade through press releases and chatty tech news sites? Let us deliver the most relevant news, technical articles, and tool tips - straight to your inbox.

+   * Linux Update
+   * ADMIN Update
+   * ADMIN HPC

Keep your finger on the pulse of the IT industry.

ADMIN and HPC: bit.ly/HPC-ADMIN-Update
Linux Update: bit.ly/Linux-Update