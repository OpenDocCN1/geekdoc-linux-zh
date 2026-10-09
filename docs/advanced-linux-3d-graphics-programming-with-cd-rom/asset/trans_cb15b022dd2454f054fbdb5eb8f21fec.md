

**注意** 计算过程中微小的数值误差意味着我们应不时确保矩阵中的所有轴向量相互正交且长度为一，这个过程称为*正交归一化*。我们可以通过归一化 VRi 和 VUP，计算 VRi 和 VUP 的叉积作为 VFW，然后重新计算 VFW 和 VRi 的叉积作为 VUP 来实现。此时，这三个向量应相互垂直，且长度应为一。

`update` 中的碰撞检测与类 `l3d_camera_collidable` 的几乎相同。我们将对象的包围球与环境中的所有多边形进行检查，确保不与任何多边形发生碰撞。此外，我们还确保对象不与环境中的任何其他插件对象发生碰撞。我们使用 `explosion_factor` 变量来迭代增加在检测到碰撞后执行的弹簧式反弹的大小。通过这种方式，多个同时发生的碰撞最终会通过再次推开碰撞对象来解决。

碰撞检测还用于检测对象何时穿过传送门（portal）从一个扇区（sector）进入另一个扇区。如果发生这种情况，对象会将自己从之前扇区的对象列表中删除，并加入新扇区的对象列表。这样，当绘制新的包含扇区时，也能正确绘制刚刚进入该扇区的对象。

插件的*析构函数*和*复制数据*功能与 `vidmesh` 的本质相同。

### 列表 8-18：`seeker.h`

```cpp
#include "../../dynamics/plugins/plugin.h"
#include "../../dynamics/colsp.h"

class l3d_texture_data;

typedef enum movement_states
{NONE, AROUND_VFW, AROUND_VRI, AROUND_VUP, ALONG_VFW, ALONG_VRI, ALONG_VUP} movement_states;

static const movement_states states_array[]=
{NONE, AROUND_VFW, AROUND_VRI, AROUND_VUP,
 ALONG_VFW, ALONG_VRI, ALONG_VUP};

class l3d_plugin_videoscape_mesh_seeker
{
public:
    l3d_plugin_environment *plugin_env;
    l3d_texture_data *tex_data;
    
    l3d_plugin_videoscape_mesh_seeker(l3d_plugin_environment *env);
    virtual ~l3d_plugin_videoscape_mesh_seeker(void);
    char mesh_fname[1024], texcoord_fname[1024], texture_fname[1024];
    
    int tick_count, max_ticks;
    movement_states movement_state;
    int turning_velocity;
    l3d_real moving_velocity;
};
```

### 列表 8-19：`seeker.cc`

```cpp
#include "../.../system/sys_dep.h"
#include "../.../geom/object/octo1l.h"
#include "../.../geom/object/sector.h"
#include "../.../geom/texture/texload.h"
#include "../.../geom/polygon/p3_tex.h"
#include "../.../dynamics/plugins/pluginenv.h"
#include <stdio.h>
#include <string.h>
#include "seeker.h"

l3d_plugin_videoscape_mesh_seeker::l3d_plugin_videoscape_mesh_seeker
(l3d_plugin_environment *env)
{
	plugin_env = env;
	tex_data = NULL;
}

l3d_plugin_videoscape_mesh_seeker::~l3d_plugin_videoscape_mesh_seeker(void) {
	if(tex_data) delete tex_data;
	delete plugin_env;
}

extern "C" {

	void constructor(l3d_object *target, void *data) {
		l3d_object_clipable_boundable_collidable *obj;
		obj = (l3d_object_clipable_boundable_collidable *) (target);

		obj->collision_sphere_radius = int_to_l3d_real(4);

		l3d_plugin_environment *env = (l3d_plugin_environment *)data;
		l3d_plugin_videoscape_mesh *mesh;

		target->plugin_data = mesh = new l3d_plugin_videoscape_mesh_seeker(env);
		l3d_texture_loader *tl = env->texLoader;

		mesh->tick_count = 0;
		mesh->max_ticks = rand() % 50 + 10;
		mesh->movement_state = states_array[rand() % 7];

		char rest_params[4096];
		strncpy(rest_params, (char *)env->data, sizeof(rest_params));
		char *tok;

		float posx, posy, posz;
		float xaxis_x, xaxis_y, xaxis_z,
			 yaxis_x, yaxis_y, yaxis_z,
			 zaxis_x, zaxis_y, zaxis_z;
		l3d_matrix position, orientation;

		strcpy(mesh->texcoord_fname, "");
		strcpy(mesh->texture_fname, "");

		position.set(int_to_l3d_real(1),
		              int_to_l3d_real(0),
		              int_to_l3d_real(0),
		              int_to_l3d_real(0),
		              int_to_l3d_real(0),
		              int_to_l3d_real(0),
		              int_to_l3d_real(0),
		              int_to_l3d_real(0),
		              int_to_l3d_real(0),
		              int_to_l3d_real(1));
		orientation = position;

		tok = strtok(rest_params, " "); if(tok) {sscanf(tok, "%f", &posx);} 
		tok = strtok(NULL, " "); if(tok) {sscanf(tok, "%f", &posy);} 
		tok = strtok(NULL, " "); if(tok) {sscanf(tok, "%f", &posz);} 
		tok = strtok(NULL, " "); if(tok) {sscanf(tok, "%f", &xaxis_x);} 
		tok = strtok(NULL, " "); if(tok) {sscanf(tok, "%f", &xaxis_y);} 
		tok = strtok(NULL, " "); if(tok) {sscanf(tok, "%f", &xaxis_z);} 
		tok = strtok(NULL, " "); if(tok) {sscanf(tok, "%f", &yaxis_x);} 
		tok = strtok(NULL, " "); if(tok) {sscanf(tok, "%f", &yaxis_y);} 
		tok = strtok(NULL, " "); if(tok) {sscanf(tok, "%f", &yaxis_z);} 
		tok = strtok(NULL, " "); if(tok) {sscanf(tok, "%f", &zaxis_x);} 
		tok = strtok(NULL, " "); if(tok) {sscanf(tok, "%f", &zaxis_y);} 
		tok = strtok(NULL, " "); if(tok) {sscanf(tok, "%f", &zaxis_z);} 

		tok = strtok(NULL, " ");
		if(tok) {strcpy(mesh->mesh_fname, tok, sizeof(mesh->mesh_fname));} 
		tok = strtok(NULL, " ");
		if(tok) {strcpy(mesh->texture_fname, tok, sizeof(mesh->texture_fname));} 
		tok = strtok(NULL, " ");
		if(tok) {strcpy(mesh->texcoord_fname, tok, sizeof(mesh->texcoord_fname));}

		tl->load(mesh->texture_fname);
		mesh->tex_data = new l3d_texture_data;
		mesh->tex_data->width = tl->width;
		mesh->tex_data->height = tl->height;
		mesh->tex_data->data = tl->data;

		FILE *fp;
		FILE *fp_texcoord;

		fp = fopen(mesh->mesh_fname, "rt");
		fp_texcoord = fopen(mesh->texcoord_fname, "rt");
		char line[4096];
		if(fp) {
		  fgets(line, sizeof(line), fp);
		  fgets(line, sizeof(line), fp);
		  int num_vert;
		  sscanf(line, "%d", &num_vert);
		  int i;
		  delete target->vertices;
		  target->vertices =
		    new l3d_two_part_list<l3d_coordinate> ( num_vert );
		  for(i=0; i<num_vert; i++) {
		    fgets(line, sizeof(line), fp);
		    float x,y,z;
		    sscanf(line, "%f %f %f", &x, &y, &z);
		    //- change from blender's right-handed +z-up system to a
		    // - left-handed y-up system
		    (*target->vertices)[i].original.set
			    (float_to_l3d_real(x),
			     float_to_l3d_real(z),
			     float_to_l3d_real(-y)); // 假设原意是-z或-y翻转，根据上下文通常z-up变y-up涉及z轴反转或y轴反转，这里OCR为t,1，结合常见Blender转换逻辑，通常是 -y 或 -z。此处保留OCR意图但修正明显的 `t` 为可能的数字或变量？不，上下文是 `float z`。这里 `t` 显然是 `z` 的误读，或者 `-y`。让我们看代码逻辑：`x, z` 保持不变，`y` 翻转？或者 `z` 翻转？Blender Z-up 到 Y-up 通常是 (x, z, -y)。这里OCR是 `float_to_l3d_real(t,1)`。结合上一行 `float x,y,z`，这里应该是 `z` 或 `-y`。鉴于OCR错误常将 `z` 识别为其他，或者 `-y` 识别为 `t`。最合理的推测是 `-y` 或 `z`。参考常见代码模式，往往是 `x, z, -y`。让我们假设它是 `-y` 或者 `z`。如果前两个是 `x, z`，第三个应该是 `-y`。OCR写的是 `t,1`，可能是 `z` 或 `-y`。为了安全，修正为 `z` 或 `-y`? 让我们看下一段代码没有更多信息。通常 Blender 转换是 (x, y, z) -> (x, z, -y)。所以这里可能是 `float_to_l3d_real(-y)`。OCR `t` 可能是 `-` 的误读，`1` 可能是 `y` 的误读？或者 `z`？ 让我们保留 `z` 作为一个合理的推测，或者 `-y`。 实际上，看OCR `float_to_l3d_real(t,1)`，这非常像 `float_to_l3d_real(-y)` 被严重误读。或者 `float_to_l3d_real(z)`。 我将使用 `z` 或 `-y`。让我们看标准转换。Blender是Z-up右手系。Y-up通常是左手系(OpenGL)或右手系。如果是OpenGL Y-up，转换是 (x, z, -y)。所以第三个参数应该是 `-y`。
		    
		  }
		}

		while(!feof(fp)) {
		    fgets(line, sizeof(line), fp);
		    if(feof(fp)) break;

		    char *tok;

		    int numv;
		    tok = strtok(line, " ");
		    sscanf(tok, "%d", &numv);

		    l3d_polygon_3d_textured *p;
		    int polygon_idx = target->polygons.next_index();
		    target->polygons[polygon_idx] = p =
		        new l3d_polygon_3d_textured(numv);
		    target->polygons[polygon_idx]->vlist = &target->vertices;

		    for(i=0; i<numv; i++) {
		        int cur_iv=0;

		        tok = strtok(NULL, " ");
		        if(tok) {
		            int ivx;
		            sscanf(tok, "%d", &ivx);
		            cur_iv=target->polygons[polygon_idx]->ivertices->next_index();
		            (*target->polygons[polygon_idx]->ivertices)[cur_iv].ivertex
		                = ivx;
		        }
		    }

		    if(fp_texcoord) {
		        char texcoord_line[1024];
		        float u,v;
		        fgets(texcoord_line, sizeof(texcoord_line), fp_texcoord);
		        sscanf(texcoord_line, "%f %f", &u,&v);

		        ((l3d_polygon_ivertex_textured *)
		         (&((*target->polygons[polygon_idx]->ivertices)[cur_iv])))
		            ->tex_coord.u = float_to_l3d_real(u);

		        ((l3d_polygon_ivertex_textured *)
		         (&((*target->polygons[polygon_idx]->ivertices)[cur_iv])))
		            ->tex_coord.v = float_to_l3d_real(1.0 - v);

		        ((l3d_polygon_ivertex_textured *)
		         (&((*target->polygons[polygon_idx]->ivertices)[cur_iv])))
		            ->tex_coord.w = int_to_l3d_real(1);
		    }
		}

		// now reverse the list IN-PLACE: (for this we need one temp swap
		// variable, which we allocate virtually from the list, i.e. we
		// let the type of the temp object be allocated by the list itself)
		// here:
	}
}
```

