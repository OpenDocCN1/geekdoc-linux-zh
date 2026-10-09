# # 8 THE GHOST PROJECT

# ## 8.1 A PHP WEB SITE GENERATOR PROJECT

The ability to write short programs in C to automate tedious tasks or to do things that would otherwise take hours of fiddling about with cumbersome tools such as doing mail-merge, is one on the things you will be most pleased you have learned how to do. This project is such a time-saver. Ghost is a lightweight PHP generator for you to customise.

If you find yourself having to build PHP web sites all the time, a quick way to generate all the parameter-passing, decoding, forms building and database management code in one step would be useful. Tools like Ruby on Rails offer such functionality but are infinitely more complex to set up and run and you end up with needing to learn yet another language to go any further.

Probably the best way to start with this tool is to compile and run it. Unzip the ghost.zip source into your public_html folder which creates a folder called ghost. The Makefile contains a target g1 that compiles and links ghost. So go to **public_html/ghost** and type: **make g1**.

To run the site generator type:

+   - ./*ghost testwebsite data1 data2 data1 data3 data4 data6 data6*
+   - This will create:
+   - a folder **public_html/testwebsite**
+   - a mysql database table called **testwebsite** with textt fields data1 data2 data1 data3 data4 data6 data6
+   - a **testwebsite.css** file
+   - empty **header.html** and **footer.html** pages
+   - **index.php** that demonstrates a form handling entry, edit & update, and delete to the database table for the data items specified.