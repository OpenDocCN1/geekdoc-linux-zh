```
mouseDown = false;
 x1 = y1 = x2 = y2 = 0;
 cOwner = owner; // Remember who owns this object
}

// Erase window's canvas and lines vector
void TCanvasPane::Clear()
{
 vCanvasPane::Clear(); // Call ancestor function
 lines.erase(lines.begin(), lines.end());
 cOwner->UpdateNumLines(lines.size()); // Update Status bar
}

// Respond to mouse button click event
// Prepares for drawing the next line
void TCanvasPane::MouseDown(int x, int y, int button)
{
 mouseDown = true; // Set mouse down flag
 x1 = x; // Remember starting location
 y1 = y;
 x2 = x1; // Set end point == beginning
 y2 = y1; // as a "do nothing" flag
 cOwner->UpdateMouseInfo(x, y); // Update status bar
}

// Respond to mouse button release event
// Save current line in the lines vector
void TCanvasPane::MouseUp(int x, int y, int button)
{
 mouseDown = false; // Reset mouse down flag
 if (x1 != x2 || y1 != y2) {
 DrawRubberLine(x1, y1, x2, y2); // Erase old line
 x2 = x; // Save line end point
 y2 = y;
 DrawLine(x1, y1, x2, y2); // Draw fixed line
 lines.push_back(TLine(GetPen(), x1, y1, x2, y2));
 // Update status bar information
 cOwner->UpdateMouseInfo(x, y);
 cOwner->UpdateNumLines(lines.size());
 }
}

// Respond to mouse movement button-down event
// Draws a "rubber line" (i.e. an erasable line)
void TCanvasPane::MouseMove(int x, int y, int button)
{
 if (mouseDown) {
 if (x1 != x2 || y1 != y2)
 DrawRubberLine(x1, y1, x2, y2); // Erase old line
 x2 = x; // Save line end point so far
 y2 = y;
 DrawRubberLine(x1, y1, x2, y2); // Draw new line
 }
 // Update status bar information
 cOwner->UpdateMouseInfo(x, y);
```