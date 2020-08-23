# Etch
A simple drawing game for the GameBoy Color.

# Release
Download the latest release [here]()

# Play
GameBoy game file (.gb) is playable in emulators or loaded on a GBC Flash card cartridge.  
Recommended emulators:
 - [BGB](https://bgb.bircd.org/) (Windows only)
 - [googulator](www.googulator.com) (Online only, requires google account)
 - [retroarch](https://www.retroarch.com/index.php)
 - [VisualBoyAdvanced](https://github.com/visualboyadvance-m/visualboyadvance-m/releases/latest)
 
Recommended GBC flash card cartridges:
 - [EZ-Flash Jr](http://www.ezflash.cn/product/ezflash-junior/)

# Build
*Refer the the [GameBoy Builder](https://gamesknightstudios.github.io/GBBuilder/) guide for in-depth details on building and running game boy games in both emulators and cartridges.*

## Setup environment
Build **Etch** from source using [GameBoy Development Kit](https://github.com/Zal0/gbdk-2020/releases/latest) (GBDK).  
Add GBDK's compiler (lcc) to the environment variable.  
In linux set the path variable using the following command:
``` bash
export PATH=PATH_TO_GBDK/bin:$PATH
```
In windows use following instructions:
 - In Search, search for and then select: System (Control Panel)
 - Click the Advanced system settings link.
 - Click Environment Variables. In the section System Variables, find the PATH environment variable and select it. Click Edit. If the PATH environment variable does not exist, click New.
 - In the Edit System Variable (or New System Variable) window, add the directory to the bin folder of GBDK to the list. Click OK. Close all remaining windows by clicking OK.

## Make
There are three approaches to build games with GBDK; make, cmake, or directly calling the GBDK compiler.  
This repository includes a MakeFile and a CMakeLists.txt file that can be used to build it whether you are using make or cmake.
*Note: Expects the GBDK bin directory to be in the PATH environment variable so that lcc is accessible.*

### MakeFile
To build on Linux use the following commands:
``` bash
cd PATH_TO_REPO
make
```
To build on Windows [MinGW](https://www.ics.uci.edu/~pattis/common/handouts/mingweclipse/mingw.html) is recommeded:
```
cd PATH_TO_REPO
mingw32-make -f MakeFile
```
These will build the example game in a folder named 'build'.  
The '.gb' file in this build folder is the gameboy game that has just been compiled. 

### CMake
To build on Linux use the following commands:
``` bash
cd PATH_TO_REPO
mkdir build
cd build
cmake ..
make
```
To build on Windows [MinGW](https://www.ics.uci.edu/~pattis/common/handouts/mingweclipse/mingw.html) is recommeded:
```
cd PATH_TO_REPO
mkdir build
cd build
cmake .. -G "MinGW Makefiles"
mingw32-make
```
These will build the example game in the folder named 'build'.  
The '.gb' file in this build folder is the gameboy game that has just been compiled. 

### Compiler
To build on Linux use:
``` bash
cd PATH_TO_REPO
mkdir build
cd build
lcc -Wa-l -Wl-m -Wl-j -DUSE_SFR_FOR_REG -c -o etch.gb ../src/etch.c
```
To build on Windows use:
```
cd PATH_TO_REPO
mkdir build
cd build
lcc -Wa-l -Wl-m -Wl-j -DUSE_SFR_FOR_REG -c -o etch.gb ..\src\etch.cc
```
This will build the app to a build folder in this repository.  
The '.gb' file in this build folder is the gameboy game that has just been compiled. 

# Installer
Generate a runable emulator of the game on Windows using the following instructions.  
This requires 7-zip to be installed which can be downloaded from [here](https://www.7-zip.org/).  

1. Copy the game file (etch-0.0.1.gb) to the release/Etch folder.
2. Add bgb.exe and game file in this directory to a 7-Zip archive. (Right click -> Add to archive).
3. Copy the resulting file to the release folder
4. Create exe from 7z archive and config on the command line:
```
copy /b 7zSD.sfx + config.txt + Etch-0.0.1-emulator.7z Etch-0.0.1-emulator.exe
```
For a more polished looking application you can use [Resource Hacker](http://www.angusj.com/resourcehacker) to change the icon and meta data. 