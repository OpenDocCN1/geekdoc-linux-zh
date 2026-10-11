# **EXAMPLE C.12 (CONTINUED)**

```
```
3  $cat  =  Cat->new(
          owner  =>  "Daniel",
          name  =>  "Felix",
          gender  =>  "M"
      );
4  $dog->eat("Table  scraps");
5  $dog->speak();

6  $cat->eat("Tuna  fish");
7  $cat->speak();
(Output)
4  Fido  says  thanks  for  the  Table  scraps
5  Fido  says  Woof
6  Felix  says  thanks  for  the  Tuna  fish
7  Felix  says  Meow
```
```

# **EXPLANATION**

+   1.  This script will use both the *Dog* and *Cat* classes.
+   2.  A new *Dog* object is created, with the listed attributes, and stored in the variable `$dog`. The dog's name is *Fido*.
+   3.  A new *Cat* object is created. The same attributes are provided, just with different values. The cat's name is *Felix*.
+   4.  The *Dog* object can eat because it is a *Pet*, and *Pets* can eat. The *eat* method prints a message containing the name of the animal. When we call the *eat* method on the *Dog*, the message contains "*Fido*"; and because we gave it the argument "*Table  scraps*", this also appears in the message.
+   5.  When the *Dog* speaks, the version from the *Dog* class runs. The message contains *Fido* and *Woof*, the first being from the object, and the second from the method itself.
+   6.7  When we call the same methods on the *Cat* object, the *eat* method behaves similarly because it runs the same code, the *eat* method in the *Pet* class. However, when we call *speak*, it says *Meow*, because it has run the *speak* method from the *Cat* class, and because `$cat` is a *Cat*!

# ### C.4  What About Moo?

You may have heard about Moo (2/3 Moose). This is a lightweight subset of Moose to get you up and running quickly and preferable for programs that only require the minimal features of Moose. For more on this see https://metacpan.org/pod/Moo.