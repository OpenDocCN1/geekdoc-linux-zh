
这段代码设置了 `FDragging` 和 `FDrawOnce` 变量。此操作的最终结果是由于用户再次开始拖动鼠标之前，`MouseMove` 调用将不会执行程序的任何代码。此时，`FDrawOnce` 变量的值确保了在第一次通过时只绘制一个矩形。

# 11

# NOTE

Some readers might notice that I do not erase the rectangle drawn on the user's last pass through the `MouseMove` method before lifting the mouse button. It is not necessary to make this erasure because the entire surface of the component is about to be redrawn in order to show the new area of focus.

After all this hand-waving is completed, the program then goes on to the serious business of actually drawing the details of the newly defined area of the Mandelbrot set. In short, it iterates once again over dear Mr. Mandelbrot's oft-traversed equation, but by this time feeds it a different set of values.

# TBitmap: Taking a Picture of the Mandelbrot Set

One of the most interesting aspects of the `TestElMandel` program is its capacity to capture the contents of the completed Mandelbrot pictures and then save them to a file. It turns out that Kylix makes this process extremely simple:

```pascal
procedure TForm1.SnapPicture;
begin
FBitmap.Width := ElMandy1.Width;
Bitmap.Height := ElMandy1.Height;
FBitRect := Rect(0, 0, ElMandy1.Width, ElMandy1.Height);
FBitmap.Canvas.CopyRect(FBitRect, ElMandy1.Canvas, FBitRect);
end;
```

`FBitmap` is a variable of type `TBitmap`. The code to create an instance of this variable is straightforward:

```pascal
FBitmap := TBitmap.Create;
```

The Kylix `TBitmap` component has its own built-in `TCanvas` object. To begin using this object, you can set the width and height of the bitmap that you want to create:

```pascal
FBitmap.Width := ElMandy1.Width;
Bitmap.Height := ElMandy1.Height;
```

# CLX

## 第二部分

After you have done this, you have a fully functional bitmap object at your disposal. In other words, using these properties does more than merely the width and height of the component; you are actually creating an empty bitmap of this width and height. You could, instance, drawing on the bitmap's canvas in order to create pictures of your own design:

```pascal
FBitmap.Canvas.Ellipse(10, 10, 25, 25);
```

However, this is not the course of action that your program wants to pursue. Instead, the `TestElMandel` program simply copies the current contents of the `TElMandy` component to the bitmap:

```pascal
FBitmap.Canvas.CopyRect(FBitRect, ElMandy1.Canvas, FBitRect);
```
