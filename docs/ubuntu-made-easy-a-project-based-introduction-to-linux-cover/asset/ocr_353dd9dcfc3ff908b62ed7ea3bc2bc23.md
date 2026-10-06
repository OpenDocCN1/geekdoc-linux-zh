3. Select the Authentication tab and click Import File. Use the window that appears to find the .key file you downloaded earlier. (It's probably in your Downloads folder.)

4. Select the .key file by clicking it once and then click OK. Check the list of trusted providers to make sure that the GetDeb Archive Automatic Signing key is now present, as is in Figure 6-11.

![](bbox=[0.266, 0.191, 0.735, 0.498])

Figure 6-11: Checking the list of trusted software providers to see whether the GetDeb key is there

5. Select the Sources window. APT will start working in the background, updating its list of packages and so. This can take a little, and APT won't tell you when it's finished, so it's probably best to do something else for a while. You can use your computer while this is going. Open the Software Center and click the arrow immediately to the right of the All Software button. If APT has finished, you should find GetDeb in the menu. If it's not there, wait a little and check again.

6. Now you can search for the program you wanted from the new repository. For instance, try searching for BookWrite, a fun little program to help you write your own novel. It should appear in the search results just like any other application, so you can install it in the usual way.

That was quite a few steps to go through, but it beats driving your local computer to buy a new program?\ One final: Remember all business about authentication and GPG keys? It relates to a security measure that checks whether the packages are from where you think they're from. (In theory, it's possible that someone could hijack a repository and put harmful packages in them.) If you don't add the GPG key, the Software Center will refuse to display any of the packages from the repository since it won't trust it. If having the GPG