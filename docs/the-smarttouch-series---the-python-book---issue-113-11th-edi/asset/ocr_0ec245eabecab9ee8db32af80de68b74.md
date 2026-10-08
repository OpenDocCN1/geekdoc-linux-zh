```
```python
["title"]
links = SkyNews["entries"][1]
["link"]
    print(text)
print(links
```
```

# 11  Append the data to the lists

In **Step 4** we created two lists named **News** and **Links**. In this step we add the news headlines that are stored in the variable from the previous step, named **text**, to the **News** list, line one. This uses the **append** function which adds each headline to the end of the list. Next, do the same for the hyperlinks, appending them to the **Links** list that we created in **Step 4**.

+   * `News.append(text)` #add headlines to News list
* `Links.append(links)` #add links to Links list

# 12  Create a dictionary of news and links

Now that we have a list of headlines and a list of hyperlinks, we can combine them into a dictionary. This works in the same way as any dictionary: you look up the word and it gives you a definition. In this program, however, the keyword is the headline and the definition is the hyperlink. Create a new dictionary named **News_Dict**, line one. Then for each entry in the **News** list, add it to the dictionary, assigning the hyperlink to the **News** headline, line three. The last line of code can be omitted, but it’s useful for testing the code.

```
```python
News_Dict = {}
for i in range(len(News)):
    News_Dict [News[i]] = Links[i]
print (News_Dict)
```
```

# 13  Create the presentation, part 1

The last section of the program creates the presentation. First assign the **Presentation()** class to the variable **prs**. Next create a **for** loop, which for each of the entries in the dictionary creates a new slide using the function from **Step 5**. This places the headline into the title placeholder on the slide, then places the hyperlink into the subtitle placeholder. As hyperlink addresses are not always user friendly and could be any length, we should assign the hyperlink to the text label **Click for full story**, which we do in line three.

![](bbox=[0.36, 0.1, 0.85, 0.39])

address the text label **Click for full story**, which we do in line three.

```
```python
prs = Presentation()
for key, value in News_Dict.items():
    this_slide = create_my_default_slide("%s" % key, "Click for full story: ")
add_hyper_link(this_slide.shapes[1], value, value)
print(len(prs.slides))
```
```

# 14  Create the presentation, part 2

For the next step, we need to write the hyperlinks to each slide. In **Step 8** and **9**, the function converts the text string into an operational hyperlink. Line one uses the **add** method to write each unique hyperlink to the text label on each slide. The label is selected using the code **this_slide.shapes[1]**, where **[1]** refers to the second textbox on the slide. The final line of code is actually optional, and prints out the total number of slides in the presentation. This is useful for checking that the program is working accurately – ten news stories should always create ten slides.

# 15  Create the presentation, part 3

The final line of the program, **prs.save()**, builds and saves the presentation. The presentation file is saved to the same folder where the Python program is stored and executed from. You can alter the file location and the name of the file if you need to do so.

```
```python
prs.save('Whats_News.pptx')
```
```

# 16  Run the program

Save your code and then run it by pressing **F5**. The program will connect to the news website and download stories. You can adjust the number that you require by editing the value in **step 10**.

The program then bundles the slides together and exports them as a file with the **.pptx** extension (Microsoft PowerPoint’s default format). You can view the presentation directly on the Raspberry Pi using Libre Office, or transfer the file to another device and use most standard presentation software to open it. Feel free, of course, to improve the program further – perhaps by adding some error-checking code in case the downloading of data fails for some reason.

# Make the What's News? app

Why not create an automated news machine, and add email functionality and a button to trigger up-to-the-minute news feeds? Simply press the big red button and the program runs, pulls down the news, creates the presentation and then emails it to a preselected account. It’s great for educational environments, see http://www.tecoco.co.uk/whats-news-app.html.

![](bbox=[0.8, 0.79, 0.88, 0.88])

Tutorial files available: fileisilo.co.uk