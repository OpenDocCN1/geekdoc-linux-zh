# Questions

+   1. Given the following:
public enum Wallpaper {
BROWN, BLUE, YELLOW;
}

+   Which of the following are legal?
A. enum PatternedWallpaper extends Wallpaper {
STRIPES, DOTS, PLAIN;
B. Wallpaper wp = Wallpaper.BLUE;
C. Wallpaper wp = 
ew Wallpaper(Wallpaper.BLUE);
D. void aMethod(Wallpaper wp) {
System.out.println(wp);
E. int hcode = Wallpaper.BLUE.hashCode();

+   2. Given the following:
package pack;

```
class Sploo {
public int a;
public static int b;
int c;
static int d;
```

```
public void eee() {}
public static void fff() {}
}
```

Which of the following features of Sploo may be accessed by a class, in package pack, as a result of the following import?

```
import static pack.Sploo;
```

+   A. a
B. b
C. c
D. d
E. eee()
F. fff()