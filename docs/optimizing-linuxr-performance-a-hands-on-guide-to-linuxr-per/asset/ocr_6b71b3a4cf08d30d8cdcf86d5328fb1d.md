# 11.10. Trying a Possible Solution

So, as we have, bonobo_window_add_popup is an expensive function that must be called every time we want to create a pop-up menu. If we are repeatedly calling it with the same parameters, it may be possible to cache the value it returns from the initial call and use that instead of calling that expensive function. Listing 11.19 shows an example of a rewritten function to do just that.

# Listing 11.19.

```
void
fm_directory_view_pop_up_background_context_menu
(FMDirectoryView *view,
GdkButton *event)
{
 /* Primitive Cache */
  static FMDirectoryView *old_view = NULL;
  static GtkMenu *old_menu = NULL;

  g_assert (FM_IS_DIRECTORY_VIEW (view));

  /* Make the context menu items not flash as they update to
  proper disabled;
   * states. by forcing menus to update now.
   */
  if ((old_view != view) ||
      view->menu_states_untrustworthy)
  {
    update_menu_if_pending(view);
    old_view = view;
    old_menu = create_popup_menu(view,
      FM_DIRECTORY_VIEW_POPUP_PATH_BACKGROUND);
  }

  eel_pop_up_context_menu (old_menu,
    EEL_DEFAULT_POPUP_MENU_DISPLACEMENT,
    EEL_DEFAULT_POPUP_MENU_DISPLACEMENT,
    event);
}
```

In this case, we remember the menu that was generated last. If we are in the same view, and we do not believe that the menu for view has changed, we just use the menu that we used instead of creating a new one. This is not a sophisticated technique, and it will break down if the user does not open a pop-up menu in directory 1, and opens in directory 2, if there opens a pop-up menu in directory 1, nautilus will create a new one. When opening a menu, the first check is to see whether we already have menu in the cache. If the cached menus could be viewed; otherwise, one could be created. This could be especially useful for special directories, such as the desktop, computer, or home where the user will likely open a pop-up menu more than once. After applying this proposed solution and with the 100ms timeout, the time has dropped to 24.0 seconds. This is a 20% performance improvement, and close to the improvement that we would get if we did not create the menu at all (21 seconds). Creating pop-up menus in various directories worked