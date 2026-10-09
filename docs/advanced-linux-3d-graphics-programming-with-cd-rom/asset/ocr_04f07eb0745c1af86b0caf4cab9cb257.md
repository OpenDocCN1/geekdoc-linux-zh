```
int next_ivtx = poly->next_clipidx_right
			(ivtx, poly->clip_ivertices, num_items);
13d_point b =
	("*"poly->vlst)[("*"poly->clip_ivertices)[next_ivtx].ivertex].transformed;

13d_point p = new_position;
13d_vector c = p - a;
13d_vector V = normalized(b-a);
13d_real d = 13d_sqrt(dot(b-a,b-a));
13d_real t = dot(V,c);

13d_point pt;

if(t<0) {
	pt = a;
}else if(t>d) {
	pt = b;
}else {
	pt = a + V*t;
}

13d_real temp_dist;
temp_dist = 13d_sqrt(dot(pt-new_position,
					pt-new_position));
if(temp_dist <smallest_dist) {
	
	smallest_dist = temp_dist;
	nearest_point = pt;
}

if( smallest_dist < collision_sphere_radius) {
	bounce_set
	(13d_mulrr(poly->plane.a,
			collision_sphere_radius - dist + EPSILON_COLLISION),
	13d_mulrr(poly->plane.b,
			collision_sphere_radius - dist + EPSILON_COLLISION),
	13d_mulrr(poly->plane.c,
			collision_sphere_radius - dist + EPSILON_COLLISION),
	int_to_13d_real(0));
	if(prevent_collision) {
		new_position = new_position + bounce;
	}

	return 2;
}

}else return 0;
}
else return 0;
}
return 0;
}else if ((sphere = dynamic_cast<13d_collidable_sphere *>(target))) {
	int result = 0;
```