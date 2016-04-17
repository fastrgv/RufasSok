# RufasSok
RufasSok is a minimalistic version of the Sokoban puzzle game for both Mac OS-X and GNU-Linux.

Get full source and binaries in the tar.gz file under releases.


# RufaSok - v2.0.1

## What's new:


**v 2.0.1 - 17apr16**

* Fixed critical error in ./gnulibs/ that prevented LINUX executable from finding needed shared libraries.  Several more softlinks fixed the problem.
* Revised library layout and compile scripts.
* Enhanced portability by using more static libs in gnu/linux compilation;
* All nonstandard libraries are static in OS-X compile script.


**v 2.0 - 22feb16**

* elliminated ksok;  now rufasok combines all options into a single executable.  The various available skins can now be seen by using the (t)-key to pick your favorite.
* added a Mac binary bundle that acts much more like a typical Mac App.  This app is delivered in the installation directory, but could be moved elsewhere, such as your personal Applications directory.  Note that there are some soft [symbolic] links in the bundle that are resolved automatically when copied by the command "cp -r rufaslider.app destination-directory".


**v 1.9 - 12feb16**

* Upgraded the puzzle file loader, which had been hardcoded, but now dynamically searches the ./games/ directory for .sok files.  This means you can add game files without recompiling ksok or rufasok.


**v 1.8 - 14oct15**

 * The command line parameter for ksok now accepts a "4" if you want a pooltable skin.

**v 1.7 - 06oct15**

 * Fixed an error that allowed oversized puzzles.

**v 1.6 - 26jun15**

* replaced previous, inferior ones with a new autosolver called "trbfs".  It is a brute-force reverse breadth-first search with no heuristics and uses a splay tree to store and check for previously seen configurations.  The command line is "trbfs puzzle_file_name max_levels level_number".  The output file (named similarly to the input file) contains directions from the set {u,d,l,r,U,D,L,R}, where upper case indicates a push.  It is size-limited to 17 or fewer boxes, and 128 or fewer interior puzzle positions.

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


## Build Requirements:
* a recent gcc compiler that supports -std=c++11;
* graphics card that supports OpenGL version 3.3 or later;

"ocmp.sh" is the build script for OSX, and "lcmp.sh" is for GNU/Linux.  ccc.sh is the build script for trbfs.  Just type "ccc.sh trbfs" to compile the autosolver on either platform.

If the delivered linux binary does not run, and recompilation fails to create a usable executable, try these...

-------------------------------------------------------
### Steps to compile and run on "other" linux distros.

* Install Cmake...complicated from source, easy using a system update.

* Install SDL2-dev.
	* First, try a system update of libSDL2-devel.
	* Downloading and building from source is the hardest way, but still easy.  Requires Cmake.

* Install SFML-dev.
	* First, try a system update of sfml-dev or libsfml-devel.  
	* Building from source using Cmake is difficult because there are several prerequisites, but if you add them one at a time based on the cmake error messages, it is achievable.

At this point, the delivered compile script is likely to work without mods.

------------------------------------------------

## Running:

Unzip the archive and you will see a new directory appear with a name like bundle+date, that you should rename to something like install_directory.  

Users may then open a terminal window, cd to install_directory, then, at the command line, type the executable name to start the game.  In Linux, you may also double click the icon for rufasok_gnu in file manager.

Mac users note that this game may be initiated in two ways.  First, by opening a terminal, navigating to the install_directory, and typing rufasok_osx on the command line.  Second, by navigating to the installation directory in Finder and clicking the "rufasok.app" icon named "Rufasok".
 

The install_directory should contain subdirectories named "data", "libLocal", "incLocal", "games".


Thus, at the command line type:

	rufasok_gnu ( or rufasok_osx )

rufasok has the following [persistent] commandline skin options:
* 0=gray bkgd
* 1=star bkgd
* 2=water bkgd
* 3=antique desk skin
* 4=pooltable skin
* 5=plain and simple
...although these are no longer needed since the (t)-key now cycles thru the skins.

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
* (z)   = setPoint...subsequent presses of (r)-key restores this configuration
* (t)   = Try next Skin color

Finally, subject to several limitations, typing: "trbfs puzzle-file-name.sok maxlevels level-number" will attempt to solve a particular puzzle for you.  There are many cases this solver cannot handle, but it is pretty good at sovling certain types of puzzles, particularly the more dense ones.  It is not very good at the near-Lishout type, if you know what that means.

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

## LodePNG (png loader module)
lodepng.cpp lodepng.h
are files copyrighted by Lode Vandevenne and so marked
with all the details of their permitted uses 
near the tops of those two files.

