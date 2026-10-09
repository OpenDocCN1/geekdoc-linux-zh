```
Xflush(dpy);

usleep(250000);
usleep(250000);
usleep(250000);
usleep(250000);

int num_mesh_vertices;
vectorvertex> mesh_vertices;
fprintf(blender_work_fname, "*s/\n",
  config->blender_path_c_str(),
  config->blender_work_filename_c_str());
fp = fopen(blender_work_fname, "rt");
fgets(line, sizeof(line), fp);
fgets(line, sizeof(line), fp);
sscanf(line, "%d", &num_mesh_vertices);
for(i=0; i<num_mesh_vertices; i++) {
  vertex v;
  fgets(line, sizeof(line), fp);
  sscanf(line, "%f %f %f",
    &v.x,
    &v.y,
    &v.z);
  mesh_vertices.push_back(v);
}

int found_overlapping_face;
int face_num;
face_num = 0;
while(!feof(fp)) {
  fgets(line, sizeof(line), fp);
  if(feof(fp)) break;

  int selface;
  char orig_line[4096];
  strncpy(orig_line, line, sizeof(orig_line));
  for(selface=0; selface<num_selected_faces; selface++) {
    strncpy(line, orig_line, sizeof(line));

    char *tok;
    tok = strtok(line, " ");

    int num_v;
    int iv;
    int ivertex;
    num_m;
    int found_overlapping_vertex;
    for(iv=0; iv<num_v; iv++) {
      tok = strtok(NULL, " ");
      int ivertex;
      sscanf(tok, "%d", &ivertex);

      found_overlapping_vertex = 0;
      int fv;
      for(fv=1; fv<selected_faces[selfface][0]; fv++) {
        if ( mesh_vertices[ivertex] ==
             face_vertices[selected_faces[selfface][fv]] )
        {
          found_overlapping_vertex = 1;
          break;
```