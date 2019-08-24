![screenshot](https://github.com/fastrgv/RufasSok/blob/master/rsok.png)

# RufasSok
RufasSok is a minimalistic version of the Sokoban puzzle game with embedded autosolvers for Windows, Mac OS-X and GNU-Linux.

Get full source and binaries in the tar.gz file under releases, or try this link:

https://github.com/fastrgv/RufasSok/releases/download/v2.3.5/as25aug19.7z



# RufaSok
-------------------------------------------------------------

## What's new:

**ver 2.3.5 -- 25aug19**

* Updated embedded autosolvers.  In particular, the alternate solver is faster but the solutions are non-optimal.
* Fixed embedded solver failures and improved interface behavior.


**ver 2.3.4 -- 14jul19**

* Updated SDL2 to version 2.0.9;
* Updated Ada binding to SDL2;
* Added user-controlled autosolver timeout;
* Corrected error in single-puzzle commandline test mode;
* Now use 9-key to enlarge, 1-key to shrink window, for better laptop control.


**See complete revision history at end of file**



-----------------------------------------------------------------

## RufaSok Introduction

This is a minimalistic version of the Sokoban puzzle game with 2 external solvers, and two embedded auto-solvers.

It has undo (u), restart (r), and setpoint (z) functions.  Each data file has several "levels".  The next (n) and previous (p) keys move between levels.  Bigger (9)-key and smaller (1)-key  help you adjust the size of the window.  The (left-shift) and (right-shift) keys move you to the previous or next puzzle files.  To move the "pusher" use the arrow keys, or WASD keys.  The objective is to push all the movable objects onto their targets.  And now the (=)-key triggers an embedded solver that helps you when you get stuck.

--------------------------------------------
## Features

* runs on Windows, OSX, Linux;
* uses SDL2;
* works on Retina displays;
* uses SFML for applause sound;
* all runtime files are in ./data/
* all puzzle files are in ./games/
* includes 2 external autosolvers:  ipuller3, ibox3
* includes 2 internal autosolver too.

----------------------------------------------
## Embedded Autosolver Function
Two autosolvers are now embedded within this application so that pressing the (=)-key at any time initiates an attempt by the primary solver to solve the present state of the current puzzle within a limited amount of time.  If successful then you will see an onscreen prompt to continue to press the same key to single-step toward the solution.  Otherwise you will see no such prompt.  These embedded solvers are good for small and dense layouts;  but not so good at large, sparse puzzles.

Similarly, the 2nd alternate solver is initiated with the (".")-key.

Thusly, you can give yourself a headstart toward a correct solution by limited use of this feature.  Once you think you can solve it yourself, stop using the equal-key and proceed manually.  This really helps when you cannot see what your next move should be.

Embedded autosolver failure might imply the present state of the puzzle is impossible to solve, or simply that the autosolver failed due to time constraint, or insufficient capability.

Finally, a single command-line argument (decimal float) specifies a persistent timeout interval to wait for the internal autosolver before giving up.  The default is 10.0 seconds.  A new setting remains in effect until a different setting is specified using a command-line argument.


## External Autosolvers
Remember that there are still two external autosolvers without time constraints.  Subject to several limitations, typing: "solver-name puzzle-file-name.sok maxlevels level-number" will attempt to solve a particular puzzle for you, where solver-name is either "ipuller3" or "ibox3".  There are many large or sparse [lishout] puzzles these solvers cannot handle, but they are pretty good at sovling the small dense ones.  Use the script ccc.sh to compile either solver for your operating system (assuming the presence of an Ada compiler).

The command to build them both [on OSX/linux] is simply:
	ccc[gnu|osx].sh ibox3
	ccc[gnu|osx].sh ipuller3

and on Windows:
	ccc.bat ibox3
	ccc.bat ipuller3

To run type:  [exeName puzzleFile TotalLevels LevelToSolve]

EG on windows type:
	binw32\puller games\pico_22.sok 22 3
	...to solve the 3rd level in file pico_22.sok.

EG on OSX type:
	puller_osx games/pico_22.sok 22 3

----------------------------------------------

## what is special about this project?
It uses the Ada programming language and modern OpenGL methods, with textures, shaders and uniforms.  Compiles and runs on Windows, GNU/Linux and Mac OSX systems.

Focusing on portability, transparency, and open source freedom, this project relies exclusively on F.O.S.S. tools:  a thin SDL2 binding, a thin OpenGL binding, a PNG reader by Stephen Sanguine & Dimitry Anisimkov, SFML-Audio with a homebrew binding, and a GNAT compiler.

------------------------------------------------

## Setup & Running:

Mac users see "osx-setup.txt".
Windows users see "windows-setup.txt".

Unzip the archive.  On Windows, 7z [www.7-zip.org] works well for this.


Users may then open a terminal window, cd to install_directory, then, at the command line, type the executable name to start the game.  In Linux, you may also double click the icon for rufasok_gnu in file manager.

Mac users must navigate to the installation directory in Finder and click the "rufasok.app" icon named "Rufasok".

Windows users type:  binw32\rufasok32.exe.  
 

The install_directory should contain subdirectories named "data", "gnulibs", "include", "games", "skins".

Pusher movement is accomplished using the arrow keys or the WASD keys.

asok has the following skin options:
* gray bkgd
* star bkgd
* water bkgd
* antique desk skin
* plain and simple
...the (c)-key now cycles thru the skins (c=color)

-----------------------------------------------------------------

Note that the (h) key brings up a help menu that looks like this:

* (esc) = exit
* (u)   = undo last move
* (r)   = restart
* (n)   = next-puzzle in current file
* (p)   = previous-puzzle in current file
* (R-shift) = next-file
* (L-shift) = previous-file
* (9)   = bigger
* (1)   = smaller
* (z)   = reZero (setPoint)...subsequent presses of (r)-key will restore this configuration
* (c)   = next skin Color
* (=)   = try autosolver #1
* (.)   = try autosolver #2
-----------------------------------------------------------------

Linux Note:  a "mouse" or "sloppy" window focus policy might allow
	window focus to slip away while changing puzzles.  In this case,
	simply move the cursor back onto the puzzle window.  This
	annoyance does NOT occur with a "click" policy.

-----------------------------------------------------------------

## Adding Your Own Sokoban Files

Note that the file naming conventions must be maintained now that dynamic file loading is done after reading the ./games/ directory.  No underscores are permitted except one that precedes the integer that indicates the number of levels in the file.  The name format is thus anyname_nnn.sok.  Note that there is a standardized format for the online sokoban files themselves that I have attempted to respect and maintain.

Note also that a specific sokoban file may be tested by naming it on the terminal window command line with the following syntax:

	rufasok sokfilepath maxlevels startlevel

where rufasok can be rufasok_gnu, rufasok_osx or rufasok.exe.

For example on linux you could type

	"rufasok_gnu games/original_50.sok 50 2"

to tackle level 2 from the original_50 sokoban file.  In this single-file mode, you can still use the next-level(n) & previous-level(p) keys, however, the next/previous files (R-shift/L-shift) keys are disabled.








## Build Requirements:
* a recent GNAT Ada compiler from AdaLibre;
* graphics card that supports OpenGL version 3.3 or later;
* Xcode g++ compiler, if using OS-X

## Build instructions:

**msWin32** => wbuildall.bat

Note that the above windows built scripts might need to be adjusted to reference your actual installation directory for 32bit AdaCore 2017 compiler.

-------------------------------------------------------

"obuildall.sh" builds on OSX, and "lbuildall.sh" is for GNU/Linux.  ccc.sh is the build script for the autosolvers "ipuller3" and "ibox3".  Just type "ccc.sh ipuller3" or "ccc.sh ibox3" to compile on any platform, assuming the presence of an Ada compiler.


The Mac binary should run on any recent version of OS-X.  Simply navigate to the install directory in Finder and click on the icon.

If the delivered GNU/Linux binary does not run, try:

* Manually install GNAT GPL from libre.adacore.com/download/.
* Rerun the compile script lcmpd.sh or lcmpd2.sh.

### Fixable Link Problems during linux build:

On a linux build machine, you might have fixable link errors, depending on its configuration.  If you are missing "libz", you can simply copy "libz.so" from /usr/gnat/lib/gps/ into /usr/local/lib/.  If "libGL" cannot be found, this literally means "libGL.so" was absent.  But you might have "libGL.so.1" present.  In this case, simply create a softlink by changing to the libGL directory, then type the line:

sudo ln -s libGL.so.1 libGL.so  (and enter the admin password)

whence the linker should now be able to find what it wants.  But if there is more than one file libGL.so present on your system, make sure you use the best one;  i.e. the one that represents your accelerated-graphic-driver.






===================================================================
## legal mumbo jumbo:

RufaSok itself is covered by the GNU GPL v3 as indicated in the sources:


 Copyright (C) 2017  <fastrgv@gmail.com>

 This program is free software: you can redistribute it and/or modify
 it under the terms of the GNU General Public License as published by
 the Free Software Foundation, either version 3 of the License, or
 (at your option) any later version.

 This program is distributed in the hope that it will be useful,
 but WITHOUT ANY WARRANTY; without even the implied warranty of
 MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 GNU General Public License for more details.

 You may read the full text of the GNU General Public License
 at <http://www.gnu.org/licenses/>.

-------------------------------------------------


## Revision History:

**ver 2.3.3 -- 16jun19**

* Improved window resize & reposition code.
* Improved autosolvers for more robustness.
* Separate, more readable help screen.
* Autosolver #2 now accessed using "." key, which is universally available on laptops, etc.


**ver 2.3.2 -- 17feb19**

* Added closeWindow handler;
* Fixed window resize errors;
* Fixed font sizing errors;


**ver 2.3.1 -- 30dec18**

* Updated to SDL2 v2.0.8 (all 3 platforms);


**ver 2.3.0 -- 25nov18**

* Now using sdl v207 uniformly (all platforms);
* Now using sfml v250 uniformly (all platforms);
* Updated all sokoban solvers to favor robustness & good solutions;


**ver 2.2.9 -- 08jul18**

* Updated to using SDL v2.0.7;
* Corrected code to handle DOS-formatted resume & puzzle files.


**ver 2.2.8 -- 04jul18**

* Added & improved 2nd built-in solver initiated with numeric-keypad "=" key.  This might solve problems that stump the 1st solver [using the normal keyboard "=" key].  [Not accessible on laptops?]
* Added a "Solution not found" message when a built-in solver fails within 10 seconds.
* Updated AdaPngLib, AdaZLib;
* Put Windows DLLs, EXEs into ./binw32/


**ver 2.2.7 -- 1apr18**

* Now using intrinsic/robust Exists() function;
* Uninverted font file;
* Improved function names in matutils;
* Too many undos no longer aborts;
* Added GPR build scripts;
* Improved & simplified OSX build;


**ver 2.2.6 -- 5nov17**

* Win32 executable now included (built on Windows-10);
* Now supports MSwin32 builds by adding DLLs and libs;
* Improved compilation scripts;
* Added sdl "pumpevents" where needed;
* Corrected logic inside equal-key handler;


**ver 2.2.5 -- 4jul17**

* Updated linux scripts to use a) SFML v2.4.2;  b) AdaCore 2017;
* Added linux script lcmp16.sh for AdaCore 2016 and earlier;
* Note that AdaCore 2017 works on OS-X with no changes;
* Added startup messages listing OGL profile & version;
* Improved keyboard response;


**v2.2.4 - 02may17**

* Added step countdown during solve.
* Made corrections to autosolvers.


**v2.2.4 - 23apr17**

* Puzzle files are now sorted alphabetically for intuitive navigation.
* An autosolver is now embedded within this application so that pressing the "=" key at any time initiates an attempt to solve the present state of the current puzzle.  See extended description below.


**v2.2.3 - 18apr17**

* Now saves the complete game state on exit so that your progress through the levels of each puzzle file will be preserved.
* Also includes precompiled solvers for each platform.


**v2.2.2 - 9apr17**

* Improved error checking in shader package;
* Removed OpenGL-deprecated functions that could cause aborts;
* Revised directory structure, simplified codes;
* Added screen output of push-count, move-count.


**v 2.2.1 - 5jan17**

* Now used improved SFML interface binding.
* Added WASD keys for movement as alternates for the arrow keys.


**v 2.2.0 - 20aug16**

* Converted to Ada with essentially the same functionality.  Of course the build scripts are different.
* Now includes two sokoban solvers, also written in Ada:  puller, ibox.


**v 2.0 - 22feb16**

* added a Mac binary bundle that acts much more like a typical Mac App.  This app is delivered in the installation directory, but could be moved elsewhere, such as your personal Applications directory.  Note that there are some soft [symbolic] links in the bundle that are resolved automatically when copied by the command "cp -r rufasok.app destination-directory".

**v 1.6 - 26jun15**

* added (z) to menu, a keystroke that creates a setpoint (reZero) such that subsequent restarts (r) actually restore this configuration instead of the initial configuration.  Use this when you have made progress but then want to embark on various alternate speculative strategies.
* Within a game session, the current level attempted in each file is now preserved as one moves between files.


-------------------------------------------------
RufasSok Autosolver in action:

https://youtu.be/_OKd3MQ8VUQ

-------------------------------------------------


