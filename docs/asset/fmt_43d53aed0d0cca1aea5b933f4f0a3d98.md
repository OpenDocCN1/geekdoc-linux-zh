
# 检查 PPD 文件结构

每个 PPD 文件包含许多能力属性、打印机选项和冲突定义。页面大小选项还包括物理边距以及打印机的最小和最大尺寸。所有这些信息都存储在 `ppd_file_t` 结构中。`ppd_file_t` 结构的成员如表 14.3 所示

## 表 14.3 PPD 能力值

| 名称 | 类型 | 描述 |
|---|---|---|
| accurate_screens | | 打印机是否支持精确色彩的指示 |
| color_device | int | 打印机是否支持色彩空间的指示 |
| | `ppd_cs_t` | 默认色彩空间 |
| num_consts | int | 约束数量 |
| | `ppd_const_t *` | 约束 |
| contour_only | int | 打印机是否仅为连续调的指示 |
| custom_margins | float [4] | 自定义页面大小的左、下、右、上边距 |
| custom_max | float [2] | 自定义页面大小的最大尺寸 |
| custom_min | float [2] | 自定义页面大小支持的最小尺寸 |
| num_emulations | int | 打印机支持的仿真器数量 |
| | `ppd_emul_t *` | 打印机支持的仿真器 |
| num_filters | int | 此打印机的过滤器数量 |
| | char ** | 此打印机的过滤器 |
| flip_duplex | int | 双面打印时打印机是否需要填充反面的指示 |
| num_fonts | int | 打印机拥有的字体数量 |
| | char ** | 打印机上的字体 |
| num_groups | int | 选项组数量 |
| | `ppd_group_t *` | 选项组 |
| jcl_begin | char * | 每个任务前发送的作业控制语言 (JCL) 字符串 | 在 PostScript 模式下放入打印机的 JCL 字符串 |
| jcl_end | char * | 结束任务的 JCL 字符串 | 横向页面的方向 |
| landscape | int | |
| lang_encoding | char * | 用于选项文本的字符集 | 用于选项字符串的语言，如英语、法语或西班牙语 |
| lang_version | char * | PostScript 语言级别，从 1 到 3 |
| language_level | int | |
| manual_copies | int | 是否需要手动复制的指示 |
| manufacturer | char * | 打印机名称 |
| model_number | int | 驱动特定的型号编号 |
| modelname | char * | 打印机型号名称 |

## 表 14.3 续接

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| nickname | char * | 打印机的别名；这通常是显示给用户的名称 |
| patches | char * | 在每个作业前发送给打印机的补丁命令 |
| product | char * | 打印机产品名称 |
| num_profiles | int | 颜色配置的数量 |
| profiles | `ppd_profile_t *` | 颜色配置 |
| shortnickname | char * | 打印机的短别名 |
| num_sizes | int | 尺寸的数量 |
| sizes | char * | 每分钟打印页数 |
| throughput | char * | 提供的 TrueType 字体光栅化器，通常为 "Type42" |
| variable_sizes | int | 打印机是否支持自定义尺寸指示 |

如果相应的 PPD 文件属性未包含在文件中，则大多数字符串值可以为 NULL。特别是，在显示 `manufacturer` 字段的值时要小心，尽管 PPD 规范要求包含，但并非所有 PPD 文件都包含该字段。

## 选项与组

PPD 文件支持多个选项，PPD 函数将其存储在 `ppd_option_t` 和 `ppd_choice_t` 结构中。

每个选项又关联到一个存储在 `ppd_group_t` 结构中的组。组可以在 PPD 文件中指定；如果选项未与任何组关联，则根据选项类型被放入“General”（常规）或“Extra”（额外）组。

PPD 文件的组列表存储在 `num_groups` 和 `groups` 成员中。每个组都有一个可读的名称，例如“General”或“Installable Options”（可安装选项），并包含一个选项数组。

组中的选项位于 `ppd_group_t` 结构的 `num_options` 和 `options` 成员中。每个选项都有一个名称（"PageSize"）、一个可读的名称（"Media Size"）、命令排序信息、一个选项类型（布尔、单选或多选）、该选项的默认选择以及一个选择数组。选项不区分大小写。

选项中的选择位于 `ppd_option_t` 结构的 `num_choices` 和 `choices` 成员中。每个选择都有一个值（"Letter"）、一个可读的名称（"Letter – 8.5x11 inches"）、一个指示该选择是否被标记的布尔值，以及选择该选项时发送给打印机的 PostScript 命令。选择值不区分大小。

## 显示 PPD 文件内容

CUPS 源码包含一个名为 `testppd` 的程序，它可以加载 PPD 文件并显示组、选项和选择。列表 14.4 显示了 `testppd` 的源代码。构建 `testppd` 后，你应该能够运行以下命令：

```
/testppd /usr/share/cups/model/deskjet.ppd ENTER
```

```
FILE: /usr/share/cups/model/deskjet.ppd

language_level = 3

color_device = TRUE

variable_sizes = FALSE

landscape = 90

colorspace = PPD_CS_RGB

num_emulations = 0

lang_encoding = ISOLatin1

lang_version = English

modelname = HP DeskJet Series

rasterizer = Type42

manufacturer = ESP

product = (CUPS v1.1)

nickname = HP DeskJet Series CUPS v1.1

shortnickname = HP DeskJet Series

patches =  bytes

num_groups = 2

group[0] = Extra

options[0] = ColorModel (Output Mode) PICKONE ANY 10

RGB (CMY Color)

CMYK (CMYK Color) *

Gray (Grayscale)

options[1] = Resolution (Output Resolution) PICKONE ANY 20

15dpi (150 DPI)

300dpi (300 DPI) *

600dpi (600 DPI) *

group[1] = General

options[0] = PageSize(Media Size) PICKONE ANY 10

A3 (A3) = 11.69x16.54in(0.2,0.5,11.4,16.0)

A4 (A4) = 8.26x11.69in(0.2,0.5,8.0,11.2)

---

Legal (US Legal) = 8.50x14.00in(0.2,0.5,8.2,13.5) *

Letter (US Letter) = 8.50x11.00in(0.2,0.5,8.2,10.5) *

Tabloid (US Tabloid) = 11.00x17.00in(0.2,0.5,10.8,16.5)
```

## 第 14 章 使用 CUPS API 函数

```
options[1] = InputSlot (Media Source) PICKONE ANY 10

Envelope (Envelope Feed)

Manual (Manual Feed)

Tray (Tray) *

options[2] = MediaType (Media Type) PICKONE ANY 10

Bond (Bond Paper)

Glossy (Glossy Paper)

Plain (Plain Paper) *

Special (Special Paper)

Transparency (Transparency)

options[3] = PageRegion (PageRegion) PICKONE ANY 10

A3 (A3) = 11.69x16.54in(0.2,0.5,11.4,16.0)

A4 (A4) = 8.26x11.69in(0.2,0.5,8.0,11.2)

---

Legal (US Legal) = 8.50x14.00in(0.2,0.5,8.2,13.5) *

Letter (US Letter) = 8.50x11.00in(0.2,0.5,8.2,10.5) *

Tabloid (US Tabloid) = 11.00x17.00in(0.2,0.5,10.8,16.5)
```
*(注：此处原文文本似乎存在重复或截断，已根据要求翻译可见部分)*

## 列表 14.4 testppd.c 源代码

```c
/* 包含 CUPS 头文件。 */
#include <cups/cups.h>

/* 包含字符串定义 */
#include <string.h>

int main(int argc, char *argv[])
{
    /* 0 status */
    /* 命令行参数 */
    int i, j, k, m; /* 循环变量 */
    const char *filename; /* 要加载的文件 */
    ppd_file_t *ppd; /* PPD 记录 */
    ppd_size_t *size; /* 尺寸记录 */
    ppd_group_t *group; /* UI 组 */
    ppd_option_t *option; /* 标准 UI 选项 */
    /* 标准 UI 选择 */
    static char *uis[] = { "BOOLE", "PICKONE", "PICKMANY" };
    static char *sections[] = { "ANY", "DOCUMENT", "EXIT", "PAGE", "PROLOG" };
    /* 显示列出的每个文件的 PPD... */
    if (argc == 1) {
        fprintf(stderr, "Usage: %s ppd.ppd filename.ppd\n", argv[0]);
        return (1);
    }
    for (i = 1; i < argc; i++) {
        if (strstr(argv[i], ".ppd"))
            filename = argv[i];
        else
            filename = cupsGetPPD(argv[i]);
    }
    if ((ppd = ppdOpenFile(filename)) == NULL) {
        fprintf(stderr, "Unable to open '%s' as a PPD file!\n", filename);
        continue;
    }
    printf("FILE: %s\n", filename);
    printf("language_level = %d\n", ppd->language_level);
    printf("color_device = %s\n", ppd->color_device ? "TRUE" : "FALSE");
    printf("variable_sizes = %s\n", ppd->variable_sizes ? "TRUE" : "FALSE");
    printf("landscape = %d\n", ppd->landscape);
    switch (ppd->colorspace) {
        case PPD_CS_CMYK:
            puts("colorspace = PPD_CS_CMYK");
            break;
        case PPD_CS_CMY:
            puts("colorspace = PPD_CS_CMY");
            break;
        case PPD_CS_GRAY:
            puts("colorspace = PPD_CS_GRAY");
            break;
        case PPD_CS_RGB:
            puts("colorspace = PPD_CS_RGB");
            break;
        default:
            puts("colorspace = <unknown>");
            break;
    }
    printf("num_emulations = %d\n", ppd->num_emulations);
    for (j = 0; j < ppd->num_emulations; j++)
        printf("emulations[j] = %s\n", ppd->emulations[j].name);
    printf("lang_encoding = %s\n", ppd->lang_encoding);
    printf("lang_version = %s\n", ppd->lang_version);
    printf("modelname = %s\n", ppd->modelname);
    printf("rasterizer = %s\n", ppd->rasterizer == NULL ? "None" : ppd->rasterizer);
    printf("manufacturer = %s\n", ppd->manufacturer);
    printf("product = %s\n", ppd->product);
    printf("nickname = %s\n", ppd->nickname);
    printf("shortnickname = %s\n", ppd->shortnickname);
    printf("patches = %s\n", ppd->patches);
    printf("num_groups = %d\n", ppd->num_groups);
    for (j = 0, group = ppd->groups; j < ppd->num_groups; j++, group++)
    {
        printf("group[%d] = %s\n", j, group->text);
        for (k = 0, option = group->options; k < group->num_options; k++, option++)
        {
            printf("options[%d] = %s (%s) %s %s\n", k, option->keyword, option->text, option->ui, option->order);
            if (strcmp(option->keyword, "PageSize") == 0 ||
                strcmp(option->keyword, "PageRegion") == 0)
            {
                for (m = 0, choice = option->choices; m > 0; m--, choice++)
                {
                    size = ppdPageSize(ppd, choice->choice);
                    if (size == NULL)
                        printf("%s (%s) = ERROR", choice->choice, choice->text);
                    else
                        printf("%s (%s) = %.2fx%.2fin \n%.1f,%.1f,%.1f,%.1f\n",
                               choice->choice, choice->text,
                               size->width / 72.0, size->length / 72.0,
                               size->left / 72.0, size->bottom / 72.0,
                               size->right / 72.0, size->top / 72.0);
                    if (strcmp(option->defchoice, choice->choice) == 0)
```
