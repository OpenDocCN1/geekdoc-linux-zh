```
```
  fputc( 10, stdout );
  fprintf( stdout, "255" ); fputc( 10, stdout );

  /* Main ray-line sweep-loop (camera emulation) */
  Scale.y = 1.0;
  for( sy = 0; sy < HEIGHT; sy++ ) {
    Scale.z = ((double)(HEIGHT/2.0-sy))/(double)HEIGHT;
    for( sx = 0; sx < WIDTH; sx++ ) {
      Scale.x = ((double)(sx-WIDTH/2))/(double)WIDTH;

      /* Calculate line-direction (from camera-center
         through a pixel)
      */
      Lind.x = Cameraright.x*Scale.x + Cameradir.x*
               Scale.y + Cameraup.x*Scale.z;
      Lind.y = Cameraright.y*Scale.x + Cameradir.y*
               Scale.y + Cameraup.y*Scale.z;
      Lind.z = Cameraright.z*Scale.x + Cameradir.z*
               Scale.y + Cameraup.z*Scale.z;

      /* Get color for pixel */
      #if (DISTLEVELS > 0)
        PixColor.x = PixColor.y = PixColor.z = 0.0;
        for( i = 0; i < DISTRIB; i++ ) {
          DistribVector( &D, &Lind, 0.5/(double)WIDTH,
                        0.5/(double)HEIGHT);
          Lind2 = Lind; Lind2.x += D.x; Lind2.y += D.y;
          Lind2.z += D.z;
          TraceLine( &CameraPos, &Lind2, &Col, MAXREC );
          PixColor.x += Col.x;
          PixColor.y += Col.y;
          PixColor.z += Col.z;
        }
        ScaleVector( &PixColor, 1.0/DISTRIB );
      #else
        TraceLine( &CameraPos, &Lind, &PixColor, MAXREC );
      #endif

      /* Write colors to stdout */
      fputc( (UBYTE)(PixColor.x*255.0), stdout);
      fputc( (UBYTE)(PixColor.y*255.0), stdout);
      fputc( (UBYTE)(PixColor.z*255.0), stdout);
    }

    return 0;
  }
```
```