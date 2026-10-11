```
```
}
echo();
str[i] = '\0';
wrefresh(pwin);

mvwprintw(pwin, 1, 1, "You typed: %s\n", str);
box(pwin, ACS_VLINE, ACS_HLINE);
wrefresh(pwin);
sleep(3);

delwin(pwin);
app_exit();
}
```
```

The screens this program creates are illustrated in Figures 11.9 and 11.10.

![](bbox=[0.106, 0.338, 0.888, 0.737])