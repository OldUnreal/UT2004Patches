# Unreal Tournament 2004 Release Notes

## General Information

### Official Unreal Tournament Web Sites

* [Unreal Tournament Home Page](https://www.unrealtournament.com)
* [Epic Games Home Page](https://epicgames.com)
* [Unreal Engine Technology Page](https://www.unrealengine.com)

### Independent Unreal Tournament Web Sites and Discord servers

* [OldUnreal site](https://www.oldunreal.com) / [OldUnreal Discord](https://discord.com/channels/143986633992175616/1053202987545264128)
* [MiA Forums](https://www.miasma/rocks)  / [MiA Discord](https://discord.gg/CxdXaEauya)
* [CEONS Forums](https://ceonss.net/) / [CEONS Discord](https://discord.com/channels/310878149158240257/310878149158240257)

## Unreal Tournament 2004 Version 3374 Release Notes

Version 3374 is completely network compatible with the previous public release of UT2004 (3369). 

### Patch Highlights

* We dropped support for 32-bit CPUs, for old versions of Windows (i.e., Vista or earlier), and for DirectX 8
* We now natively support Linux and macOS systems with x86_64/amd64 and arm64/aarch64 CPUs 
* The Windows version of the game now requires DirectX 9
* The Linux and macOS versions now use SDL3 instead of SDL1
* You can now play the game or run a server on a Raspberry Pi 4 or 5, albeit at rather slower frame-rate than on a PC!
* We dealt a first (minor) blow to the editor goblin! Unreal Editor will no longer freeze for several seconds when clicking a viewport

### Stability Improvements

#### Unreal Editor

* We fixed a bug that made Unreal Editor crash when converting meshes to brushes

#### UnrealScript

* The game should no longer crash if you click a tab in an in-game menu whose content is still being rendered

#### Miscellaneous

* We fixed a bug that made the game crash when reading an Unreal package with an unexpected GUID

### Bug Fixes

#### Unreal Editor and UCC

* The procedural sound context menus should now be fully functional
* The display checkbox for placeables actors in the actor browser should now work as expected
* We fixed a bug that made Unreal Editor create dummy packages when converting static meshes to or from brushes
* Unreal Editor now saves viewport sizes correctly even when viewports are minimized
* Large .int files are now saved correctly without truncation ([#12](../../issues/12))
* The UnrealScript compiler now parses and compiles scripts in the correct order after it processes `dependson` directives

#### UnrealScript

* We fixed a plethora of accessed nones and UnrealScript-based exploits, crash bugs, and denial-of-service attacks (Thank you Wormbo and Shambler!)
* We fixed a bug that could make the SPMA camera explosion loop without stopping ([#24](../../issues/24))
* The PlayerController.AskForPawn function now jumps to the Spectating.Begin state correctly ([#10](../../issues/10))
* The PlayerController.ToggleScreenShotMode function no longer discards user preferences such as the weapon handedness, crosshair visibility, HUD visibility, and the TeamBeaconMaxDist and bHideVehicleNoEntryIndicator settings ([#11](../../issues/11))
* The DeathMatch.InitTeamSymbols function can no longer give multiple teams the same symbol ([#16](../../issues/16))

#### Networking and Netcode

* The game now reports the correct progress percentage when downloading files from a game server

#### Miscellaneous

* We now support command lines longer than 1024 characters

### Enhancements

#### Unreal Editor

* The Unreal Editor window no longer minimizes when testing a map
* The properties window now supports mouse wheel scrolling
* You can now expand and collapse items in the properties window using keyboard arrows
* The music browser now supports ogg files

#### Networking and Netcode

* Download messages now include information about the number of packages to download and the percentage of total download completed
* The game client now downloads and collates game server information from multiple master servers
* Game servers can now connect to multiple community master servers
* You can now configure the UCC server query port number for admins. See [here](https://github.com/ukpiglet/UDPRelay) for an example of how this can be used on a Windows based UCC server

#### Audio and 3D Rendering

* Full screen support is now available in the 64-bit Windows client
* You can now cap your frame rate for menus and for offline games using the MaxMenuFrameRate and MaxOfflineFrameRate settings (see Default.ini)
* The player model now renders in mirror reflections
* Vertex models now render in OverlayMaterial

#### Input and Windowing

* The log and terminal windows can now be minimized and maximized
* The Unreal Editor log window position now persists through restarts

#### UnrealScript

* A "drowning" sound now plays, rather than "hit underwater" sound, when underwater and losing health ([#18](../../issues/18))
* We added a new console command, `stat fpos`, that configures the placement of the `stat fps` output relative to the top-right corner of the screen. See Default.ini: `FPSPosX` and `FPSPosY`
* We added a new console command `is_pi`, which returns 1 when running on a Raspberry Pi
* We have added more default screen resolutions to the Display menu

#### Miscellaneous

* The game will no longer truncate log files when it crashes
* We added a KarmaPath setting to UT2004.ini