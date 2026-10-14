![](bbox=[0.213, 0.069, 0.603, 0.164])

# # Project 11: Setting Up Asian-Language Support

So, what do you do if, for example, you want to be able to type Chinese, Japanese, Korean, Hindi, Thai, or Nepali while still in your usual English environment? What if you want to be able to type all of those languages in the same document? Can you do it?

You bet.

There are actually several ways of going about this, but the default method in Ubuntu is the easy-to-use Intelligent Input Bus (IBus). IBus supports most Asian languages, including Chinese, Japanese, and Korean, and it provides a number of input methods for many of these.

# ## 11-1: Selecting Input Method Modules

The first thing you will need to do to use IBUs is select the appropriate input modules for the language(s) you want to input. To do this, go to the **System** menu, and select **Preferences ▸ IBus Preferences**. A window will then appear asking you whether you would like to start the IBus daemon. Click **Yes**, after which yet another window may appear telling you what to do if you cannot get IBus to work. Click **OK** in that window. (Fortunately, these two windows will appear only when you first start IBus.) The IBus Preferences window will then appear. Click the **Input Method** tab.

> **NOTE**  A daemon is a program that runs in the background, unbeknownst to the average user, providing a system with added functionality. In the case of IBUs, that added functionality is the ability to input complex character sets.

On that tab, click the **Select an input method** drop-down button, select the input method you require, and then click **Add**. The input method you just added will then appear in the main pane of the window beneath the default method, English. Repeat the process for any other input methods you want to add. When done, your window should look like a variation on what you see in Figure 11-10, depending on which languages you actually select. When you’re done making your selection, click the **Close** button.