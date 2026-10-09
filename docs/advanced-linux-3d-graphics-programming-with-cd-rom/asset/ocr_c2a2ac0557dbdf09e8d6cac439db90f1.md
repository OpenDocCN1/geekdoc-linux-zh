```
void push_polys_to_children
(l3d_halfspace *tree,
l3d_object_clipable_boundable *unsplitt_obj_from_parent);

void make_visibleface_meshes(l3d_halfspace *tree);
void print_stats(l3d_halfspace *tree);
});

#endif
```

# **Listing 5-3: bspree.cc**

```
#include "bspree.h"
#include "halfspace.h"
#include "../object/obound.h"
#include "../object/obound.h"
#include "../object/obound.h"
#include "../qdynamic/plugins/vidmesh/vidmesh.h"
#include "../tool_os/newman.h"

l3d_bspree::~l3d_bspree(void) {
    root = NULL;
}

void l3d_bspree::_recursive_delete_tree(l3d_halfspace *root) {
    if(root) {
        _recursive_delete_tree(root->children[0]);
        _recursive_delete_tree(root->children[1]);
        if(root->object) {
            delete root->object;
        }
    }
}

l3d_bspree::~l3d_bspree(void) {
    _recursive_delete_tree(root);
}

void l3d_bspree::print_stats(l3d_halfspace *tree) {
    static int level = 0;
    level++;
    if(tree) {
        printf("*%sLEVEL %d ", level*2, level*2, "", level);
        if(tree->object) {
            printf("%d polys, obj %p", tree->object->polygons.num_items, tree->object);
        }
        else {
            printf("NO OBJECT (0 polys)");
        }
        printf("*%sleft child:", level*2, level*2, "");
        print_stats(tree->children[0]);
        printf("%s*right child:", level*2, level*2, "");
        print_stats(tree->children[1]);
    }
    level--;
}

void l3d_bspree::compute_for_object(l3d_halfspace *root,
l3d_object_clipable_boundable *rest_of_obj)
{
    static int recurselevel=0;
```