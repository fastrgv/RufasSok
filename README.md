![screenshot](https://github.com/fastrgv/RufasSok/blob/master/rsok.png)

# RufasSok
RufasSok is a minimalistic version of the Sokoban puzzle game for both Mac OS-X and GNU-Linux.

Get full source and binaries in the tar.gz file under releases, or try this link:
https://github.com/fastrgv/RufaSok/releases/download/v2.2.0/asok_20aug2016.tar.gz


# RufaSok - v2.2.0

## What's new:

**v 2.2.0 - 20aug16**

* Converted to Ada with essentially the same functionality.  Of course the build scripts are different.
* Now includes two sokoban solvers, also written in Ada:  puller, ibox.


**v 2.0 - 22feb16**

* added a Mac binary bundle that acts much more like a typical Mac App.  This app is delivered in the installation directory, but could be moved elsewhere, such as your personal Applications directory.  Note that there are some soft [symbolic] links in the bundle that are resolved automatically when copied by the command "cp -r rufasok.app destination-directory".

**v 1.6 - 26jun15**

* added (z) to menu, a keystroke that creates a setpoint (reZero) such that subsequent restarts (r) actually restore this configuration instead of the initial configuration.  Use this when you have made progress but then want to embark on various alternate speculative strategies.

* Within a game session, the current level attempted in each file is now preserved as one moves between files.

-----------------------------------------------------------------

## RufaSok Introduction

This is a minimalistic version of the Sokoban puzzle game.  It uses data in a format that is found on the internet, perhaps requiring a bit of editting.

The beauty of this implementation is that it is fully OpenGL 3.3 core profile, and uses no OpenGL-deprecated functions.

It has few embellishments, but it does have undo (u), restart (r), and setpoint (z) functions.  Each data file has several "levels".  The next (n) and previous (p) keys move between levels.  Bigger (b) and smaller (s) keys help you adjust the size of the window.  The (left-shift) and (right-shift) keys move you to the previous or next puzzle files.  To move the "pusher" use the arrow keys.  The objective is to push all the movable objects onto their targets.

--------------------------------------------
## Features

* uses SDL2;
* works on OS-X Retina displays;
* uses SFML for applause sound;
* all runtime files are in ./data/
* all puzzle files are in ./games/

----------------------------------------------

## what is special about this project?
Uses the Ada programming language and fully modern OpenGL methods.  Achieves version 3.3 core profile contexts, and compiles and runs on both GNU/Linux and Mac OS-X systems.

Focusing on portability and freedom, no coding effort or compromise has been made to accomodate proprietary operating systems.  It relies on a thin SDL2 binding from Dan Vazquez, a thin OpenGL binding from "Lumen", a PNG reader by Stephen Sanguine, and SFML-Audio (because of its elegant audio interface).



## Build Requirements:
* a recent GNAT Ada compiler from AdaLibre;
* graphics card that supports OpenGL version 3.3 or later;

"ocmp.sh" is the build script for OSX, and "lcmp.sh" is for GNU/Linux.  ccc.sh is the build script for the autosolvers puller and ibox.  Just type "ccc.sh puller" or "ccc.sh ibox" to compile on either platform.

If the delivered linux binary does not run, recompile with lcmp.sh.

The Mac binary should run on any recent version of OS-X.  Simply navigate to the install directory in Finder and click on the icon.

------------------------------------------------

## Running:

Unzip the archive and you will see a new directory appear with a name like bundle+date, that you should rename to something like install_directory.  

Users may then open a terminal window, cd to install_directory, then, at the command line, type the executable name to start the game.  In Linux, you may also double click the icon for rufasok_gnu in file manager.

Mac users must navigate to the installation directory in Finder and click the "rufasok.app" icon named "Rufasok".
 

The install_directory should contain subdirectories named "data", "gnulibs", "include", "games", "skins".



asok has the following skin options:
* gray bkgd
* star bkgd
* water bkgd
* antique desk skin
* plain and simple
...the (t)-key now cycles thru the skins.

-----------------------------------------------------------------

Note that the (h) key brings up a help menu that looks like this:

* (esc) = exit
* (u)   = undo last move
* (r)   = restart
* (n)   = next-puzzle in current file
* (p)   = previous-puzzle in current file
* (R-shift) = next-file
* (L-shift) = previous-file
* (b)   = bigger
* (s)   = smaller
* (z)   = reZero (setPoint)...subsequent presses of (r)-key will restore this configuration
* (c)   = next skin Color

Finally, subject to several limitations, typing: "solver-name puzzle-file-name.sok maxlevels level-number" will attempt to solve a particular puzzle for you, where solver-name is either "puller" or "ibox".  There are many cases these solvers cannot handle, but they are pretty good at sovling certain types of puzzles, particularly the more dense ones.

-----------------------------------------------------------------

## Adding Your Own Sokoban Files

Note that the file naming conventions must be maintained now that dynamic file loading is done after reading the ./games/ directory.  No underscores are permitted except one that precedes the integer that indicates the number of levels in the file.  The name format is thus anyname_nnn.sok.  Note that there is a standardized format for the online sokoban files themselves that I have attempted to respect and maintain.



Please send questions or comments to

	fastrgv@gmail.com



RufaSok itself is covered by the GNU GPL v3 as indicated in the sources:


 Copyright (C) 2015  <fastrgv@gmail.com>

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

