# Desktop effects

# Emerald theme manager

Access dozens of separate themes using Emerald.

If you think that Compiz is overburdened with possibility, with a wealth of options that make it hard to get your desktop you want, then Emerald is the answer. It is a simple interface to changing the appearance of your desktop. There’s no talk of plugins and categories in Emerald – just click on the preview you like, and the display changes accordingly. Themes have been created to ape many popular desktops, but they’re easy enough to edit and create your own. All of this is achieved through the manager. There’s a little hoop jumping to get everything installed, and you need to type a single line on the command line to be able to install the most useful themes, but it’s definitely worth the effort.

The options that load below the Frame Engine menu are particular to each engine, but most themes will let you change the colour of the theme as well as the gradients used to fill in the window border. As you move each slider, the effects can be seen on your desktop in real time, so you can quickly tell whether you like the modification or not. Switch to the ‘Frame/Shadow’ tab in the Edit Themes window and you can change some of the more general options attached to a theme. The most obvious effect is a subtle distance. But changing the opacity, as well as the radius of the shadow, can make it more obvious in quite a pleasing way. You can also alter the X and Y axes to change the direction in which the shadow falls relative to the window.

![](bbox=[0.623, 0.192, 0.896, 0.348])

> The combination of Compiz and Emerald gives Linux an unbeatable desktop.

# Create your own

After installing the themes (see our walkthrough), you’ll find a preview for each listed in the ‘Themes’ tab when you first launch the Emerald Theme Manager from the ‘System > Preferences’ menu. Clicking on any of them will apply the theme to the windows on your desktop. Compiz is being used in the background to add transparency, reflections, blur effects, refraction and the shadows. These effects are handled by something called a frame engine, and you can see which one each theme is using by switching to the ‘Edit Themes’ tab. Just switching between frame engines can alter the appearance of your desktop. The ‘truglass’ engine, for instance, gives the impression of a reflective see-through desktop, while ‘Oxygen’ is what you should choose if you want a theme that looks a little like Microsoft’s Aero theme.

# Save your theme

Most importantly, you need to remember to save your changes. You can do this from any of the Edit Themes pages by typing a name into the bottom field and clicking the ‘Save’ button. This will add your new theme with your own modifications to the Themes list on the first page, and change the theme description. This is accomplished from the ‘Theme’ page, from where you can add yourself as the author, as well as give your theme a name and a version number. You can also attach a screenshot of your theme that’s used to preview its appearance in the Themes page.

# Step by step: Install Emerald

![](bbox=[0.11, 0.688, 0.35, 0.83])

1 Emerald, like everything else in Ubuntu, is installed through the Synaptic package manager. You need to look for and install the following packages: emerald, gnome-compiz-manager and subversion. The last one is a developer’s tool we’re going to use to download themes. You also need to make sure the Compiz ‘Windows Decorations’ plugin is enabled.

![](bbox=[0.37, 0.688, 0.61, 0.83])

2 You will now see a new addition to the System > Preferences menu. Click on Emerald to launch the application. By default there are no themes, and before we can get them, we need to add the repositories security certificate. Open a Terminal and type the command at the bottom of the Theme Settings > Repositories page. Press P to add the certificate permanently.

![](bbox=[0.63, 0.688, 0.87, 0.83])

3 With the connection to the theme repository authenticated, we can now download some themes. From the Repositories page, click on both the ‘Fetch’ buttons to download the latest themes into the manager. When this has completed, you will find them listed in the ‘Themes’ tab, and you can enable them with a double click. After which, you should have a shiny new desktop theme!