

```c
g_n_o_m_e _ i n i t ( " s h o w g c ", " 1 . 0 ", a r g c , a r g v ) ;
 a p p = g n o m e _ a p p _ n e w ( " f l a s h e r ", " L i s t i n g G C ") ;
 g t k _ s i g n a l _ c o n n e c t ( G T K _ O B J E C T ( a p p ) , " d e l e t e _ e v e n t ",
         G T K _ S I G N A L _ F U N C ( e v e n t D e l e t e ) , N U L L ) ;
 g t k _ s i g n a l _ c o n n e c t ( G T K _ O B J E C T ( a p p ) , " d e s t r o y ",
         G T K _ S I G N A L _ F U N C ( e v e n t D e s t r o y ) , N U L L ) ;

 a r e a = g t k _ d r a w i n g _ a r e a _ n e w ( ) ;
 g t k _ w i d g e t _ s e t _ u s i z e ( a r e a , W I D T H , H E I G H T ) ;
 g n o m e _ a p p _ s e t _ c o n t e n t s ( G N O M E _ A P P ( a p p ) , a r e a ) ;
 g t k _ s i g n a l _ c o n n e c t ( G T K _ O B J E C T ( a p p ) , " r e a l i z e ",
         G T K _ S I G N A L _ F U N C ( l i s t V a l u e s ) , a r e a ) ;
 g t k _ w i d g e t _ s h o w _ a l l ( a p p ) ;
 g t k _ m a i n ( ) ;
 e x i t ( 0 ) ;
 } 

 i n t l i s t V a l u e s ( g p o i n t e r d a t a )
 { 
 G t k W i d g e t * w i d g e t = G T K _ W I D G E T ( d a t a ) ;
 G d k G C * g c ;
 G d k G C V a l u e s g c v ;

 g c = w i d g e t - > s t y l e - > w h i t e _ g c ;
 g d k _ g c _ g e t _ v a l u e s ( g c , & g c v ) ;

 p r i n t f ( " f o r e g r o u n d R G B : % u % u % u ( 0 x % 0 8 X ) \ n ",
         g c v . f o r e g r o u n d . r e d , g c v . f o r e g r o u n d . g r e e n ,
         g c v . f o r e g r o u n d . b l u e , ( g u i n t ) g c v . f o r e g r o u n d . p i x e l ) ;
 p r i n t f ( " b a c k g r o u n d R G B : % u % u % u ( 0 x % 0 8 X ) \ n ",
         g c v . b a c k g r o u n d . r e d , g c v . b a c k g r o u n d . g r e e n ,
         g c v . b a c k g r o u n d . b l u e , ( g u i n t ) g c v . b a c k g r o u n d . p i x e l ) ;
 p r i n t f ( " f o n t i d : % d a s c e n t : % d d e s c e n t : % d \ n ",
         g c d _ f o n t _ i d ( g c v . f o n t ) ,
         g c v . f o n t - > a s c e n t , g c v . f o n t - > d e s c e n t ) ;
 p r i n t f ( " p i x e l d r a w i n g f u n c t i o n : % s \ n ",
         f u n c t i o n S t r i n g ( g c v . f u n c t i o n ) ) ;
 p r i n t f ( " f i l l m e t h o d : % s \ n ", f i l l S t r i n g ( g c v . f i l l ) ) ;
 p r i n t f ( " s u b w i n d o w m o d e : % s \ n ",
         s u b w i n d o w S t r i n g ( g c v . s u b w i n d o w _ m o d e ) ) ;
 p r i n t f ( " t i l i n g / s t i p p l i n g o r i g i n : ( % d , % d ) \ n ",
         g c v . t s _ x _ o r i g i n , g c v . t s _ y _ o r i g i n ) ;
 p r i n t f ( " c l i p p i n g o r i g i n : ( % d , % d ) \ n ",
         g c v . c l i p _ x _ o r i g i n , g c v . c l i p _ y _ o r i g i n ) ;
 p r i n t f ( " g r a p h i c e x p o s u r e s : % d \ n ",
         g c v . g r a p h i c s _ e x p o s u r e s ) ;
 p r i n t f ( " l i n e w i d t h : % d \ n ", g c v . l i n e _ w i d t h ) ;
 p r i n t f ( " l i n e s t y l e : % s \n ",
         l i n e S t y l e S t r i n g ( g c v . l i n e _ s t y l e ) ) ;
 p r i n t f ( " c a p s t y l e : % s \n ",
         c a p S t y l e S t r i n g ( g c v . l i n e _ s t y l e ) ) ;
 p r i n t f ( " j o i n s t y l e : % s \n ",
         j o i n S t y l e S t r i n g ( g c v . l i n e _ s t y l e ) ) ;
 }
 return(TRUE);
 }
 static char *functionString(GdkFunction function)
 {
 switch(function) {
 case GDK_COPY: return("copy");
 case GDK_INVERT: return("invert");
 case GDK_XOR: return("and invert");
 case GDK_CLEAR: return("clear");
 case GDK_AND: return("and");
 case GDK_AND_REVERSE: return("and reverse");
 case GDK_AND_INVERT: return("and invert");
 case GDK_NOOP: return("noop");
 case GDK_OR: return("or");
 case GDK_EQUIV: return("equiv");
 case GDK_OR_REVERSE: return("or reverse");
 case GDK_COPY_INVERT: return("copy invert");
 case GDK_OR_INVERT: return("or invert");
 case GDK_NAND: return("nand");
 case GDK_SET: return("set");
 default: return("");
 }
 }
 static char *fillString(GdkFill fill)
 {
 switch(fill) {
 case GDK_SOLID: return("solid");
 case GDK_TILED: return("tiled");
 case GDK_STIPPLED: return("stippled");
 case GDK_OPAQUE_STIPPLED: return("opaque stippled");
 default: return("");
 }
 }
 static char *subwindowString(GdkSubWindowMode mode)
 {
 if(mode == GDK_CLIP_BY_CHILDREN)
 return("clip by children");
 else if(mode == GDK_INCLUDE_INFERIORS)
 return("include inferiors");
 return("");
 }
 static char *lineStyleString(gint style)
 {
 switch(style) {
 case GDK_LINE_SOLID: return("solid");
 case GDK_LINE_ON_OFF_DASH: return("on off dash");
 case GDK_LINE_DOUBLE_DASH: return("double dash");
 default: return("");
 }
 }
 static char *capStyleString(gint style)
 {
 switch(style) {
 case GDK_CAP_NOT_LAST: return("not last");
 case GDK_CAP_BUTT: return("butt");
 case GDK_CAP_ROUND: return("round");
 case GDK_CAP_PROJECTING: return("projecting");
 default: return("");
 }
 }
 static char *joinStyleString(gint style)
 {
 switch(style) {
 case GDK_JOIN_MITER: return("miter");
 case GDK_JOIN_ROUND: return("round");
 case GDK_JOIN_BEVEL: return("bevel");
 default: return("");
 }
 }

gint eventDelete(GtkWidget *widget,
 GdkEvent *event, gpointer data) {
 return(FALSE);
 }
gint eventDestroy(GtkWidget *widget,
 GdkEvent *event, gpointer data) {
 gtk_main_quit();
 return(0);
 }
```

第 31 行至第 35 行创建了一个绘图区域，将其插入主窗口，并连接回调函数 `listValues()`。该函数由 "realize" 信号触发，这意味着回调只在窗口完全构建并具备显示能力时被调用一次。必须等待窗口被实体化（realized），因为只有那时才能获取到 GdkGC 的值。

回调函数 `listValues()` 从第 41 行开始，它会打印出 widget 中找到的图形上下文（GdkGC）中的所有值。widget 中还有许多图形上下文，我将在本章后续部分加以描述，但此程序在第 47 行获取的是名为 `white_gc` 的那个。GdkGC 对象中的值无法直接访问，因此，在第 48 行，对 `gdk_gc_get_values()` 的调用会将 GdkGC 中的信息填充到一个 GdkGCValues 结构体中。该函数的其余部分用于打印这些值。

第 50 行至第 55 行显示关于颜色的信息。图形上下文中存储了两种颜色：一种是前景色，另一种是背景色。所有的绘制和作画都使用前景色，而清除和擦除操作则使用背景色。

第 56 行列出了关于字体的信息。关于字体，已知的大概只有其内部 ID 号、字符在基线上方可能占据的最大像素数（上升距离），以及字符在基线下方可能占据的最大像素数（下降距离）。将这两个数值相加即可得到最高字符的高度。还有其他可用的尺寸信息，但只有在应用于特定字符串时才有意义，如第 13 章所述。

第 59 行调用在第 80 行定义的函数 `functionString()`，以显示将用于绘制像素的方法（函数）。如表 11-2 所示，有几种可用的方法。默认且最常见的是 `GDK_COPY`，它简单地用新值覆盖旧像素值。这些函数是逐位操作，因此无论每像素多少位，它们的工作方式完全相同。

### 表 11-2
### 用于写入像素的函数

| 函数 | 位运算描述 |
| :--- | :--- |
| `GDK_AND` | 每个目标位是源位和目标位进行“与”操作的结果。 |
| `GDK_AND_INVERT` | 源位被取反。然后，每个目标位是源位和目标位进行“与”操作的结果。 |
| `GDK_AND_REVERSE` | 目标位被取反。然后，每个目标位是源位和目标位进行“与”操作的结果。 |
| `GDK_CLEAR` | 目标像素的所有位被设置为 0。忽略源像素。 |
| `GDK_COPY` | 目标像素从源像素复制而来。 |
| `GDK_COPY_INVERT` | 源数据复制到目标后，再进行取反。 |
| `GDK_EQUIV` | 源位被取反。然后，每个目标位是源位和目标位进行“异或”操作的结果。 |
| `GDK_INVERT` | 目标像素的位被取反（0 变为 1，1 变为 0）。忽略源像素。 |
| `GDK_NAND` | 源和目标都被取反。然后，目标是源位和目标位进行“与”操作的结果。 |
| `GDK_NOOP` | 目标保持不变。 |
| `GDK_OR` | 每个目标位是源位和目标位进行“或”操作的结果。 |
| `GDK_OR_REVERSE` | 目标位被取反。然后，每个目标位是源位和目标位进行“或”操作的结果。 |
| `GDK_SET` | 所有目标像素被设置为 1。 |
| `GDK_XOR` | 每个目标像素位是源像素位和目标像素位进行“异或”操作的结果。 |

