# General Info
*Written by [polyproxy](https://github.com/polybiusproxy)*

It is well known that Vib-Ribbon's main gimmick was that you could swap out the original PlayStation game disc with your own CDs and the game would generate levels out of the CD's audio tracks.<br>
For this reason, the game had to be small enough to fit in the PlayStation's tiny RAM (2 MB)<br>

In order to do this, the game is separated in four executables, **SCPS_180.12**, **MAIN_T.EXE**, **MAIN_K.EXE** and **MAIN_G.EXE**.<br>
According to the PsyQ SDK, these executables are internally called **modules**.

## SCPS_180.12

**SCPS_180.12** (named **SCES_028.73** on the PAL release, **loader.exe** on the PlayStation Magazine demo) is the main executable ran when the Vib-Ribbon disc is inserted (first boot).

This executable, when ran, searches for the executable to run on an array (**MAIN_T.EXE** by default), searches for it on the disc, and then runs it. When said executable finishes execution, control is passed back to **SCPS_180.12**, which then runs the next executable on the array.

## MAIN_T.EXE

**MAIN_T.EXE** is the executable in charge of the title screen.

The **T** suffix stands for **TITLE**.

## MAIN_K.EXE

**MAIN_K.EXE** is the executable in charge of the `HOW TO PLAY` level.

The **K** suffix stands for **KIOSK**. It is not known what `KIOSK` means in this case.

## MAIN_G.EXE

**MAIN_G.EXE** is the executable in charge of the game's main menu (the course selection, high scores, settings) and gameplay.

The **G** suffix stands for **GAME**.