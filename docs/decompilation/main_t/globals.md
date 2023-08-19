Here are some of the globals found in MAIN_T.EXE, the title executable. These globals are saved as 4-byte DWORDS, usually as either values or pointers to game functions, in the console's memory during execution.
### PAL
None yet.

<!---
*Included by PSYQ*
```
printf                 = "0x80030674";  // Print formatted output
exit                   = "0x80030914";  // Terminate a program normally
SwEnterCriticalSection = "0x80030924";  // uppresses interrupts
SwExitCriticalSection  = "0x80030480";  // Enables interrupts
SpuQuit                = "0x80033184";  // Terminates SPU processing
SpuIsTransferCompleted = "0x800330D4";  // Checks whether transfer is completed or waits for completion
InitClip               = "0x80035E1C";  // Initialize clipping parameter
ResetGraph             = "0x8002CDE8";  // Initialize drawing engine
FntFlush               = "0x8002F724";  // Draw contents of print stream
Clip3F                 = "0x80035CAC";  // Three-vertex clipping functions
GsSetProjection        = "0x80035DFC";  // Set the projection plane position
rcos                   = "0x80035F3C";  // Finds the cosine function of the angle
rsin                   = "0x80035FDC";  // Finds the sine function of the angle
HWD0                   = "0x800481E8";  // Horizontal resolution
VWD0                   = "0x800481EC";  // Vertical resolution
```
-->