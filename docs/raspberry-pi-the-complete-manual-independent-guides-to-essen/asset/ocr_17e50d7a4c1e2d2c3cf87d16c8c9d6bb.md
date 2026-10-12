# ## Program Minecraft-Pi

# ## Projects

use it as a template for all your projects.  
Write the following into the terminal to enter your folder and get started.

```
```
cd ~/minecraft
nano minecraft.py
```
```

With nano open, copy the following and then save and exit with Ctrl+X, pressing “Y” for yes, then Enter to return to the command prompt:

```
```python
from mcp import import
Minecraft from mcp_pi import block
from mcp_pi.vec3 import Vec3
mc = Minecraft.create()
mc.postToChat("Minecraft API connected")
```
```

# ### 02 Test your script

The short script you created contains everything you need to get started with hacking Minecraft-Pi in the Python language. For it to work, you need to have the game already running (and be playing). To grab control of the mouse while in-game, you can press Tab. Open a fresh terminal window, navigate into your minecraft folder and start it.

```
```
cd ~/minecraft
python minecraft.py
```
```

You’ll see a message appear on screen to let you know the API connected properly. Now we know it works, let’s get coding…

# ### 03 Hide & Seek

As you’ll see from the code on the next two pages, we’ve created a game of Hide & Seek adapted from Martin O’Hanlon’s original creation (which you can find on www.stuff4bootstrap.com). When you launch the script, you’ll be challenged to find a hidden diamond in the fastest time possible. We’ve used it to demonstrate some of the more accessible methods available in the API. Follow along with the next few steps in the guide to get an idea of how they work and how you can use them in your future projects. Hacking Minecraft is serious fun!

![](bbox=[0.12, 0.43, 0.89, 0.85])

![](bbox=[0.0, 0.85, 0.99, 1.0])