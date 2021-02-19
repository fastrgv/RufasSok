![screenshot](https://github.com/fastrgv/RufasSok/blob/master/rsok.png)

# RufasSok
RufasSok is a minimalistic version of the Sokoban puzzle game with embedded autosolvers for Windows, Mac OS-X and GNU-Linux.

Get full source and binaries in the tar.gz file under releases, or try this link:

https://github.com/fastrgv/RufasSok/releases/download/v2.5.1/as20feb21.7z




# RufaSok  using GLFW3, OpenAL audio
-------------------------------------------------------------

## What's new:


**ver 2.5.1 -- 20feb2021**
* Fixed annoying changes of user-set window size/position.
* Upgraded to OpenAL sound.
* Updated autosolvers.
* Added more capable hbox4 autosolver.
* Added visual aid that shows 
	* possible destinations when a box is clicked.
	* possible sources when a goal is clicked.

**See complete revision history at end of file**



-----------------------------------------------------------------

## RufaSok Introduction

This is a minimalistic version of the Sokoban puzzle game with 3 external solvers, and two embedded auto-solvers designed to help you to learn to solve puzzles on your own.

It has undo (u), restart (r), and setpoint (z) functions.  Each data file has several "levels".  The next (n) and previous (p) keys move between levels.  Bigger (f2)-key/(2)-key and smaller (f1)-key/(1)-key  help you proportianally readjust the size of the window.  The (left-shift) and (right-shift) keys move you to the previous or next puzzle files.  To move the "pusher" use the arrow keys, or WASD keys.  The objective is to push all the movable objects onto their targets.  And the embedded solvers help you a little, or a lot, when you get stuck.

--------------------------------------------
## Features

* runs on Windows, OSX(>=10.13,sep2017), Linux;  New linux binary now runs on many linux distros!
* uses GLFW3;
* works on Retina displays;
* uses OpenAL for applause sound;
* all runtime files are in ./data/
* all puzzle files are in ./games/
* includes 3 external autosolvers:  iplr3r, ibox3r, hbox4
* includes 2 embedded autosolvers that help you to learn.

----------------------------------------------
## Embedded Autosolver Function
Two autosolvers are now embedded within this application so that pressing the (=)-key at any time initiates an attempt by the primary solver to solve the present state of the current puzzle within a limited amount of time.  If successful then you will see an onscreen prompt to continue to press the same key to single-step toward the solution.  Otherwise you will see no such prompt.  These embedded solvers are good for small and dense layouts;  but not so good at large, sparse puzzles.

Similarly, the 2nd alternate solver is initiated with the (".")-key.

Thus, you can give yourself a headstart toward a correct solution by limited use of this feature.  Once you think you can solve it yourself, stop using the solver and proceed manually.  This really helps when you cannot see what your next move should be.

Note also that the solvers can tell you when you have gone too far and gotten yourself into a deadlock. If you periodically test to see if a solution is available as you proceed manually, then if you go too far you will suddenly find no solution is available. This means you need to undo (u) until a solution is once again available.

Embedded autosolver failure might imply the present state of the puzzle is impossible to solve, or simply that the autosolver failed due to time constraint, or insufficient capability.

Finally, a single command-line argument (decimal float) specifies a persistent timeout interval to wait for the internal autosolver before giving up.  The default is 10.0 seconds.  A new setting remains in effect until a different setting is specified using a command-line argument.


## External Autosolvers
Remember that there are still three external autosolvers without time constraints.  Subject to several limitations, typing: "solver-name puzzle-file-name.sok maxlevels level-number" will attempt to solve a particular puzzle for you, where solver-name is either "iplr3r" or "ibox3r".  There are many large or sparse [lishout] puzzles the first two solvers cannot handle, but they are pretty good at sovling the small dense ones.  Use the script ccc.sh to compile either solver for your operating system (assuming the presence of an Ada compiler).

The command to build them both [on OSX/linux] is simply:
	ccc[gnu|osx].sh ibox3r
	ccc[gnu|osx].sh iplr3r
	ccc[gnu|osx].sh hbox4

and on Windows:
	ccc.bat ibox3r
	ccc.bat iplr3r
	ccc.bat hbox4

To run type:  [exeName puzzleFile TotalLevels LevelToSolve]

EG on windows type:
	binw64\iplr3r.exe games\pico_22.sok 22 3
	...to solve the 3rd level in file pico_22.sok.

EG on OSX type:
	ibox3r_osx games/pico_22.sok 22 3

EG on Linux type
	hbox4_gnu games/pico_22.sok 22 3

----------------------------------------------

## what is special about this project?

It uses the Ada programming language and modern OpenGL methods, with textures, shaders and uniforms.  Compiles and runs on Windows, GNU/Linux and Mac OSX systems.

Focusing on portability, transparency, and open source freedom, this project relies exclusively on F.O.S.S. tools:  a thin GLFW3 binding, a thin OpenGL binding, a PNG reader by Stephen Sanguine & Dimitry Anisimkov, and a GNAT compiler.

The linux-build is among very few modern OpenGL games where a single pre-built executable can run on multiple Linux distros without 3rd party add-ons!

------------------------------------------------

## Setup & Running:

Mac users see "osx-setup.txt".
Windows users see "windows-setup.txt".

Unzip the archive.  On Windows, 7z [www.7-zip.org] works well for this.

Users may then open a terminal window, cd to install_directory, then, at the command line, type the executable name to start the game.  

----------------------------------------------------------------------
In Linux type "rufasok_gnu" OR you may also double click the icon for rufasok_gnu in file manager.

The distributed linux executable requires glibc v2.14 or newer.  That means if your distribution is older, it might not run, and you will need to recompile.

----------------------------------------------------------------------
Mac users must navigate to the installation directory in Finder and click the "rufasok.app" icon named "Rufasok".

----------------------------------------------------------------------
Windows users type:  "rufasok.bat"
 
----------------------------------------------------------------------

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
* (z)   = reZero (setPoint)...subsequent presses of (r)-key will restore this configuration
* (2,f2) = bigger
* (1,f1) = smaller
* (c)   = next skin Color
* (=)   = try autosolver #1 (iplr3r)
* (.)   = try autosolver #2 (hbox4)
* box-click: possible destinations
* goal-click: possible sources
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

where rufasok can be rufasok_gnu, rufasok_osx or rufasok.bat.

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

"obuildall.sh" builds on OSX, and "lbuildall.sh" is for GNU/Linux.  ccc.sh is the build script for the autosolvers "iplr3r" and "iboxr3".  Just type "ccc.sh iplr3r" or "ccc.sh ibox3r" to compile on any platform, assuming the presence of an Ada compiler.


The Mac binary should run on any recent version of OS-X.  Simply navigate to the install directory in Finder and click on the icon.

-------------------------------------------------------

The distributed linux executable requires glibc v2.14 or newer.  That means if your distribution is older than june 2011, it probably will not run, and you will need to recompile.

If the delivered GNU/Linux binary does not run, try:

* Manually install GNAT GPL from libre.adacore.com/download/.
* Rerun the compile script lcmpd.sh or lcmpd2.sh.

### Fixable Link Problems during linux build:

On a linux build machine, you might have fixable link errors, depending on its configuration.  If, for example, you are missing "libz", you can simply copy "libz.so" from the AdaCore ~/lib/ directory into /usr/local/lib/.  If "libGL" cannot be found, this literally means "libGL.so" was absent.  But you might have "libGL.so.1" present.  In this case, simply create a softlink by changing to the libGL directory, then type the line:

sudo ln -s libGL.so.1 libGL.so  (and enter the admin password)

whence the linker should now be able to find what it wants.  But if there is more than one file libGL.so present on your system, make sure you use the best one;  i.e. the one that represents your accelerated-graphic-driver.





===================================================================
## License

RufaSok itself is covered by the GNU GPL v3 as indicated in the sources:


 Copyright (C) 2021  <fastrgv@gmail.com>

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

**ver 2.5.0 -- 3nov20**
* Greatly simplified build process.

**ver 2.4.2 -- 19sep20**
* Updated all glfw libs to v3.3.2.
* Removed unused linux libraries.
* Included [yet unused] linux sound library with soundloop capability.
* Added on-screen message when setpoint is saved.
* Added "rufasok.bat" for Windows users.
* Made direct ALSA sound the default build for linux.



**ver 2.4.0 -- 04jan20**
* Converted to GLFW3;
* Improved compile scripts;
* Improved key bindings;



**ver 2.3.6 -- 26nov19**

* Repaired a library problem with GNU/Linux build that limited portability.
* No problems with Mac/OSX or M.S. Windows builds.


**ver 2.3.5 -- 25aug19**

* Updated embedded autosolvers.  In particular, the alternate solver is faster but the solutions are non-optimal.
* Fixed embedded solver failures and improved interface behavior.




-------------------------------------------------
RufasSok Autosolver in action:

https://youtu.be/_OKd3MQ8VUQ

-------------------------------------------------


