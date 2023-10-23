# Resources and Setup

## How to decompile
If you want to help us research the game, and even reverse engineer, you will need the following things:

* Basic C and C++ knowledge
* A disassembler (IDA Pro or Ghidra is recommended)

### Instructions for Ghidra
You will need **[Ghidra 10.3.1](https://github.com/NationalSecurityAgency/ghidra/releases/tag/Ghidra_10.3.1_build)** specifically. An extension is also needed to load PSX binaries, which can be found [here](https://github.com/lab313ru/ghidra_psx_ldr/releases/tag/v6.7). After you have extracted the archive, open Ghidra, navigate to `File -> Install Extensions` in the main menu, and install the extension. Then, restart Ghidra.

## How to extract PAK files
You will need a tool called VibRipper, which can be found in [this GitHub repository](https://github.com/resistiv/VibRipper/), courtesy of Resistiv. To use this tool, the executable will need to be placed in the same folder or directory as the PAK file you want to extract.

After this, run the extract command, `./VibRipper.exe u 01_FILES.PAK EXTRACTED_FILES` for example. (Append `mono` to the beginning in the case of Linux.) In this case, all the extracted files should be in EXTRACTED_FILES. If you wish to edit the files that you extracted, follow the other sections on this page accordingly.




## How to edit TMDs, ANMs, and ANCs
The models and animations can be imported into 3D modeler programs, but there currently isn't a known way to export the models or animations into their respectable file formats. There are two currently known methods to edit models and animations. One uses Blender and the other uses LightWave.

### Blender Instructions
If you want to export the animations on Blender, you can use a tool created by [Murugo](https://github.com/Murugo/), who created a custom addon that can work with Vib-Ribbon's animation and model files; however the plugin was designed for Blender 2.8.x and as such will only work in that version range alone.

For further instructions, visit the [repository for the plugin](https://github.com/Murugo/Misc-Game-Research/tree/main/PS1/Vib-Ribbon).

### LightWave Instructions
(WIP)
It was discovered that LightWave was the tool used to create the original files, so naturally, there are methods to work with the models and animations here as well. You can get LightWave [at this link](https://lightwave3d.com//try_lightwave/).



## How to edit Audio files
There is not a currently known way to edit the audio of Vib-Ribbon, but there will likely be one eventually. Looking at different SDKs will likely have some answers.

### Extracting the audios
This is a simple process, and requires the use of PSound. [You can download PSound by following this link.](https://cdn.discordapp.com/attachments/1141802613231337522/1141803662734274560/PSound.exe). Browse the folders with audio such as `GAME/AUDIO/PSJ_SE.VB`, `KIOSK/AUDIO/PSJ_SE.VB`, or `TITLE/AUDIO/PSJ_SE.VB`. Each piece of audio tends to be played at different speeds because sample rates vary across them. To export, you can convert them as WAV in the File Tab.



## How to edit obstacle data
This one is still in the works... You can help us out by analyzing the `SCRIPT/SYSTEM3.FSL` file! *After extraction, of course.*
