Grab the latest version of this script from [my github](https://github.com/peon2/memory-watcher).

# Memory Watcher

A simple Memory Watching tool for use with FBNEO or MAME.\
**WARNING**: This script tends to crash due to memory issues!

This script can be run stand-alone or as an addon to the [fbneo-training-mode](https://github.com/peon2/fbneo-training-mode).

This script has seven basic operations.

**N.B. USE ENTER TO FINISH AN INPUT STREAM**

## OPERATIONS
~~~
INIT      -  Start Reading Memory, takes 3 inputs, Start Address, End Address, and Word Size.
CMP       -  Sets the operation used to compare Memory (described below).
STEP      -  Steps through the Memory *once* and compares the values using the CMP operation set. Each Step saves to history, allowing it to be undone (default history of 3)
AUTO STEP -  Steps through the Memory for as long as the Key is held down using the CMP operation set. Does not save to history.
UNDO      -  Deletes the current Memory and replaces it with the previous Memory, undoing the previous CMP.
CONFIG    -  Rebind all of the Keys.
DUMP      -  Dumps all of the active addresses to a file named memory.txt

Defaults to "ICSAUCD" in order.
~~~
## MEMORY

For each Address of Memory, four values are tracked for the user:
~~~
 Address        -> Address of Memory
 Value          -> Value of Memory when Stepping
 Starting Value -> Value of Memory when Memory Watch began
 Active Status  -> Whether or not this Address should be ignored.
~~~

Active Status is an unseen value which tracks if a piece of memory has failed the compare operation chosen. \
If Memory has been marked Inactive, it will no longer display to the user, nor be displayed as part of the live count of active addresses. \
Once an address has been marked Inactive, the only way to reactivate it is with UNDO or by starting a new memory watch with INIT.


In addition, a Memory History is kept, which can be accessed with UNDO, be warned, there is no REDO operation at this time.
## COMPARE OPERATIONS
~~~

Input these using the CMP Operation

EQ	- Equals                 -> True if the current value equals the previous value.
IS	- Is                     -> True if the current value equals a given constant.
EQS	- Equals Starting        -> True if the current value equals the starting value of memory.
NE	- Not Equals             -> True if the current values doesn't equal the previous value.
NES	- Not Equals Starting    -> True if the current value doesn't equal the starting value.
LT 	- Less Than              -> True if the current value is less than a given constant.
LTE	- Less Than or Equals    -> True if the current value is less than or equals a given constant.
LTS	- Less Than Starting     -> True if the current value is less than the starting value.
GT 	- Greater Than           -> True if the current value is greater than a given constant.
GTE	- Greater Than or Equals -> True if the current value is greater than or equals a given constant.
GTS	- Greater Than Starting  -> True if the current value is greater than the starting value.
DE 	- Decreased              -> True if the current value is less than the previous value.
DEE	- Decreased or Equals    -> True if the current value is less than or equals the previous value.
INC	- Increased              -> True if the current value is greater than the previous value.
INE	- Increased or Equal     -> True if the current value is greater than or equal to the previous value.
~~~
# CONSTANTS

A number of constants are defined at the top of the file, the user is encouraged to edit these to their preference.
~~~
MEMORY_HISTORY_MAX    -  How many times UNDO can be used in a row.
XOFFSET               -  Defines where the text is drawn on the X axis.
YOFFSET               -  Defines where the text is drawn on the Y axis.
DISPLAY_COUNT         -  How many addresses to display in live-tracking.
MEMORY_OUTPUT_FORMAT  -  String for formatting, outputs address, then memory value, then starting value. Used to print out to console and memory dump.
DEFAULT_MEMORY_START  -  Default Memory Start Value
DEFAULT_MEMORY_SIZE   -  Default Amount of Memory to scan at one time.
DEFAULT_WORD_SIZE     -  Default Word Size (1, 2, or 4).
DUMP_FILE             -  File to dump memory to.
DEFAULT_KEYS          -  Default Keys used to control the Base Operations.
~~~
