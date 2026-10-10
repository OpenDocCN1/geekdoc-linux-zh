# # Signals

# APPENDIX F

Every event received from a hardware device, as the result of some action by the user, is capable of signaling the application program by making a call to a callback function. Table F-1 lists the classes that have signals, the names of the signals, and the prototypes for their corresponding callback functions.

All callback functions have at least two arguments, but they may have more. The first argument is always a pointer to the widget that issues the signal. The last argument is always the pointer that the application program passes to the function to register the callback with the widget. Some callback functions have other arguments; these arguments are included between the widget pointer and the data pointer.