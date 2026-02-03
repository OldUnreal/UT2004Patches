# Unreal Tournament 2004 Release Notes

## General Information

### Official Unreal Tournament Web Sites

* [Unreal Tournament Home Page](https://www.unrealtournament.com)
* [Epic Games Home Page](https://epicgames.com)
* [Unreal Engine Technology Page](https://www.unrealengine.com)

### Independent Unreal Tournament Web Sites and Discord servers

* [OldUnreal site](https://www.oldunreal.com) / [OldUnreal Discord](https://discord.com/channels/143986633992175616/1053202987545264128)
* [MiA Forums](https://www.miasma.rocks)  / [MiA Discord](https://discord.gg/CxdXaEauya)
* [CEONS Forums](https://ceonss.net/) / [CEONS Discord](https://discord.com/channels/310878149158240257/310878149158240257)

## Unreal Tournament 2004 Version 3374 Release Notes (Release Preview Coming Soon!)

Version 3374 is completely network compatible with the previous public release of UT2004 (3369). 

> [!IMPORTANT]
> If you are installing our patch manually, you should update your game client to version 3369 and install the Epic ECE Bonus Pack first.
> If you use our installers, the necessary files will be installed automatically.

### Patch Highlights

* We now natively support Linux and macOS systems with x86_64/amd64 and arm64/aarch64 CPUs 
* You can now play the game or run a server on a Raspberry Pi 4 or 5, albeit at rather slower frame-rate than on a PC!
* The Linux and macOS distributions of the patch now include a fully functional UCC with an UnrealScript compiler (UCC make)
* We dropped support for 32-bit CPUs, for old versions of Windows (i.e., Vista or earlier), and for DirectX 8
* The Windows version of the game now requires DirectX 9
* The Linux and macOS versions now use SDL3 instead of SDL1
* We dealt a first (minor) blow to the editor goblin! Unreal Editor will no longer freeze for several seconds when clicking a viewport
* Our patch includes a brand new OpenGL 3.3 / ES 3.0 renderer, AntiDrv. This renderer outperforms the original OpenGLDrv on most platforms, adds new features (e.g., shader-based gamma/color correction), implements/fixes several features that were missing/broken in the original OpenGLDrv (e.g., gradient projectors and weightmap terrain rendering), makes features that were previously nvidia/amd-exclusive available on all platforms (e.g., CO_AlphaBlend_With_Mask combiners), and it can serve as a reference implementation for other new renderers. AntiDrv will be available in Preview 6

### Stability Improvements

#### Unreal Editor

* We fixed a bug that crashed Unreal Editor when converting meshes to brushes
* We fixed a bug that crashed Unreal Editor when you opened a map while the 3D viewport was in realtime mode
* We fixed a bug that could crash Unreal Editor when selecting something in a 3D viewport that uses D3D9Drv
* We fixed a bug that made UnrealEd crash when importing certain skeletal meshes ([#115](https://github.com/OldUnreal/UT2004Patches/issues/115))
* The terrain editor no longer crashes when the TerrainMap is null ([#120](https://github.com/OldUnreal/UT2004Patches/issues/120))
* The terrain editor no longer crashes when the terrain has a scale of 0 ([#139](https://github.com/OldUnreal/UT2004Patches/issues/139))
* We fixed a bug that made the editor crash when deleting a shader texture and selecting another shader afterwards

#### Networking and Netcode

* We fixed a networking bug that allowed players to perform illegal combo moves and to crash servers
* Clients no longer hang in connecting screen when server has too many server packages

#### Audio and 3D Rendering

* We fixed a bug that could crash the game when rendering skeletal meshes with invalid hierarchies
* We fixed a bug that could crash the game when rendering particles emitted by invalid skeletal mesh actors

#### Physics

* We fixed a bug that could make the game crash when an emitted particle collides with an actor

#### UnrealScript

* The game should no longer crash if you click a tab in an in-game menu whose content is still being rendered
* We fixed a bug that could make the game crash when calling Engine.Controller.PickTarget while the pawn, level, or game is invalid

#### Miscellaneous

* We fixed a bug that made the game crash when reading an Unreal package with an unexpected GUID
* We fixed a garbage collection bug that made the game crash upon shutdown
* We fixed a bug that made the game randomly crash when it tried to write to the log file during shutdown

### Bug Fixes

#### Unreal Editor and UCC

* The procedural sound context menus should now be fully functional
* The display checkbox for placeables actors in the actor browser should now work as expected
* We fixed a bug that made Unreal Editor create dummy packages when converting static meshes to or from brushes
* Unreal Editor now saves viewport sizes correctly even when viewports are minimized
* Large .int files are now saved correctly without truncation ([#12](../../issues/12))
* The UnrealScript compiler now parses and compiles scripts in the correct order after it processes `dependson` directives
* The editor no longer moves left and down when clicking on a viewport, when used on a multi-monitor setup
* Viewport selection no longer takes a century, instead acting instantly
* We fixed bugs that made Unreal Editor incorrectly import and export DDS files
* We fixed a bug that made the Unreal Editor tooltips disappear on some systems
* We fixed a bug that made materials used by static meshes not appear in the texture browser's "in use" tab
* The static mesh to brush converter now works as expected when converting a mesh with a negative draw scale
* We fixed a bug that made Unreal Editor freeze when closing a modal dialog using the X button
* We fixed a bug that crashed the editor when opening a non-existing file
* We fixed some UI sizing issues in the terrain editor
* Skeletal mesh faces should now get sorted correctly during import
* We fixed a bug that made the 'None' group list show all sounds from other groups
* We fixed a bug that made surface properties update slowly when unselecting a surface

#### Networking and Netcode

* The game now reports the correct progress percentage when downloading files from a game server
* The game client will no longer call PostNetBeginPlay twice for certain actors
* We fixed an issue that made the server browser not update information/pings when the netspeed is above 20000 ([#72](https://github.com/OldUnreal/UT2004Patches/issues/72))

#### Audio and 3D Rendering

* We fixed a bug that made ambient sounds restart whenever the player camera switches to a different view target
* Music fadeouts should now work as expected
* We fixed an issue that made music volume changes reset the currently playing song ([#102](https://github.com/OldUnreal/UT2004Patches/issues/102))

#### Physics

* We fixed a bug that triggered a "moved without proper hashing" warning when a player disconnected while possessing a live pawn
* We fixed a bug that made SVehicleWheels collide with Pawns even when the vehicle had bBlockActors set to false ([#37](https://github.com/OldUnreal/UT2004Patches/issues/37))

#### Webadmin

* We fixed a bug that made the webadmin fail intermittently on some platforms

#### Input and Windowing

* We fixed a problem that made the game receive mouse and joystick input even while its window is not in focus
* We fixed a bug that made the game window lose mouse focus after alttabbing out and back in on Windows
* We fixed a bug that made the mouse cursor stick to the edge of the game window in fullscreen mode

#### UnrealScript

* We fixed a plethora of accessed nones and UnrealScript-based exploits, crash bugs, and denial-of-service attacks (Thank you Wormbo and Shambler!)
* We fixed a bug that could make the SPMA camera explosion loop without stopping ([#24](../../issues/24))
* The PlayerController.AskForPawn function now jumps to the Spectating.Begin state correctly ([#10](../../issues/10))
* The PlayerController.ToggleScreenShotMode function no longer discards user preferences such as the weapon handedness, crosshair visibility, HUD visibility, and the TeamBeaconMaxDist and bHideVehicleNoEntryIndicator settings ([#11](../../issues/11))
* The DeathMatch.InitTeamSymbols function can no longer give multiple teams the same symbol ([#16](../../issues/16))
* We fixed a bug where gibbed players or monsters can be gibbed multiple times by sources of constant damage
* We fixed several bugs that made Engine.Canvas incorrectly process newline characters and color codes
* We fixed a bug that made the Linux and macOS clients crash when loading font textures with remapped fonts
* We fixed a bug that could make the game crash after calling LinkMesh on a new skeletal mesh that uses dynamic hitboxes
* We fixed a bug that could make the game crash when you called TerrainInfo.PokeTerrain
* Mortar shells should now work correctly on low-grav maps
* We fixed a bug that could unexpectedly prevent you from exiting raptor vehicles
* We fixed memory leaks in the ONSShockTankMuzzleFlash and SVehicle classes
* We fixed a bug in the Linux/macOS client that made the game exit when trying to open a URL if the BROWSER environment variable was not set ([#132](https://github.com/OldUnreal/UT2004Patches/issues/132))
* The game should now display item pickup messages when playing with the vehicle pickups mutator ([#154](https://github.com/OldUnreal/UT2004Patches/issues/154))
* We fixed a bug that made the player model in the player selection menu appear upside down ([#146](https://github.com/OldUnreal/UT2004Patches/issues/146))
* The domination tutorial should now work as expected
* We fixed a typo in the particle emitter velocity scaling code that made particle emitters ignore Z-scaling
* We fixed a bug that made it possible to receive bloodrites challenges for non-existent team members ([#136](https://github.com/OldUnreal/UT2004Patches/issues/136#issuecomment-3745256548))

#### Miscellaneous

* We now support command lines longer than 1024 characters
* We backported UT 469's FMemCache implementation. This will give us some decent performance improvements on some maps

### Enhancements

#### Unreal Editor and UCC

* The Unreal Editor window no longer minimizes when testing a map
* The properties window now supports mouse wheel scrolling
* You can now expand and collapse items in the properties window using keyboard arrows
* The music browser now supports ogg files
* You can now import ASE and OBJ models as static meshes
* We overhauled the texture compression code and switched to a new texture compression support library (AMD Compressonator). The new code works on all platforms so you can now import compressed textures using UCC make
* You can now launch UCC from different folders on Linux and macOS
* The mesh browser now has a package combo box and a button to open the mesh properties window
* Unreal Editor now embeds the full name of exported textures in the names of the exported files
* The sound and material browsers now have a menu option allowing you to export all in-use sounds/materials
* The map export dialog now uses the correct map name as the default name of the exported file
* You can now use the CTRL+Space hotkey to align the camera to the selected actor
* Viewports now refresh when you jump to an actor using the search actor dialog
* The editor can now import and export convex volumes
* We added support for importing UnrealEngine 1 T3D files
* You can now search classes in the actor browser
* Double-clicking a package name in the actor browser now opens all of that package's classes in the code editor
* The editor now remains responsive during slow operations that show a progress bar
* The editor progress bar dialogs now update only when the progress has increased
* We added an audio beep notification that signals the completion of a long editor operation (configurable using the Options.NotifyActionEndAfterSeconds option in UnrealEd.ini)
* We optimized the reachspecs generation code and made this code log build times
* We reduced the log spam caused by path nodes being too close to eachother
* We added colored output to UCC (might not work on some platforms)
* We made the output of UCC make more compact
* Unreal Editor and UCC now log additional information when they warn about invalid materials in skeletal meshes
* We implemented several optimizations that should speed up undo/redo operations ([#63](https://github.com/OldUnreal/UT2004-testing/issues/63))

#### Networking and Netcode

* Download messages now include information about the number of packages to download and the percentage of total download completed
* The game client now downloads and collates game server information from multiple master servers
* Game servers can now connect to multiple community master servers
* You can now configure the UCC server query port number for admins. See [here](https://github.com/ukpiglet/UDPRelay) for an example of how this can be used on a Windows based UCC server
* Demos recorded in offline games will now work with mods that add packages to the package map using Actor.AddToPackageMap
* You can now add favorite servers using their fully qualified domain name
* We now automatically detect the GoG CD key and replace it with a unique key

#### Audio and 3D Rendering

* Full screen support is now available in the 64-bit Windows client
* You can now cap your frame rate for menus and for offline games using the MaxMenuFrameRate and MaxOfflineFrameRate settings (see Default.ini)
* The player model now renders in mirror reflections
* Vertex models now render in OverlayMaterial
* You can now crossfade between two music tracks using MusicEvents
* Music OGG files support loop points (or even looping disabled)
* Text-to-speech is now available in the 64-bit Windows client
* OpenGLDrv now supports gamma correction even when the game runs in windowed mode
* We no longer delete the renderer when switching between fullscreen and windowed mode. This should make these mode switches much faster

#### Physics and Movement

* We optimized the memory allocation strategy when moving actors
* We optimized the AI pathfinding code

#### Input and Windowing

* The log and terminal windows can now be minimized and maximized
* The Unreal Editor log window position now persists through restarts
* You can now set the WinDrv.WindowsClient.DirectEnhancedPointerPrecision option to true to enable enhanced pointer precision when using DirectInput-based mouse input
* We backported UT 469's log window, which incurs far lower run-time overhead when logging

#### UnrealScript

* The game now plays a "drowning" sound rather than "hit underwater" sound when the player is under water and starts losing health ([#18](../../issues/18))
* We added a new console command, `stat fpos`, that configures the placement of the `stat fps` output relative to the top-right corner of the screen. See Default.ini: `FPSPosX` and `FPSPosY`
* We added a new console command `is_pi`, which returns 1 when running on a Raspberry Pi
* We have added more default screen resolutions to the Display menu
* We added a new native function, Actor.KRagdollExists, to check if a named ragdoll exists for the actor
* Dying players now play their death animation if they do not have a ragdoll
* We improved several of the error messages the game logs when encountering errors in UnrealScript code
* You can now set the MaxWarnPerFunc option in the [Core.System] section of the ini file to limit how many errors individual UnrealScript functions can log before the game silences them
* You can now add asset files (ogg/ka) to the package map using the Actor.AddToPackageMap function
* Several HUD and menu elements are now widescreen-aware and will scale correctly at 21:9, 16:9, and 16:10 resolutions. You can enable the widescreen-aware menu by setting the MainMenuClass to GUI2K4.UT2K4MainMenuWS in the [Engine.GameEngine] section of the game ini. Our installers will set this setting automatically
* The in-game console's command history now persists across game launches
* You can now configure the inactivity time and the effect spawned by weapon lockers
* Engine.Actor.GetHumanReadableName() now returns the plain class name rather than the instance name (which sometimes contains a number)
* Several Engine.PlayerController functions can now be called from static contexts
* The game now shows you the UnrealScript call stack when it logs an accessed none error
* The various frame rate limits can now be configured in the in-game menu
* We made the map voter load the map list much more quickly ([#89](https://github.com/OldUnreal/UT2004Patches/issues/89))
* We added an "All" game type to the server browser
* We added new aspect ratio scaled image style (`ISTY_AspectRatioScaled`) with alignment options for widescreen support
* We added widescreen main menu images for aspect ratios between 1.7 and ultra-widescreen
* The "join game" menu now remembers your last selected tab ([#126](https://github.com/OldUnreal/UT2004Patches/issues/126))
* The SkaarjPack.Invasion.ReduceDamage function now calls the super function to handle damage reduction for victims that do not belong to the same species as the damage instigators
* The bonus pack 2 maps are now in the lists of alternative ladder maps ([#136](https://github.com/OldUnreal/UT2004Patches/issues/136))
* The onslaught ladder should now appear in the single player menu ([#136](https://github.com/OldUnreal/UT2004Patches/issues/136))
* The tutorial maps in the single player campaign now have a thumbnail

#### Webadmin

* The webadmin map list page now shows a sequence number for the maps in the map cycle

#### Miscellaneous

* The game will no longer truncate log files when it crashes
* We added a KarmaPath setting to the [Core.System] section of the ini file
* The game now reads and writes human-readable text color codes from and to the ini file
* The Linux binaries now perform a case-insensitive file search when they cannot open required localization files
* The game now performs a case-insensitive file lookup when it can't find the music file it's supposed to play. This should fix issues with music not playing on Linux systems
* The game will now save screenshots in PNG format
* We increased the default cache size
* We optimized the code that saves your game configuration to INI files