# File Extraction
*Written by ILovezCartoonz, aka ILC-YTP*

[Click here to access the original gist](https://gist.github.com/ILC-YTP/e3700d685482552c515eebc9323ec92b)

This is a guide on how to extract files from Vib-Ribbon. It'll also go over how to repackage files, letting you mod the game.
Do note that this guide is based on using Windows, but you should still be able to do everything on Linux with a few adjustments.
You'll also need some knowledge on how to navigate CMD/Powershell, or whatever terminal you use.


## Extracting From BIN/ISO file
You'll need: 
- A copy of Vib-Ribbon on your computer.
- A program that can read and extract files from the "disc." Any program that can extract files from a bin or iso file is fine, but if you wanna rebuild the iso/bin file for later, consider using DUMPSXISO, which comes included with [MKPSXISO](https://github.com/Lameguy64/mkpsxiso).
  
 Run through CMD/Powershell, and remember to add `-s whateverfilename.xml` to set it up to recompile itself as a bin/iso file later on. EX: ``dumpsxiso -s rebuild.xml "Vib-Ribbon (Europe) (En,Fr,De,Es,It) (Track 1).bin"``


## Extracting PAK files
You'll need [VibRipper](https://github.com/resistiv/VibRipper). There's no GUI for the program, it can only be run from a CMD or Powershell window. Basically, when you find a pak file you wanna extract, paste the program into where the pak file is, open a CMD/powershell window, and then enter the command to extract the pak file. EX: ``vibripper u FILES.PAK FILES_EXT``  More info can be found on the github page

PAL NOTE: The PAL version of the game has a bunch of pak files that are basically the same, only with some models and text changes for the different languages. 01_FILES = Japan


## Models (TMD)
There does exist a Vibri model on the models resource website to [download](https://models-resource.com/playstation/vibribbon/). But, if you don't like how it was compiled, or if you wish to make your own version/rig, or if you wanna mess with animations, continue reading this section.

If you're using blender then consider [this blender plugin](https://github.com/Murugo/Misc-Game-Research/tree/main/PS1/Vib-Ribbon). You can easily port the models in, as well as all the animations and camera angles/animations. It's as accurate as you can get, and what I recommend even if you don't wanna use blender for your purpose, since you can then export the result to whatever you need. Instructions on how to install are listed on the page. If for some reason the addon fails to work correctly, uninstall it, open the zip file and delete the readutil file and replace it with [this folder](https://cdn.discordapp.com/attachments/939246273423355908/1001254517070888980/readutil.zip).

However, if you insist on not using blender, [TMD2LWO](https://zophar.net/utilities/psxutil/tmd2lwo.html) and a program that can read LWO (LightWave Objects) files will be needed. Use TMD2LWO the same way as Vib-Ripper was used. EX: ``TMD2LWO.EXE MODEL.TMD WORM``


## Animations (ANM and ANC)
ANM are character/model animation files, while ANC are camera animation files. You can port them through blender with the addon mentioned above. Just make sure you select the whole model before importing the character animations.


## Images/Textures (TIM)
TIM files are the texture files. Vib-Ribbon only uses textures during start-up, with the "Sony Computer Entertainment inc. Presents" text and NanaOn-Sha logo. On PAL, there is another texture that replaces the "SCE INC" screen, making it go unused. [TIM2VIEW](https://github.com/lab313ru/tim2view) allows you to view TIM files, export them as PNGs and replace textures. When editing the extracted PNGs, you'll need to use an image editor that'll export the images with the same color palette and bit depth, or else reimporting the images back to TIM2VIEW will mess with the colors.

I used [GIMP](https://www.gimp.org/) and it worked well for editing and exporting the textures. Use the Palette and Colormap windows to edit colors. When you wanna export, make sure Save resolution, Save Color Profile and Automatic Pixelformat are set before exporting the images. To replace an image, simply import the image to TIM2VIEW while on the same tab of the TIM you wanna replace. Once imported, the texture contained in the TIM file will automatically get replaced and overwritten.

Do note that the color pallete will remain the same, and you'll need to edit each color one at a time from the program. Best to keep the amount of colors you use small if you don't want the process to be long and tedious. 


## AUDIO (VB and VH)
Use [PSound](https://www.romhacking.net/utilities/679/) [(ALT VERSION)](https://www.zophar.net/utilities/psxutil/psound-soundreaver2.html). VB files contain all the audio clips. VH has audio header data. Can extract audio, but currently no known way to replace audio. Read more about VAB audio [here.](https://wiki.xentax.com/index.php/VAB_Audio) <!-- Consider removing this last sentence when vb-vh.md is finished -->


## Rebuilding PAK files
When unpacking PAK files, VibRipper will make a text file that'll be needed to make a pak file. EX: ``vibripper r 01_FILES_EXT 01_FILES.PAK_TOC.txt`` Make sure to back up the pak file before repacking just in case it doesn't get overwritten and potentially lose progress or waste time trying to get a new one.


## Making a BIN/ISO file
Earlier, I mentioned MKPSXISO, which is what we'll be using to make the bin/iso file. We'll use the xml file DUMPSXISO created earlier. Simply run the program through CMD and specify the xml file. EX: ``mkpsxiso.exe rebuild.xml``  You'll get a new bin+cue file named mkpsxiso.bin/.cue. Consider editing the xml file to change the name of the bin+cue file names. Also consider editing the .cue file if you want to include your own custom music tracks in the game.
