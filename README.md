Recitation 9: Solutions
-----

1) GDB informs us that we received a `SIGSEGV` (segmentation fault) at line 29, calling the insert method (give credit if the student answers any line number that corresponds to a call to the insert() method). This is because the insert method is being called recursively for 100000 times and this causes stack overflow because of the number of frames for each recursive call that have to be pushed on to the stack. 100000 frames is way above the limit as the calculation in 2) shows. Once the stack is used up, the method attempts to deference an address outside the program space (due to overflow) and this results in the segmentation fault.

2) The stack size is `8192KB`. The insert function creates a 100 char array every time, so this will take up 100B. On top of this, we have two arguments that are pointers for every stack frame. This is an additional 2 * 8B = 16B per frame. Inside every function, we also create a new head pointer (head, not to be confused with headp). This is an additional 8B per frame. The return address of a function is pushed onto the stack as well. On a 64-bit machine, addresses are 8B. We also need to account for the fact that we will push the previous stack base pointer, so that's another 8B. 

 So, our answer is `8192 KB/ (100B + 16B + 8B + 16B) = 8192KB/(140B) = 58514`, which is pretty close to our actual 58224 recursive calls. If the students calculate a stack frame size anywhere between 120B and 140B, give that full credit.
