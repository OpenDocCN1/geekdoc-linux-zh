```
scores = gnome_scores_new(3,names,values,times,FALSE);
gtk_widget_show_all(scores);

gtk_main();
exit(0);
}
```

![](bbox=[0.113, 0.242, 0.71, 0.383])

# # GnomeSpell

This is an incomplete widget. When completed, it will use the Linux ispell program to scan text for words not found in the dictionary, and then display the words — possibly along with some suggested alternatives — so the user can correct the spelling.

**Inheritance**
GnomeSpell->GtkVBox->GtkBox->GtkContainer->GtkWidget->
GtkObject

**Functions**
void gdk_child_register(pid_t pid, GChildFunc func, gpointer user_data)
void gnome_spell_accept(GnomeSpell \*spell, gchar \*word)
gint gnome_spell_check(GnomeSpell \*spell, gchar \*str)
guint gnome_spell_get_type()
void gnome_spell_insert(GnomeSpell \*spell, gchar \*word, gint lowercase)
void gnome_spell_kill(GnomeSpell \*spell)
GtkWidget \*gnome_spell_new()
int gnome_spell_next(GnomeSpell \*spell)

# # GnomeStock

The GnomeStock widget is used to create buttons, pixmaps, and other objects, and to register them with the set of predefined stock objects. An application also can use it to add new pixmaps for its own purposes.