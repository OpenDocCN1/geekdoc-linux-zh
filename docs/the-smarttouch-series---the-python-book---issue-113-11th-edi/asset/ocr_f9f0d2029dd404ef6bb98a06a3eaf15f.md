![](bbox=[0.1, 0.13, 0.33, 0.22])

```
```

### Unix_News.py – FriFreeware WordLiNux Tutorials| Linux News|Linux_News.py *(6:0)

File Edit Format Run Options Window Help

`````` What's News App #####

### http://python-ptkx.readthedocs.io/en/latest/user/quickstart.html

# sudo pip3 install feedparser

# http://python-ptkx.readthedocs.io/en/latest/user/install.html

import feedparser

from pptx import Presentation

from pptx.util import Inches, Pt

from pptx.dml.color import RGBColor



### lists to hold headline and link ###

News = []

links = []

`````` Create News Feed, pull down latest News ####

#BBCNews = feedparser.parse("http://feeds.bbci.co.uk/news/rss.xml?edition=uk")

SKYnews = feedparser.parse("http://feeds.skynews.com/feeds/rss/uk.xml")
```
```

# 01 Install feedparser

The program uses a Python library called feedparser. The process of parsing basically means taking input from a string and then returning some data. feedparser applies this process to web feeds such as RSS. Atom and RDF. In our program, feedparser is used to collect input from news websites, which is then downloaded and used to pull out data, such as the headline and a hyperlink to the website where the news story is stored. Open the LXterminal window and type `sudo pip3 install feedparser`. This will download the required Python library.

```
```
from pptx import Presentation
from pptx.util import Inches, Pt
from pptx.dml.color import RGBColor
```
```

```
```
def create_my_default_slide(title, subtitle):
    title_slide_layout = prs.slide_layouts[0]
    slide = prs.slides.add_slide(title_slide_layout)
```
```

![](bbox=[0.1, 0.44, 0.33, 0.57])

# 02 Install Python-ptkx

Python-ptkx is a program for creating customised presentations via Python code. Data from webpages, Twitter, databases and so on can be automatically captured and written to slides. The Python-ptkx library can be used to customise the slide layout, colour, font and style. Return to the LXterminal window and enter the command `sudo pip3 install python-ptkx` to download the required library.

# 04 Create the lists

Now create two lists to hold the data which feedparser collects from the news websites. Lists are a useful feature of programming languages and work much like shopping lists. You can add items to them, delete, edit and even merge lists. Next, create a variable and use feedparser to collect the news headlines. The code below includes two different news websites. You can try either of them. These are used in **Step 10** to access the news data.

# 06 Create the slide layout, part 2

To complete this function we state where the parsed information needs to be placed. On line one, add the pptx code to assign the news headline from the **title** variable to an individual slide. The command `shapes` enables you to select the empty title textbox on the slide and write the news headline into it. Line two does the same except that it assigns the weblink to the second placeholder on the slide, the **subtitle** textbox.

# 03 Import the required modules

Open your Python3 editor and start a new file. Begin by importing **feedparser**, line one, which is used to download the data from the news websites. The next three lines enable the program to create the presentation. Import **presentation** from the Python-ptkx library, line two, and then the ptx utilities, line three, which enable you to customise the point size of the font. This is useful for setting your own sizes for the news headline and the hyperlink. Last, import the colour modules, line four, so that you can change the colour of your fonts.

```
```
News = []
links = []

#BBCNews = feedparser.parse("http://feeds.bbci.co.uk/news/rss.xml?edition=uk")
SKYnews = feedparser.parse("http://feeds.skynews.com/feeds/rss/uk.xml")
```
```

```
```
slide.shapes.title.text = title
slide.placeholders[1].text = subtitle
return slide
```
```

# 05 Create the slide layout, part 1

In order to make the presentation we need to create a function which customises and builds the slides. Begin by defining the name of the function and then adding the parameters **title** and **subtitle**. When the program runs, these will be replaced with the news headline and a hyperlink to the webpage. On line two set the slide layout to **0** – this is the standard default presentation slide layout, with a title and subtitle textbox. Next create a variable which holds the slide information comprising its layout, the title and the subtitle.

# 07 Create the hyperlink, part 1

Next we need to write a function to create and edit the hyperlinks. Each hyperlink needs to display a link to the web page and, when clicked on, should take the user to the specific news story on the website.

Begin the process by naming the function, line one, and add the following arguments. **shape** is used to select which box on the slide the hyperlink is written to, and **text** adds the string to the textbox. The last argument is `url`, which adds and enables a hyperlink address.
On line two, assign `shape.ptx_frame` to a variable named `p`. These properties enable you to manipulate the text within the frame.

```
```import feedparser```
```