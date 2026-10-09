```
cam->VRI_velocity += l3d_mulrr(dot(cam->bounce, cam->VRI),
                            damping_factor);
cam->VUP_velocity += l3d_mulrr(dot(cam->bounce, cam->VUP),
                            damping_factor);

cam->VRP = cam->new_position;

some_collision_occurred = 1;
}

n->next;
}
}

cam->prevent_collision = 0;
l3d_point new_pos_with_portal_displacement
(cam->new_position.X + l3d_mulrr(float_to_l3d_real(5.0),
                                 cam->VFM.X),
 cam->new_position.Y + l3d_mulrr(float_to_l3d_real(5.0),
                                 cam->VFM.Y),
 cam->new_position.Z + l3d_mulrr(float_to_l3d_real(5.0),
                                 cam->VFM.Z),
 int_to_l3d_real(1)),
original_new_pos = cam->new_position;

n = sector->nonculled_polygon_nodes;
while(n) {
   l3d_polygon_3d_portal_collidable *portal;
   
   portal = dynamic_cast<l3d_polygon_3d_portal_collidable *>(n->polygon);
   if(portal) {
      
      cam->new_position = new_pos_with_portal_displacement;
      
      if(cam->detect_collision_with(portal) == 1) {
         current_sector = portal->connected_sector;
         break;
      }
   }
   
   n=n->next;
}

cam->new_position = original_new_pos;
}

n = sector->nonculled_polygon_nodes;
while(n) {
   l3d_polygon_3d_collidable *poly3;
   
   poly3 = dynamic_cast<l3d_polygon_3d_collidable *>(n->polygon);
   if(poly3 && cam) {
      
      if (poly3->plane.side_of_point(cam->VRP) < 0) {
```