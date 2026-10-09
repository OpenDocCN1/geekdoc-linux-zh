```
if (right_cell_end > ysize) right_cell_end = ysize;

// - STEP 7: Loop until left and/or right edge is finished
//
while ( ( scanline < left_cell_end) && (scanline < right_cell_end) ) {
   if(! first_scanline_done) {
      first_scanline_done = 1;
   }

   int top_pad;
   top_pad = scanline - yPAD;
   if(top_pad < 0) top_pad = 0;
   int target = scanline;

   for(scanline=top_pad ; scanline < target; scanline++) {

      clipleftedge = ifloor(left_x)-xPAD;

      clipleftedge = (clipleftedge < 0) ? 0 : clipleftedge;
      cliprightedge = iceil(right_x)*xPAD;

      cliprightedge = (cliprightedge > xsize-1) ? xsize-1 : cliprightedge;

      int lumeI_x = clipleftedge;
      for(register char unsigned *pix =
            &address_of_point(clipleftedge,
            SW_RAST_Y_REVERSAL(ysize,scanline));

            pix <= &address_of_point(cliprightedge, scanline);
            lumeI_x++) {
         {
            int light_value = compute_light_level(lumeI_x, scanline);

            light_value += *pix;
            if(light_value > 255) light_value = 255;
            draw_point_at_padress(&pix, light_value);
         }
      }

      left_x+= left_dx;
      right_x+= right_dx;
   }
}

clipleftedge = ifloor(left_x)-xPAD;

clipleftedge = (clipleftedge < 0) ? 0 : clipleftedge;
cliprightedge = iceil(right_x)*xPAD;

cliprightedge = (cliprightedge > xsize-1) ? xsize-1 : cliprightedge;
{
// - - STEP 8: Draw horizontal span
//
int lumeI_x = clipleftedge;
for(register char unsigned *pix =
```

TEAM LIN G - Live, Informative, Non-cost and Genuine!