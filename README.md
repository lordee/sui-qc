# SUI Template for FTEQW
SUI is a simple QuakeC (MenuQC) UI system for FTE QuakeWorld game engine.

This repository includes a working empty template with SUI already set up with a decent project structure already using Menu QC and CS QC.

Source code for SUI itself can be found in `src/sui_sys.qc` and its usage can be found `src/m_main.qc` for example.

You need FTEQCC (FTE QuakeC Compiler) to compile the source, and FTE QuakeWorld engine to run it.

## Key goals

SUI makes it easier to draw more user interfaces that games typically need, with things like scrollable views, text inputs, sliders, drag and drop elements, etc. 

SUI is meant to be operated in a very imperative manner, there no objects in the menu system, no class hierarchy. SUI itself doesn't do state management for UI, to display menus you draw them per frame and to remove elements you just stop drawing them. It does some magic to connect user actions like clicks and keypresses to your elements and then you bind the elements that need state (what position a slider is in?) to the data (a state object passed as a pointer into menu draw routines, globals, whatever you want).

SUI provides a pseudo windowing system called framing to make it easier to group and align elements. Frames are pushed into a stack and any sui draws done inside a frame will use that frame's position/size to determine placement. This combined with the aligning system makes for a fairly powerful tool for creating the layouts you need. Example:
```
// Let's assume the draw area is from [0, 0] to [640, 480]
vector SCREEN_SIZE = [640, 480];

void() draw_our_frame =
{
  // Sets Horizontal align to center, sets Vertical align to center.
  sui_set_align([SUI_ALIGN_CENTER, SUI_ALIGN_CENTER]); 
  // Create a new frame in the dead center of the screen with 0, 0 (because of previous align), with size 100*100
  sui_push_frame([0, 0], [100, 100]);
  // Set align to top left corner (of our current frame)
  sui_set_align([SUI_ALIGN_START, SUI_ALIGN_START]);
  // Draw a red box in the top-left corner of the frame, which is at screen_center - frame_size * 0.5
  sui_fill([0, 0], [50, 50], [1.0, 0, 0], 1.0, 0);
  // Done with this frame. We could do more frames inside frames and the transforms would stack.
  sui_pop_frame();
};
```

## Documentation

To be done.
