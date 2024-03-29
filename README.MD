# Attention

You should be using [QSS-M](https://qssm.quakeone.com/) instead. [I assisted in porting it to Apple Silicon](https://github.com/timbergeron/QSS-M/pull/15) and QSS-M supports all the same features of Quakespasm and more.

The original README.MD for this project is retained below for historical purposes.

## Original README.MD
## Quakespasm on Apple Silicon

This project builds [Quakespasm](http://quakespasm.sourceforge.net/), a Quake engine source port, on Apple Silicon hosts for Apple Silicon targets.

It is forked from the [official Quakespasm SourceForge repository](https://sourceforge.net/p/fteqw/code/HEAD/tree/trunk/) circa 065c15.

## Building
Currently, building requires [homebrew](https://brew.sh/), a macOS package manager. Install it if you don't have it already.
```
git clone https://github.com/BryanHaley/Quakespasm-AppleSilicon.git
cd Quakespasm-AppleSilicon/AppleSilicon
make brew_install_tools
make distributable
```
The result will be an executable ```.app``` bundle inside a folder with other items necessary to run Quakespasm.

## Running
Locate the ```id1``` folder from your Steam or CD install of Quake. 

Copy it into the folder containing ```Quakespasm-SDL2-AppleSilicon.app```. 

Make sure ```id1```, ```id1/pak0.pak```, and ```id1/pak1.pak``` are all lowercase. 

Finally, Ctrl+Click to open ```Quakespasm-SDL2-AppleSilicon.app```.

## Planned
In the future, a native Metal renderer might be a necessity. Eventually OpenGL will be removed from macOS; it has been deprecated for years now.

## Quakespasm.txt
**NOTE:** Not all of the original readme applies to this build of Quakespasm. For example, the compiling instructions for Mac OS X do not apply.
```
  QuakeSpasm

  ____________________________________________________________

  Table of Contents

  1. About
  2. Downloads
  3. Hints
     3.1 Music Playback
     3.2 Controller Support
        3.2.1 Cvars
        3.2.2 Buttons

  4. Compiling and Installation
     4.1 Linux/Unix
     4.2 Windows
     4.3 Mac OS X
     4.4 Quake '2021 re-release'

  5. Changes
     5.1 Changes in 0.94.3
     5.2 Changes in 0.94.2
     5.3 Changes in 0.94.1
     5.4 Changes in 0.94.0
     5.5 Changes in 0.93.2
     5.6 Changes in 0.93.1
     5.7 Changes in 0.93.0
     5.8 Changes in 0.92.1
     5.9 Changes in 0.92.0
     5.10 Changes in 0.91.0
        5.10.1 Bugfixes
        5.10.2 Visual improvements
        5.10.3 Interface improvements
        5.10.4 Code cleanup / Other
        5.10.5 Raised limits
     5.11 Changes in 0.90.1
        5.11.1 Bugfixes
        5.11.2 Performance
        5.11.3 Visual improvements
        5.11.4 Interface improvements
        5.11.5 Code cleanup
     5.12 Changes in 0.90.0
     5.13 Changes in 0.85.9
     5.14 Changes in 0.85.8
     5.15 Changes in 0.85.7
     5.16 Changes in 0.85.6
     5.17 Changes in 0.85.5
     5.18 Changes in 0.85.4
     5.19 Changes in 0.85.3
     5.20 Changes in 0.85.2
     5.21 Changes in 0.85.1

  6. Copyright
  7. Contact
  8. Links


  ______________________________________________________________________

  Page last edited: December 2021


  1.  About

  QuakeSpasm <http://quakespasm.sourceforge.net> is a modern, cross-
  platform Quake engine based on FitzQuake
  <http://www.celephais.net/fitzquake>.

  It includes support for 64 bit CPUs and custom music playback, a new
  sound driver, some graphical niceities, and numerous bug-fixes and
  other improvements.

  Quakespasm utilizes either the SDL or SDL2 frameworks, so choose which
  one works best for you.  SDL is probably less buggy, but SDL2 has
  nicer features and smoother mouse input - though no CD support.


  2.  Downloads

  o  Project Downloads: http://quakespasm.sourceforge.net/download.htm

  o  Latest code repository:
     https://sourceforge.net/p/quakespasm/quakespasm/ci/master/tree/


  3.  Hints

  Visit the FitzQuake homepage <http://www.celephais.net/fitzquake> for
  a full run-down of the engine's commands and variables.

  o  To disable some changes, use "quakespasm -fitz"

  o  Quakespasm's custom data is stored in "quakespasm.pak". Install
     this file alongside your id1 directory to enable the custom console
     background and other minor features.

  o  For different sound backend drivers use :
     "SDL_AUDIODRIVER=DRIVER ./quakespasm"
     where DRIVER may be alsa, dsp, pulse, esd ...

  o  Shift+Escape draws the Console.

  o  From the console, use UP to browse the command line history and TAB
     to autocomplete command and map names.

  o  There is currently no CD Music volume support and SDL2 doesn't
     support CD audio. cd_sdl.c needs replacing with cd_linux.c,
     cd_bsd.c etc..

  o  In windows, alternative CD drives are accessible by
     "quakespasm -cddev F" (for example)

  o  Quakespasm allows loading new games (mods) on the fly with
     "game GAMENAME {-quoth/hipnotic/rogue}"

  o  Use "quakespasm -condebug" to save console log to "qconsole.log".
     SDL2 builds no longer generate stdout.txt/stderr.txt.

  3.1.  Music Playback

  Quakespasm can play various external music formats, including MP3, OGG
  and FLAC.

  o  Tracks should be named like "track02.ogg", "track03.ogg" ... (there
     is no track01) and placed into "Quake/id1/music".

  o  Unix users may need some extra libraries installed: "libmad" or
     "libmpg123" for MP3, and "libogg" and "libvorbis" for OGG.

  o  As of 0.90.0, music is played back at 44100 Hz by default with no
     need to adjust "-sndspeed".

  o  Use the "-noextmusic" option to disable this feature.

  o  See Quakespasm-Music.txt for more details.

  3.2.  Controller Support

  The SDL2 variant of Quakespasm supports Xbox 360 style game
  controllers.

  The default configuration uses the left analog stick for movement and
  the right for looking.

  If your controller doesn't work you can try placing this file
  https://raw.githubusercontent.com/gabomdq/SDL_GameControllerDB/master/gamecontrollerdb.txt
  in your Quake directory, it is a community-maintained database that
  adds support for more controllers to SDL2.

  3.2.1.  Cvars

  o  joy_deadzone - Fraction of the stick travel to be deadzone, between
     0 and 1. Default 0.175.

  o  joy_deadzone_trigger - Fraction of trigger range required to
     register a button press on the analog triggers, between 0 and 1.
     Default 0.2.

  o  joy_sensitivity_yaw/pitch - Max angular speed in degrees/second
     when looking. Defaults are 300 for yaw (turning left/right) and 150
     for pitch (up/down).

  o  joy_exponent - For the look stick, the stick displacement (between
     0 and 1) is raised to this power. Default is 3. A value of 1 would
     give a linear relationship between stick displacement and fraction
     of the maximum angular speed.

  o  joy_invert - Set to 1 to invert the vertical axis of the look
     stick.

  o  joy_swapmovelook - Set to 1 to swap the left and right analog stick
     functions. Default 0, move on the left stick, look on the right
     stick.

  o  joy_enable - Set to 0 to disable controller support. Default 1.

  3.2.2.  Buttons

  Some of the controller buttons are hardcoded to allow navigating the
  menu:

  o  Back - alias for TAB
  o  Start - alias for ESC
  o  DPad, analog sticks - mapped to arrow keys
  o  A Button - alias for ENTER in menus
  o  B Button - alias for ESC in menus

  These buttons can be bound normally:

  o  LTRIGGER - Left trigger
  o  RTRIGGER - Right trigger
  o  LSHOULDER - Left shoulder button
  o  RSHOULDER - Right shoulder button
  o  LTHUMB - Clicking the left thumbstick
  o  RTHUMB - Clicking the right thumbstick
  o  ABUTTON
  o  BBUTTON
  o  XBUTTON
  o  YBUTTON

  quakespasm.pak contains a default.cfg which has been updated to give
  some default bindings. L/R shoulder buttons are bound to weapon
  switching, and L/R triggers are jump and attack.

  The controller support started as Jeremiah Sypult's implementation in
  Quakespasm-Rift and also uses ideas and code from LordHavoc
  (DarkPlaces).


  4.  Compiling and Installation

  See the Downloads section to get the sourcecode, then below for
  platform specific instructions.  Quakespasm can also be built with the
  cross-platform Codeblocks.
  Quakespasm's (optional) custom data is now stored in the file
  quakespasm.pak. This file should be placed alongside your quakespasm
  binary and id1 directory.

  4.1.  Linux/Unix

  After extracting the source tarball, "cd Quake" and edit the Makefile
  for music options.

  Streaming music playback requires "libmad" or "libmpg123" for MP3, and
  "libogg" and "libvorbis" for OGG files.

  Then type "make" to compile the program, and copy the "quakespasm"
  binary (and "quakespasm.pak") to your Quake game directory.
  Compile time options include

  o  make DO_USERDIRS=1 to include user directories support

  o  make DEBUG=1 for debugging

  o  make SDL_CONFIG=/PATH/TO/sdl-config for unusual SDL installations

  o  make USE_SDL2=1 to compile against SDL2 instead of SDL-1.2

  4.2.  Windows

  The QuakeSpasm developers cross-compile windows binaries using MinGW
  <http://www.mingw.org> and MinGW-w64 <http://mingw-w64.sf.net>.

  The project can also be built using Visual Studio 2005 (or newer).

  4.3.  Mac OS X

  A Quakespasm App (including program launcher and update framework) can
  be made using the Xcode template found in the MacOSX directory.

  Alternatively, have a look at Makefile.darwin for more instructions on
  building from a console.

  4.4.  Quake '2021 re-release'

  QuakeSpasm 0.94.0 has initial support for playing the 2021 re-release
  content: Copy the quakespasm binary to your rerelease installation and
  run quakespasm as you normally do.


  5.  Changes


  5.1.  Changes in 0.94.3

  o  Handle sky textures with non-standard sizes and warn about them
     (e.g. ad_tears)
  o  Allow loading textures not aligned to 16 pixels and warn about them
     (eg. the horde2 map of Dimension of the Machine from 2021 rerelease
     update/2.)
  o  Updated included SDL2 to latest version 2.0.18.


  5.2.  Changes in 0.94.2

  o  2021 rerelease: Support for playing the latest update.

  o  2021 rerelease: Fix pitch black models in lit areas in DOTM.

  o  2021 rerelease: Fix black candles in the DOTM start map.

  o  2021 rerelease: Look for QuakeEX.kpf under userdir, too.


  5.3.  Changes in 0.94.1

  o  Fix lightmap issues after vkQuake surface mark/cull optimizations
     merge (sf.net bug/50)


  5.4.  Changes in 0.94.0

  o  Initial support for playing the 'Quake 2021 re-release' content
     (thanks to Andrei Drexler for bulk of the work, Guillaume Plourde
     for Q64 bsp format support.)

  o  Fix rendering bug when cl_bobcycle was set to zero (sf.net bug/41)

  o  Fixed buffer overflow with large char skybox names (sf.net bug/38)

  o  Fixed a missing MAXALIASFRAMES bounds check (sf.net bug/37)

  o  OpenGL: workaround Intel UHD 600 driver bug (sf.net bug/39)

  o  OpenGL: merged surface mark & cull optimizations from vkQuake.

  o  Compensate viewmodel distortion at fov > 90 (based on code from
     Qrack, thanks to Andrei Drexler for the patch.)

  o  Raised MAX_GLTEXTURES limit from 2048 to 4096 for now.

  o  Changed 'model has a skin taller than 480' error into a warning

  o  Reject lit files if they're the wrong size (eg hipnotic/start.bsp
     vs id1/start.lit or just a bsp that no longer has any coloured
     lits, etc)

  o  External ent files are now versioned using 4 digit crc of the
     original map's ents, like e1m1@c49d.ent, which is much safer. The
     old method (e.g. e1m1.ent) still works but isn't recommended.

  o  Support for external vis files.

  o  Save: remove CR/LFs from level name to avoids broken saves, e.g.
     with autumn_sp map.

  o  Music: improvements to mp3 tag detection / skipping.

  o  Music: umx loader fix for malformed / crafted files.

  o  New console command music_jump: Jump to given order in music, like
     Unreal's music change - only for module (tracker) music.

  o  Updated third-party libraries (music codecs, SDL, etc.) Other minor
     fixes, tidy-ups and protability tweaks.

  o  Source repository moved to git.


  5.5.  Changes in 0.93.2

  o  Lightmaps are now dynamically allocated (from QSS), and
     BLOCK_WIDTH/HEIGHT raised from 128 to 256.

  o  Fixed several uncheked limits that would crash the Slayer's
     Testaments mod (sf.net bug #33).

  o  Raised MAXALIASTRIS from 2048 to 4096, so that the Slayer's
     Testaments mod works.

  o  Fixed 'pants' and 'shirt' types so that those textures load
     correctly on platforms where char type is unsigned by default
     (sf.net bug #28).

  o  Windows audio: WASAPI-enabled SDL2 dlls function properly now.

  o  Update the third-party libraries. Other fixes/cleanups.


  5.6.  Changes in 0.93.1

  o  Fixed a fog regression which was introduced in 0.93.0.

  o  Fixed a crash (buffer overflow) with invalid vis data.

  o  Fixed buttons crushing players in 64-bit builds.

  o  Change controller movement to use cubic easing by default; added
     "joy_exponent_move" cvar.

  o  config.cfg is no longer written in case of a Sys_Error.

  o  Fixed Opus encoded cd tracks not being recognized as ripped tracks.

  o  Update the third-party libraries. Other fixes/cleanups.


  5.7.  Changes in 0.93.0

  o  Raise default "joy_deadzone_trigger" cvar to 0.2.

  o  Raise console buffer size to 1MB.

  o  Raise MAX_STATIC_ENTITIES from 512 to 4096.

  o  Raise MAX_STACK_DEPTH from 32 to 64.

  o  Raise command buffer size from 8K to 256K to support large configs.

  o  Remove MAX_EFRAGS and MAX_MAP_LEAFS limits.

  o  Remove "Loadgame buffer overflow" limit, which could happen when
     loading DP or QSS saves.

  o  Adjust "exceeds standard limit of" debug warnings to include the
     actual QS limit.

  o  Change "game" command to now exec quake.rc.

  o  Change "games" / "mods" commands to list all subdirectories.

  o  Restore vid_refreshrate from fitzquake-0.85 for SDL2 builds.

  o  Alpha-masked model support. (MF_HOLEY: 0x4000).

  o  Invalid skin index now draws skin 0 (WinQuake behaviour) instead of
     blue checkerboard.

  o  Change default screenshot format to png. The 'screenshot' command
     now supports optional format (tga, png or jpg) and quality (1-100)
     arguments.

  o  Revert "always run" changes from 0.85.9 and move the QuakeSpasm
     customizations to a new "cl_alwaysrun" cvar: Set to 1 in order to
     scale forward/side/up speed by "cl_movespeedkey" (usually 2), and
     to make "speedkey" act as "slowkey".

  o  Change the "always run" menu option to offer three choices:
     off        (cl_alwaysrun 0, cl_forwardspeed 200, cl_backspeed 200)
     vanilla    (cl_alwaysrun 0, cl_forwardspeed 400, cl_backspeed 400)
     quakespasm (cl_alwaysrun 1, cl_forwardspeed 200, cl_backspeed 200)

  o  New "r_scale" cvar. Set to 2, 3, or 4 to render the view at 1/2,
     1/3, or 1/4 resolution.

  o  New "r_viewmodel_quake" cvar. Set to 1 for WinQuake gun position
     (from MarkV).

  o  New "find" / "apropos" command, searches for commands/cvar names
     for the given substring (from Spike).

  o  New "randmap" command for loading a random map.

  o  New "gl_cshiftpercent_contents", "gl_cshiftpercent_damage",
     "gl_cshiftpercent_bonus", "gl_cshiftpercent_powerup" cvars for
     tuning the strength of specic view blends.

  o  GL2 renderer: use a GLSL shader for world faces. Fixes reports of
     integrated+discrete GPU laptops having inconsistent fog rendering.

  o  Fix macOS startup delay (avoid calling gethostbyname() for ".local"
     hostnames).

  o  Fix memory corruption in PF_lightstyle with out of bounds
     lightstyles.

  o  Fix crash in BoundPoly with polygons extending beyond +/-9999.

  o  Fix QS window to stay on the current monitor when changing video
     modes (SDL2 only).

  o  Fix possible freeze in SV_TouchLinks regardless of what QC does in
     the touch function.

  o  Fix for maps with empty strings for vector keys (e.g. "origin");
     don't read uninitialized memory.

  o  Support for Open Watcom compiler.

  o  Update the third-party libraries.


  5.8.  Changes in 0.92.1

  o  Fixed large menu scale factors (was broken in 0.92.0).

  o  Fixed PAUSE key (was broken in 0.92.0).

  o  Updated some of the third-party libraries.


  5.9.  Changes in 0.92.0

  o  SDL2 Game Controller support.

  o  Contrast support with new "contrast" cvar, behaving the same as
     MarkV. It may be a useful alternative to the existing gamma control
     for laptops in a bright environment, etc. Raising contrast gives
     less of a gray/washed out look than raising gamma, but at a
     disadvantage: colors near white get clipped to white.

  o  RMQ protocol (999) support, adapted from RMQEngine.

  o  New "-protocol x" command line option. Accepted values for 'x' are
     15 (NetQuake), 666 (FitzQuake, default), and 999 (RMQ).

  o  New "setpos" console command.

  o  New "vid_borderless" cvar for getting a borderless window.

  o  Increased MAX_MAP_LEAFS from 65535 to 70000 and MAX_LIGHTMAPS from
     256 to 512 in order to handle the oms3 map pack.

  o  Server edicts are now allocated using malloc instead of allocating
     on the hunk.

  o  gl_clear now defaults to 1.

  o  Fix items falling out of the world on oms3.bsp on SSE builds.

  o  Worked around an OSX 10.6 driver bug when using FSAA, which was
     leading to an unplayable HOM effect on the rest of the screen.

  o  Fix wrong trace endpoint from the tracepos console command.

  o  Updated some of the third-party libraries. Other fixes/clean-ups.


  5.10.  Changes in 0.91.0

  5.10.1.  Bugfixes

  o  Fix unwanted fog mode change upon video restart.

  o  Work around Intel 855 bug in status bar drawing with "r_oldwater 0"
     and "scr_sbaralpha 0".

  o  Fix an obscure GLSL bug where changing gamma would result in the
     screen turning to noise.

  o  Fix GLSL gamma causing the tiled screen border to turn white when
     "sizedown" is used.

  o  Fix an alias model VBO renderer bug where a model not precached
     during map start wouldn't be drawn.

  o  Fix the order of OpenGL context creation and window creation in
     SDL2 video.

  o  Fix a calling convention issue in windows DPI awareness function
     pointers.

  o  Fix a random texture recoloring after video mode change.

  o  Fix a liquid turning to garbage after several video mode changes
     and "r_oldwater 0".

  o  Fix a wrong alpha-sorting bug introduced in 0.90.1.

  o  Fix "flush" command not reloading mdl's from disk (bug introduced
     in 0.90.1).

  o  Prevent a possible buffer overflow in Cbuf_Execute (old Q1/Q2 bug).

  o  Prevent a possible vulnerability in MSG_ReadString (old Q1/Q2 bug).

  5.10.2.  Visual improvements

  o  New cvars r_lavaalpha, r_slimealpha, r_telealpha for fine-tuning
     specific liquid opacities (from DirectQ/RMQEngine, non-archived,
     default to 0), and new worldspawn keys _wateralpha, _lavaalpha,
     _slimealpha, _telealpha, _skyfog (unique to Quakespasm, similar to
     the behaviour of the "fog" worldspawn key).

  o  GLSL gamma is now supported on older hardware without NPOT
     extension.

  5.10.3.  Interface improvements

  o  New r_pos command to show player position.

  o  NaN detection in traceline with "developer 1" set now warns instead
     of errors.

  5.10.4.  Code cleanup / Other

  o  Update third-party libraries.

  5.10.5.  Raised limits

  o  Default max_edicts 8192 (was 2048) and no longer saved to
     config.cfg.

  o  Default heapsize 256 MB (was 64 MB).

  o  Default zone 4 MB (was 384 KB).

  o  Raised MAX_SFX to 1024 (was 512).


  5.11.  Changes in 0.90.1

  5.11.1.  Bugfixes

  o  Fix dynamic light artifact where changing lightmap are rendered one
     frame late (bug introduced in 0.90.0).

  o  Fix texture memory leak when changing video modes with SDL2.

  o  Fix a rare incorrect mdl lighting on 64-bit builds. (details here:
     http://forums.insideqc.com/viewtopic.php?f=3&t=5620)

  o  Fix fullbrights turning black after "kill" command (bug introduced
     in 0.90.0).

  o  Clear all fog values on map change to prevent colored fog carrying
     over to jam3_tronyn.bsp.

  o  Allow loading saves with } character in quoted strings, fixes issue
     with retrojam1_skacky.bsp.

  o  Fix viewmodel not lerping on extended-limit maps.

  o  Fix crash on out-of-bounds skin number.

  5.11.2.  Performance

  o  Use multithreaded OpenGL on OS X for better performance.

  o  New, faster mdl renderer using GLSL. Disable with "-noglslalias".

  5.11.3.  Visual improvements

  o  New gamma correction implementation using GLSL. Fixes all known
     gamma issues (affecting the full display, persisting after
     quitting, or darkening the screen on OS X). Disable with
     "-noglslgamma".

  o  Use high-quality water by default (r_oldwater 0).

  o  Shadows use stencil buffer to avoid overlapping artifacts (from
     MarkV.)

  o  r_noshadow_list cvar added (from MarkV.)

  5.11.4.  Interface improvements

  o  Support pausing demo playback with the "pause" command.

  o  Autocompletion for "game", "record", "playdemo".

  o  Experimental windowed fullscreen mode available with
     vid_desktopfullscreen 1 (only in SDL2 builds, takes effect upon
     entering fullscreen mode the next time.)

  o  Silence "exceeded standard limit" messages unless developer cvar is
     >= 1.

  o  Some spam moved from developer 1 to 2: "can't find tga/lit/ent",
     "trying to load ent", "bad chunk length", "meshing",
     "PR_AlocStringSlots: realloc'ing"

  5.11.5.  Code cleanup

  o  Clean up IDE project files to build on fresh systems.

  o  Update 3rd-party libraries.


  5.12.  Changes in 0.90.0

  o  Fix issues on Windows systems with DPI scaling.

  o  Unix/Mac user directories support. Disabled by default,
     'make DO_USERDIRS=1' to enable it.

  o  SDL2 support. Disabled by default, 'make USE_SDL2=1' to enable it.

  o  Revised keyboard input code.

  o  Revised/improved the 'game' command, i.e. on-the-fly mod changing.
     It now accepts an optional second argument for mission packs or
     quoth support i.e. -hipnotic, -rogue, or -quoth. For example, for
     WarpSpasm: "game warp -quoth"

  o  Command line: "-game {quoth/hipnotic/rogue}" is now treated the
     same as -quoth, -hipnotic, or -rogue.

  o  Console speed now resolution-independent.

  o  Disabled gl_zfix, which caused glitches and is undesirable for new
     maps. Replacement .ent files to fix z-fighting for several id1 maps
     added to quakespasm.pak.

  o  PF_VarString buffer bumped to 1024, avoids truncated centerprints
     from the 'In The Shadows' mod.

  o  Support for opengl non-power-of-two-textures extension (disable
     with command line: "-notexturenpot".)

  o  Support for OpenGL vertex buffer objects (VBO, OpenGL 1.5 or newer)
     for world and brush models (disable with command line: "-novbo".)

  o  Antialiasing (FSAA) support (command line: -fsaa x, where x can be
     0, 2, 4, 8).

  o  Fence textures support.

  o  Dynamic light speedup. Speedup loading of tga and pcx external
     images.

  o  Brush model drawing speedup.

  o  Support for BSP2 and 2PSB map formats.

  o  Support for Opus, FLAC, and tracker music (S3M, IT, UMX, etc.), as
     compile-time options.

  o  Music and sfx now mixed at 44100 Hz to avoid downsampling music.
     Low-pass filter applied to the sfx if -sndspeed is 11025 (the
     default), to preserve the same sound quality as 0.85.9.  New
     -mixspeed option sets the rate for mixing sfx and music, and output
     to the OS (default 44100), setting it to 11025 reverts to 0.85.9
     behaviour. New snd_filterquality cvar, value can be between 1
     (emulate OS X resampler) and 5 (emulate Windows resampler),
     controls the sound of the low-pass filter.

  o  Better Hor+ field of view (FOV) scaling behavior.

  o  Better cross-map demo playback support.

  o  Fix screenshots when screen width isn't a multiple of 4.

  o  Fix a lighting glitch due to floating point precision.

  o  Fix a looping sounds glitch.

  o  Fix a vulnerability in file extension handling. Tighten path
     handling safety.

  o  Initialize opengl with 24-bit depth buffer at 32 bpp.

  o  Reset all models upon gamedir changes. (Fixes failures with mods
     using custom content.)

  o  Fix broken behavior upon gamedir changes if -basedir is specified
     on the command line.

  o  NET_MAXMESSAGE and MAX_MSGLEN limits bumped to 64000.

  o  MAX_EFRAGS bumped to 4096, and MAX_CHANNELS to 1024.

  o  MAX_ENT_LEAFS bumped from 16 to 32 to work around disappearing or
     flickering brush models in some situations. Also, if an entity is
     visible from MAX_ENT_LEAFS or more leafs, we now always send it to
     the client.

  o  Fix cvar cycle command not working sometimes.

  o  Host_Error upon missing models. (Prevents segmentation faults.)

  o  Change sv_aim default value to 1 (i.e. turn off autoaim)

  o  Add 'prev' and 'next' keywords to the 'cd' command.

  o  Work around a linux cdrom issue (playback might not start for a
     while after a stop).

  o  Quakespasm content customization moved from engine-embedded into a
     new optional quakespasm.pak file.

  o  Version bumped to 0.90.0 (because Quakespasm has a decent life of
     it's own)

  o  Other fixes and clean-ups.


  5.13.  Changes in 0.85.9

  o  Fixes for several undefined behaviors in C code (gcc-4.8 support.)

  o  Implemented Hor+ style field of view (FOV) scaling, useful for
     widescreen resolutions. Configured by new cvar fov_adapt: set it to
     1 and your fov will be scaled automatically according to the
     resolution. Enabled by default.

  o  Adjusted string buffers for PR_ValueString and friends to fix
     crashes with excessively long global strings seen in some rude
     mods.

  o  Toned down warning messages from PF_VarString() a bit.

  o  Fixed Fitzquake's map existence check in changelevel (used to leak
     file handles which would end up in a Sys_Error() due to consuming
     all free handles if many maps reside not in pak files.)

  o  Fixes/cleanups in chat mode handling. Client no longer gets stuck
     in chat mode upon disconnect.

  o  Mouse grab/key_dest fixes and key cleanups.

  o  The "speedkey" now acts as "slowkey" when "always run" is on.

  o  Support for demo recording after connection to server. (thanks to
     Baker for a patch)

  o  Corner case fixes in COM_Parse() for quoted strings and support for
     C-style /*..*/ comments.

  o  Changed lightmaps to GL_RGBA instead of GL_RGB.

  o  Better parse for opengl extensions list (from quakeforge.)

  o  Vsync saving/loading fixes.

  o  Fixed pointfile loading.

  o  Multiple cleanups in gl_vidsdl.c.

  o  Opus music decoding support (as an optional patch only.)

  o  Several other minor fixes/cleanups.


  5.14.  Changes in 0.85.8

  o  Made Quake shareware 1.00 and 1.01 versions to be recognized
     properly.

  o  Fixed control-character handling in unicode mode. Keyboard input
     tweaks.

  o  Made the keypad keys to send separate key events in game mode.

  o  Text pasting support from OS clipboard to console. (windows and
     macosx.)

  o  Support for the Apple (Command) key on macosx.

  o  Fixed increased (more than 32) dynamic lights.

  o  Music playback: Made sure that the file's channels count is
     supported.

  o  Support for Solaris.

  o  Switched to using libmad instead of libmpg123 for MP3 playback on
     Mac OS X.

  o  Better support for building the Mac OS X version using a makefile,
     support for cross-compiling on Linux.

  o  Fixed a minor intermissions glitch.

  o  Increased string buffer size from 256 to 384 for PF_VarString to
     work around broken mods such as UQC.

  o  Restored original behavior for Quake registered version detection.

  o  Minor demo recording/playback tweaks.

  o  Minor tweaks to the scale menu option.

  o  unbindall before loading stored bindings (configurable by new cvar
     cfg_unbindall, enabled by default.)

  o  New icon.

  o  Miscellaneous source code cleanups.


  5.15.  Changes in 0.85.7

  o  Added support for cross-level demo playback

  o  gl_texturemode is reimplemented as a cvar with a callback and the
     setting is automatically saved to the config

  o  Fixed execution of external files without a newline at the end

  o  Reduced memory usage during reloading of textures

  o  Fixed compilation on GNU/kFreeBSD (Debian bug #657793)

  o  Fixed backspace key on Mac OS X

  o  Disable mouse acceleration in Mac OS X

  o  Worked around recursive calling of the anisotropic filter callback

  o  Console word wrap and long input line fixes

  o  Verified correct compilation by clang (using v3.0)

  o  Several other small changes mostly invisible to the end-user


  5.16.  Changes in 0.85.6

  o  More work for string buffer safety

  o  Reverted v0.85.5 change of not allowing deathmatch and coop cvars
     to be set at the same time (was reported for possibility of causing
     compatibility issues with mods)

  o  Several cleanups/changes in the cvar layer

  o  Minor SDL video fixes.


  5.17.  Changes in 0.85.5

  o  SDL input driver updated adding native keymap and dead key support
     to the console

  o  Fixed a crash in net play in maps with extended limits

  o  Verified successful compilation using gcc-4.6.x

  o  Added workaround against GL texture flicker (z fighting),
     controlled by new cvar 'gl_zfix'

  o  Read video variables early so that a vid_restart isn't necessary
     after init

  o  mlook and lookspring fixes

  o  Added support for loading external entity files, controlled by new
     cvar 'external_ents'

  o  Made mp3 playback to allocate system memory instead of zone

  o  Some updates to the progs interpreter code

  o  Fixed r_nolerp_list parsing code of fitzquake

  o  Made sure that deathmatch and coop are not set at the same time

  o  Several code updates from uHexen2 project, several code cleanups.


  5.18.  Changes in 0.85.4

  o  Implement music (OGG, MP3, WAV) playback

  o  A better fix for the infamous SV_TouchLinks problem, no more hard
     lockups with maps such as "whiteroom"

  o  Add support for mouse buttons 4 and 5

  o  Fix the "unalias" console command

  o  Restore the "screen size" menu item

  o  Fixed an erroneous protocol check in the server code

  o  Raised the default zone memory size to 384 kb

  o  Raised the default max_edicts from 1024 to 2048

  o  Revised lit file loading, the lit file must be from the same game
     directory as the map itself or from a searchpath with a higher
     priority

  o  Fixed rest of the compiler warnings

  o  Other minor sound and cdaudio updates


  5.19.  Changes in 0.85.3

  o  Fix the "-dedicated" option (thanks Oz) and add platform specific
     networking code (default) rather than SDL_net

  o  Much needed OSX framework stuff from Kristian

  o  Add a persistent history feature (thanks Baker)

  o  Add a slider for scr_sbaralpha, which now defaults to 0.95
     (slightly transparent, allowing for a nicer status bar)

  o  Allow player messages longer than 32 characters

  o  Sockaddr fix for FreeBSD/OSX/etc networking

  o  Connect status bar size to the scale slider

  o  Include an ISNAN (is not-a-number) fix to catch the occassional
     quake C bug giving traceline problems

  o  Enumerate options menus

  o  Add a "prev weapon" menu item (from Sander)

  o  Small fix to Sound Block/Unblock on win32

  o  Lots of code fixes (some from uhexen2)

  o  Sys_Error calls Host_Shutdown

  o  Added MS Visual Studio support

  o  Add a "-cd" option to let the CD Player work in dedicated mode, and
     some other CD tweaks.


  5.20.  Changes in 0.85.2

  o  Replace the old "Screen size" slider with a "Scale" slider

  o  Don't constantly open and close condebug log

  o  Heap of C clean-ups

  o  Fix mapname sorting

  o  Alias the "mods" command to "games"

  o  Block/Unblock sound upon focus loss/gain

  o  NAT fix (networking protocol fix)

  o  SDLNet_ResolveHost bug-fix allowing connection to ports other than
     26000

  o  Bumped array size of sv_main.c::localmodels from 5 to 6 fixing an
     old fitzquake-0.85 bug which used to cause segfaults depending on
     the compiler.

  o  Accept commandline options like "+connect ip:port"

  o  Add OSX Makefile (tested?)


  5.21.  Changes in 0.85.1

  o  64 bit CPU support

  o  Restructured SDL sound driver

  o  Custom conback

  o  Tweaked the command line completion and added a map/changelevel
     autocompletion function

  o  Alt+Enter toggles fullscreen

  o  Disable Draw_BeginDisc which causes core dumps when called
     excessively

  o  Show helpful info on start-up

  o  Include real map name (sv.name) and skill in the status bar

  o  Remove confirm quit dialog

  o  Don't spam the console with PackFile seek requests

  o  Default to window mode

  o  Withdraw console when playing demos

  o  Don't play demos on program init

  o  Default Heapsize is 64meg

  o  Changes to default console alpha, speed

  o  Changes to cvar persistence gl_flashblend (default 0), r_shadow,
     r_wateralpha, r_dynamic, r_novis


  6.  Copyright

  o  Quake and Quakespasm are released under the GNU GENERAL PUBLIC
     LICENSE Version 2: http://www.gnu.org/licenses/gpl-2.0.html

  o  Quakespasm console background image by AAS, released under the
     CREATIVE COMMONS PUBLIC LICENSE:
     http://creativecommons.org/licenses/by/3.0/legalcode


  7.  Contact

  o  QuakeSpasm Project page:
     https://sourceforge.net/projects/quakespasm/

  o  Bug reports:
     https://sourceforge.net/p/quakespasm/bugs/

  o  Ozkan <mailto:gmail - dot - com - username - sezeroz>
     Eric <mailto:gmail - dot - com - username - ewasylishen>
     Sander <mailto:gmail - dot - com - username - a.h.vandijk>


  8.  Links

  o  QuakeSpasm Homepage: http://quakespasm.sourceforge.net

  o  Downloads: http://quakespasm.sourceforge.net/download.htm

  o  FitzQuake Homepage: http://www.celephais.net/fitzquake

  o  Func Quakespasm forum:
     http://www.celephais.net/board/view_thread.php?id=60452

  o  Inside3D forums: http://forums.insideqc.com

```
