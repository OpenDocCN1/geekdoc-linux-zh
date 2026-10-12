# QStyleSheet QStyleSheet provides a basic collection of styles for use by the Qt simple rich-text rendering mechanisms.

# A Possible Instantiation

```
```cpp
QStyleSheet *ns = QStyleSheet::defaultSheet();
```
```

By adding QStyleSheetItems to a style sheet, you are adding new tag support to that style sheet.

# OUTPUT WIDGETS

The following widgets are used only for output or display purposes.

# QFrame A frame is a graphic border around a widget, or it can appear as a vertical or horizontal line. QFrame is the base class for widgets that either have a frame or have an optional frame such as QLabel.

![](bbox=[0.18, 0.585, 0.64, 0.715])

Figure 3.32 Various QFrame widgets

# A Possible Instantiation

```
```cpp
QFrame *f = new QFrame( this );
```
```

# Example Use

```
```cpp
QFrame *f = new QFrame( this );
    f->setFrameStyle( QFrame::HLine | QFrame::Sunken );
    f->setLineWidth( 2 );
```
```

If you are from a Motif background, you'll probably assume that pushbuttons inherit QFrame somewhere—but they don't.