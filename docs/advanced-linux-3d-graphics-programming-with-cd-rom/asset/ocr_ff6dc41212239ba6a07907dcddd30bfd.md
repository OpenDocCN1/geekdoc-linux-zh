```
l3d_real top_y,bottom_y;
int point_on_right=0;
int left_idx,right_idx, top_y_idx, bottom_y_idx;

int clipeleftedge, cliprightedge;
int maxy_upper, iceil_y0, iceil_y1, iceil_y2;

int i;


/*- convenience macro for accessing the vertex coordinates. Notice
/*- that we access the clipped vertex index list (not the original),
/*- and the transformed coordinate (not the original). This means
/*- we draw the clipped version of the transformed polygon.
#define VTX(i) ((*((p_poly->clist)[ ((*p_poly->clip_vertices)[i]).ivertex ])).transformed)

#define XPAD 4
#define YPAD 1
/*-
/*- STEP 1: Find top and bottom vertices
/*-

 top_y = VTX(0).Y;
 top_y_idx = 0;
 bottom_y = top_y;
 bottom_y_idx = top_y_idx;
 for(i=0; i<p_poly->clip_ivertices->num_items; i++) {

   if(VTX(i).Y < top_y) {
     top_y = VTX(i).Y;
     top_y_idx = i;
   }

   if(VTX(i).Y > bottom_y) {
     bottom_y = VTX(i).Y;
     bottom_y_idx = i;
   }
 }

 left_idx = top_y_idx;
 right_idx = top_y_idx;

/*-
/*- STEP 2: Create empty left edge
/*-
 left_x_start = VTX(top_y_idx).X;
 left_y_start = VTX(top_y_idx).Y;
 left_celly_start=iceil(left_y_start);
 left_celly_end=left_celly_start;

/*-
/*- STEP 3: Create empty right edge
/*-
 right_x_start=left_x_start;
 right_y_start=left_y_start;
 right_celly_start=left_celly_start;
 right_celly_end=right_celly_start;

/*-
/*- STEP 4: Loop from top y to bottom y
```