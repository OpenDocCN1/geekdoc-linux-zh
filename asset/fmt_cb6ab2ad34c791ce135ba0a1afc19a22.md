
```c
keypad(stdscr, TRUE);
break();
nocho();
key = 0;
while (key == 'q' && key != KEY_ENTER && key != '\n') {
    if (key == KEY_UP) {
        if (selected_row == 0)
            selected_row = max_row - 1;
        else
            selected_row--;
    }
    if (key == KEY_DOWN) {
        if (selected_row == (max_row - 1))
            selected_row = 0;
        else
            selected_row++;
    }
    selected = *choices[selected_row];
draw_menu(choices, selected_row, start_screenrow, start_screencol);
key = getch();
keypad(stdscr, FALSE);
nocbreak();
echo();
if (key == 'q')
    selected = 'q';
return (selected);
```

2. 注意在 `getchoice` 内部还调用了两个本地函数：`clear_all_screen` 和 `draw_menu`。我们先看 `draw_menu`：

```c
void draw_menu(char *options[], int current_highlight,
 start_row, int start_col)
{
    int current_row = 0;
    char *option_ptr;
    char *txt_ptr;
    option_ptr = options;
    while (*option_ptr) {
        if (current_row == current_highlight) attron(A_STANDOUT);
        txt_ptr = options[current_row];
        txt_ptr++;
        mvprintw(start_row + current_row, start_col, "%s", txt_ptr);
        if (current_row == current_highlight) atroff(A_STANDOUT);
        current_row++;
        option_ptr++;
    }

    mvprintw(start_row + current_row + 3, start_col,
        "Move highlight then press Return");
    refresh();
}
```

3. `clear_all_screen` 出人意料的是它会清空屏幕并重写标题。如果选择了 CD，则会显示其信息。

```c
void clear_all_screen()
{
    clear();
    mvprintw(2, 20, "%s", "CD Database Application");
    if (current_cd[0]) {
        mvprintw(ERROR_LINE, 0, "Current CD: %s\n",
                 current_cd, current_cd);
    }
    refresh();
}
```

现在我们查看添加或更新 CD 数据库的函数。从 `main` 调用的函数有 `add_record`、`update_cd` 和 `remove_cd`。这些函数调用了将在后续章节定义的函数。

## 尝试一下——数据库操作

1. 首先，我们如何向数据库添加新的 CD 记录？

```c
mvprintw(PROMPT_LINE-2, "About to add this new entry:");
print(cd_entry, "%s,%s",
catalog_number, cd_title, artist);
mvprintw(PROMPT_LINE, 5, "%s", cd_entry);
refresh();
move(PROMPT_LINE, 0);
if (get_confirm()) {
    insert_title(cd_entry);
}
```

2. `get_string` 在当前屏幕位置提示并读取输入。它还会删除末尾的换行符。

```c
void get_string(char *string) {
    int len;
    wgetstr(stdscr, string, MAX_STRING);
    len = strlen(string);
    if (len > 0 && string[len - 1] == '\n')
        string[len - 1] = '\0';
}
```

3. `get_confirm`

```c
{
    int confirmed = 0;

    char first_char;

    mvprintw(PROMPT_LINE, 5, "Are you sure?");

    clrol();

    refresh();

    cbreak();

    first_char = getch();

    if (first_char == 'Y' || first_char == 'y')

        confirmed = 1;

    if (!confirmed) {

        mvprintw(PROMPT_LINE, 1, "Cancelled");

        clrol();

        refresh();

        sleep(1);

    }

    return confirmed;

}
```

4. 最后，我们查看 `insert_title`。它通过将标题字符串附加到文件末尾来更新 CD 数据库。

```c
void insert_title(char *cditle)
{
    FILE *fp = fopen(title_file, "a");

    if (!fp) {
        mvprintw(ERROR_LINE, 0, "cannot open CD database");
    }
    size_t size;
    fprintf(fp, "%s\n", cditle);
    fclose(fp);
}
```

5. `main` 调用的文件操作函数从 `update_cd` 开始。该函数使用了滚动窗口并需要一些全局定义的常量，因为稍后 `list_tracks` 函数会用到它们。

```c
#define BOXED_LINES 11
#define BOXED_ROWS 60
#define BOX_LINE_POS 8
#define BOX_ROW_POS 2
```

`update_cd` 允许用户重新输入 CD 的轨道。删除轨道记录后，它会提示输入新信息。

```c
void update_cd()
{
    FILE *tracks_fp;
    char tracks_name[MAX_STRING];
    int len;
    int track = 1;
    int screen_line = 1;
    WINDOW *box_window_ptr;
    WINDOW *sub_window_ptr;

    clear_all_windows();

    mvprintw(PROMPT_LINE, 0, "Re-entering tracks for CD.");

    if (!get_confirm()) {
        return;
    }

    move(PROMPT_LINE, 0);
    rtol();
    remove_tracks();
    mvprintw(MESSAGE_LINE, 0, "Enter a blank line to finish");
    tracks_fp = fopen(tracks_file, "a");
}
```

我们稍后会继续列表；现在想停一下，介绍如何在滚动窗口中输入信息。技巧是设置一个子窗口，在其边缘画一个框，然后在框内再添加一个新的滚动子窗口。

```c
sub_window_ptr = subwin(stdscr, BOXED_LINES + 2, BOXED_ROWS + 2,
BOX_LINE_POS - 1, BOX_ROW_POS - 1);

if (!box_window_ptr)
  return;

box(box_window_ptr, ACS_VLINE, ACS_HLINE);

sub_window_ptr = subwin(stdscr, BOXED_LINES, BOXED_ROWS,
BOX_LINE_POS, BOX_ROW_POS);

if (!sub_window_ptr)
  return;

scrollok(sub_window_ptr, TRUE);
werase(sub_window_ptr);
touchwin(stdscr);

do {
  mvprintw(sub_window_ptr, screen_line++, BOX_ROW_POS + 2,
  "Track @: %s", track);
  rtol();
  refresh();
  wgetnstr(sub_window_ptr, track_name, MAX_STRING);
  len = strlen(track_name);
  if (len > 0 && track_name[len - 1] == '\n')
    track_name[len - 1] = '0';
  if (*track_name)
    fprintf(tracks_fp, "%s,%d\n", current_cat, track, track_name);
  track++;
  if (screen_line > BOXED_LINES - 1) {
    /* time to start scrolling */
    scroll(sub_window_ptr);
    screen_line--;
  }
} while (*track_name);

delwin(sub_window_ptr);
fclose(tracks_fp);
```

6. `main` 调用的最后一个函数是 `remove_cd`。

```c
void remove_cd()
{
  FILE *titles_fp, *temp_fp;
  char entry[MAX_ENTRY];
  int cat_length;

  if (current_cat[0] == '0')
    return;

  clear_all_screen();

  mvprintw(PROMPT_LINE, 0, "About to remove CD %s: %s",
  current_cat, current_cd);

  if (!get_confirm())
    return;

  cat_length = strlen(current_cat);
}
```

## 第 6 章

```c
/* 将标题文件拷贝到临时文件，忽略此 CD */
titles_fp = fopen(title_file, "r");
temp_fp = fopen(temp_file, "w");
while (gets(entry, MAX_ENTRY, fp)) {
  /* 比较目录索引号，如果不匹配则拷贝条目 */
  if (strncmp(current_cat, entry, cat_length) != 0)
    fputs(entry, temp_fp);
}
close(titles_fp);
close(temp_fp);

/* 删除标题文件，并重命名临时文件 */
unlink(title_file);
rename(temp_file, title_file);

/* 现在对轨道文件执行相同的操作 */
remove(tracks_);

/* 将当前 CD 重置为 'None' */
current_cd[0] = '\0';
```

7. 我们只需要列出 `remove_tracks` 函数，这是用于从 CD 中删除轨道的函数。它被 `update_cd` 和 `remove_cd` 同时调用。

```c
void remove_tracks () {
  FILE *tracks_fp, *temp_fp;
  char entry[MAX_ENTRY];
  int cat_length;

  if (current_cd[0] == '\0')
    return;

  cat_length = strlen(current_cat);

  tracks_fp = fopen(tracks_file, "r");
  if (tracks_fp == (FILE *)NULL) return;

  temp_fp = fopen(temp_file, "w");

  while (gets(entry, MAX_ENTRY, tracks_fp)) {
    /* 比较目录索引号，如果不匹配则拷贝条目 */
    if (strncmp(current_cat, entry, cat_length) != 0)
      fputs(entry, temp_fp);
  }

  close(tracks_fp);
  close(temp_fp);

  /* 删除轨道文件，并重命名临时文件 */
  unlink(tracks_file);
  rename(temp_file, tracks_file);
}
```

## 使用 curses 管理文本文本界面

### 尝试一下——查询 CD 数据库

- 1. 对于所有收藏爱好来说，了解自己拥有了多少种收藏品是至关重要的。下一个函数执行得非常出色；它扫描数据库，统计标题和轨道。

```c
void count_cds() {
  FILE *titles_fp, *tracks_fp;
  char entry[MAX_ENTRY];
  int titles = 0;
  int tracks = 0;

  titles_fp = fopen(title_file, "r");
  if (titles_fp) {
    while (fgets(entry, MAX_ENTRY, titles_fp)) {
      titles++;
    }
    fclose(titles_fp);
  }

  tracks_fp = fopen(tracks_file, "r");
  if (tracks_fp) {
    while (fgets(entry, MAX_ENTRY, tracks_fp)) {
      tracks++;
    }
    fclose(tracks_fp);
  }

  mvprintf(ERROR_LINE, 0, "数据库包含 %d 个标题，总共 %d 条轨道。", titles, tracks);
  get_return();
}
```

- 2. 你丢失了最喜欢的 CD 的内页介绍，但别担心！由于已经仔细输入了详细信息，你现在可以使用 `find_cd` 找到轨道列表。它会提示输入一个在数据库中匹配的字符串，并将全局变量 `current_cd` 设置为找到的 CD 标题。

```c
void find_cd() {
  char match[MAX_STRING], entry[MAX_ENTRY];
  FILE *titles_fp;
  int count = 0;
  char *found, *title, *catalog;

  mvprintf(Q_LINE, 0, "要在 CD 标题中搜索的字符串:");
  get_string(match);

  titles_fp = fopen(title_file, "r");
  if (titles_fp) {
    while (fgets(entry, MAX_ENTRY, titles_fp)) {
      /* 跳过目录索引号 */
      catalog = entry;
      if (found = strstr(catalog, ",")) {
        found = "\0";
```

尽管 `catalog` 指向的数组比 `current_cat` 大，理论上可能会覆盖内存，但 `fgets` 中的检查防止了这种情况。

- 3. 最后，我们需要能够在屏幕上列出选中的 CD。我们利用了上一节中 `update_cd` 所使用的子窗口的定义。

```c
void list_tracks()
{
    FILE *tracks_fp;
    char entry[MAX_ENTRY];
    int cat_length;
    int lines_cp = 0;
    WINDOW *track_pad_ptr;
    int tracks = 0;
    int key;
    int first_line = 0;

    if (current_cd[0] == '\0') {
        mvprintw(ERROR_LINE, 0, "你必须先选择一个 CD.");
    }

    get_return();
    return;
}
```

```c
clear_all_screen();
```
