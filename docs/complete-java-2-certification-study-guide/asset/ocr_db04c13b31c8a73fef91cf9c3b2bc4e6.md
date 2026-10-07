The output is

France:
17/01/05
17 janv. 2005
17 janvier 2005
lundi 17 janvier 2005

China:
05-1-17
2005?1?17?
2005?1?17? ???

Italy:
17/01/05
17-genna-2005
lunedi 17 gennaio 2005

# Formatting Numbers and Currency

The java.text.Number class is useful for formatting numbers in general, and especially numbers that represent currency.

Standard number formats vary somewhat from one region to another. The variation is slight compared to variations around dates, but it needs to be dealt with. Obviously, variations in currency formats are significant. So it is not surprising that the behavior of the Format class is affected by locale. Once again, a default instance of the formatting class is controlled by the current locale; it is possible to use other instances that use other locales.

NumberFormat is actually an abstract superclass, so you can never call its constructors. Instead you call a static factory method. The factory methods you should know for the exam are these:

```
public static NumberFormat getInstance() Returns a number formatter that uses the current locale.
```

```
public static NumberFormat getInstance(Locale loc) Returns a number formatter that uses the specified locale.
```

```
public static NumberFormat getCurrencyInstance() Returns a currency formatter that uses the current locale.
```

```
public static NumberFormat getInstance(Locale loc) Returns a currency formatter that uses the specified locale.
```