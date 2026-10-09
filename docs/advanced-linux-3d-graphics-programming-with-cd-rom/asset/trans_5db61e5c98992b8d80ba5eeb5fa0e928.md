

# FACE <X> USES_TEX_SPACE <NAME>

`FACE <X> USES_TEX_SPACE` 属性使得多边形使用由纹理定义三角形定义的纹理空间。`<NAME>` 是要使用的纹理空间的名称，并隐式理解为是特定于扇区的（sector-specific）。这意味着在同一扇区中必须还有一个定义纹理空间 `<NAME>` 的纹理定义三角形。

通过为多个多边形分配相同的纹理空间，所有多边形在边缘处将无缝对齐。例如，对于墙壁，您通常会定义一个纹理空间，然后让墙壁上的所有多边形使用同一个纹理空间。下一个教程将说明如何执行此操作。

# FACE <X> IS_INVISIBLE

`FACE <X> IS_INVISIBLE` 属性仅对作为纹理定义三角形的面有意义。该属性指定该面不定义任何几何体（仅定义纹理空间），并且不应出现在最终的世界文件中。

这意味着，如果我们不指定 `IS_INVISIBLE` 属性，一个面可以同时是纹理定义三角形和几何多边形。如果网格几何体恰好包含一个大小和方向都正确的直角三角形，这将很有用；在这种情况下，我们可以直接重用现有的几何三角形作为纹理定义三角形。不过，通常网格中不会恰好存在这样的直角三角形，而人为引入此类三角形可能会很麻烦。在这些更常见的情况下，我们通常在网格中定义额外的三角形而不干扰现有几何体，并将这些额外三角形标记为不可见的纹理定义三角形。

# Actors 的属性

如果网格类型为 `ACTOR`，则世界文件中可能会出现以下附加属性，以指定关于扇区的更多信息。

## NAME <NAME>

`NAME` 属性指定一个不含空格的字符串，用于唯一标识 actor。`<NAME>` 代表实际字符串。

## PARENT <SECTOR>

`PARENT` 属性指定父扇区的名称 `<SECTOR>`，该对象最初位于此扇区中。该对象最初被插入到父扇区的对象列表中，以便与该扇区一起绘制。

请注意，父扇区并不拥有该对象，也不负责其销毁；该对象仅仅是位于扇区内。实际上，对象可以在扇区之间移动，在这种情况下，它必须将自己从旧扇区的对象列表中移除，并插入到新扇区的对象列表中。

## IS_CAMERA YES

`IS_CAMERA` 属性仅在值为 `YES` 时出现。存在此类行时，关联的网格被解释为相机对象，其起始位置和父扇区用于初始化相机位置。在这种情况下，下面描述的其他 actor 属性当前都被忽略。（不过，将几何体关联到相机对象也是可能的。）

## MESH <FILENAME.OBJ>

`MESH` 属性指定 Videoscape 网格的名称 `<FILENAME.OBJ>`，它定义插件对象的几何体。

## TEXTURE <FILENAME.PPM>

`TEXTURE` 属性指定纹理图像文件的名称 `<FILENAME.PPM>`，该文件应应用于插件对象的几何体。

## TEXCOORDS <FILENAME.UV>

`TEXCOORDS` 属性指定纹理坐标文件的名称 `<FILENAME.UV>`，该文件用于将纹理文件映射到多边形上。有关如何创建此文件的信息，请参见第 3 章。

## PLUGIN <FILENAME.SO>

`PLUGIN` 属性指定动态库文件的名称 `<FILENAME.SO>`，它控制此插件对象的行为。有关创建此类动态库文件的信息，请参阅入门配套书籍《Linex 3D Graphics Programming》或查看 CD-ROM 上包含的 Makefiles。

# VidsParser.pm 和 vidinfo 的属性解析

我们现在已经了解了如何使用 `blend_at` 将属性信息与网格关联起来，以及哪些特定属性对生成世界文件有意义。这是属性系统的写入端，我们基本上是将信息插入到属性数据库中。属性系统的读取端发生在模块 `VidsParser.pm` 中，在此处提取并评估属性信息。通过理解属性系统的运作方式，我们现在可以检查我们在早期讨论中跳过的 `VidsParser.pm` 中那些部分。

整个属性系统的关键是在 Videoscape 导出前后对每个网格进行唯一标识，我们通过嵌入 ID 号的二进制编码，利用网格几何体内重叠且位置特殊的边缘来实现这一点（这种方法我们也可以用“障眼法”来指代）。在解析 Videoscape 文件时，我们需要从网格几何体中提取 ID，以找到对应的属性文件 `attribXXX.dat`。从网格几何体中提取 ID 是通过工具 `vidinfo` 完成的。

### Listing 6.12: vidinfo.cc

```cpp
#include <unistd.h>
#include <stdio.h>
#include <vector>
#include <string>

struct vertex {
    float x, y, z;

    int operator==(const vertex &r) {
        return(  -0.001 < x-r.x && x-r.x < 0.001 &&
                  -0.001 < y-r.y && y-r.y < 0.001 &&
                  -0.001 < z-r.z && z-r.z < 0.001
                );
    }
};

int main(int argc, char **argv)
{
    if(argc != 2) {
        printf("Usage: %s videoscape_file.obj", argv[0]);
        exit(-1);
    }
    FILE *fp;
    unsigned long oid;
    vector<vertex> vidscape_vertices;
    char vidscape_line[1024];
    float float1, float2, float3;
    int found=0;
    char blender_work_fname[1024];
    sprintf(blender_work_fname, argv[1]);
    fp = fopen(blender_work_fname, "rt+");
    int lineno = 1;
    int num_vertices=0;
    float xsun=0.0, ysum=0.0, zsum=0.0;
    float xc,yc,zc;
    float x0_0,y0_0,z0_0 ,  x0_1,y0_1,z0_1,
        x1_0,y1_0,z1_0 ,  x1_1,y1_1,z1_1,
        x2_0,y2_0,z2_0 ,  x2_1,y2_1,z2_1;
    int prev_v_vtxcount=0, prev_v_vtx0_0, prev_v_vtx0_1;
    int overlapping_edge_count=0;
    vertex pos;
    vertex x_axis, y_axis, z_axis;
    
    while(!feof(fp) && !found) {
        fgets(vidscape_line, 1024, fp);
        if(!feof(fp)) {
            #define VIDSC_VTXCOUNT_LINENO 2
            if((lineno==VIDSC_VTXCOUNT_LINENO &&
                lineno!=VIDSC_VTXCOUNT_LINENO + num_vertices))
            {
                vertex v;
                sscanf(vidscape_line, "%f %f %f", &float1,&float2,&float3);
                v.x = float1;
                v.y = float2;
                v.z = float3;
                vidscape_vertices.push_back(v);
            }
            if (lineno == VIDSC_VTXCOUNT_LINENO) {
                sscanf(vidscape_line, "%d", &num_vertices);
            }

            int sc;
            int v_txtcount=0, v_vtx0_0=0, v_vtx0_1=0;
            unsigned long v_color;
            char v_color_str[255];
            
            if((lineno == VIDSC_VTXCOUNT_LINENO + num_vertices + 1)
                && (sc=sscanf(vidscape_line, "%d %d %d %s",&v_txtcount, &v_vtx0_0, &v_vtx0_1, v_color_str))==4
                && (v_txtcount==2))
            {
                if((prev_v_txtcount==2
                    &&(vidscape_vertices[v_vtx0_0]==vidscape_vertices[prev_v_vtx0_0]
                    && vidscape_vertices[v_vtx0_1]==vidscape_vertices[prev_v_vtx0_1])
                    ||(vidscape_vertices[v_vtx0_0]==vidscape_vertices[prev_v_vtx0_1]
                    && vidscape_vertices[v_vtx0_1]==vidscape_vertices[prev_v_vtx0_0]))
                    ) {
                        overlapping_edge_count++;
                    }else {
                        overlapping_edge_count--;
                    }

                prev_v_txtcount = v_txtcount;
                prev_v_vtx0_0 = v_vtx0_0;
                prev_v_vtx0_1 = v_vtx0_1;
            }
            if((overlapping_edge_count==4))
            {
                int x_v0, x_v1,
                    y_v0, y_v1,
                    z_v0, z_v1;

                fgets(vidscape_line, 1024, fp);
                sscanf(vidscape_line, "%d %d %d",&v_txtcount, &x_v0, &x_v1);
                fgets(vidscape_line, 1024, fp);
                sscanf(vidscape_line, "%d %d %d",&v_txtcount, &y_v0, &y_v1);
                fgets(vidscape_line, 1024, fp);
                sscanf(vidscape_line, "%d %d %d",&v_txtcount, &z_v0, &z_v1);

                vertex x0, y0, x1, y1, z0, z1;
                if ( vidscape_vertices[x_v0] == vidscape_vertices[y_v0]) {
                    x0 = vidscape_vertices[x_v0];
                    y0 = vidscape_vertices[y_v0];
                    x1 = vidscape_vertices[x_v1];
                    y1 = vidscape_vertices[y_v1];
                }else if(vidscape_vertices[x_v0] == vidscape_vertices[y_v1]) {
                    x0 = vidscape_vertices[x_v0];
                    y0 = vidscape_vertices[y_v1];
                    x1 = vidscape_vertices[x_v1];
                    y1 = vidscape_vertices[y_v1];
                }
                // Note: The original OCR cut off here, but context suggests continued logic
            }
            lineno++;
        }
    }
}
```

