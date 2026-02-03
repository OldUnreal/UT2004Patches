# OldUnreal Patch Repository for Unreal Tournament 2004

This is the public repository for [OldUnreal's](https://www.oldunreal.com/index.html) Unreal Tournament 2004 patches. OldUnreal took over maintenance of the Unreal Tournament code base after reaching an agreement with [Epic Games](https://www.epicgames.com) in 2025.

Our patches fix stability, security, and performance bugs in the game client, server and editor. They also add quality-of-life features and support for modern platforms and operating systems.

Patch releases hosted here are considered stable enough for widespread use, but they are by no means a finished product. We still release updates on a regular basis.

**Legal Disclaimer:** This project was approved by Epic Games, but it is not an official Epic project, nor has it been reviewed or tested by Epic.

## Downloads

This repository provides downloads for release previews and stable releases on the [Releases Page](https://github.com/OldUnreal/UT2004Patches/releases).
If you are an active tester who wants to test bleeding-edge changes and who can write top-quality bug reports, then please come talk to us on [Discord](https://discord.com/channels/143986633992175616/1053202987545264128) to join our internal testers team.

### Release Previews

Our release previews primarily target modders and beta testers who want to test our latest changes after they have passed the internal testing stage. These previews are considered relatively stable, but they may not work in online play.

### Stable Releases

If you are a regular player or if you want to play online, then please use stable releases only.

> [!IMPORTANT]
> If you want to test out our patches, but maintain the possibility to uninstall them, we strongly urge you to create a backup of your entire UT2004 folder before installing the patch.

> [!IMPORTANT]
> If you are installing our patch manually, you should update your game client to version 3369 and install the Epic ECE Bonus Pack first.
> If you use our installers, the necessary files will be installed automatically.

## Windows Installation

We distribute our patches for **Windows** systems in multiple formats. We recommend that you run the exe installer to patch your game.

However, you can also simply unpack the zip package **on top of an existing installation** of Unreal Tournament 2004. No other actions are needed to install the patch.

## Linux Installation

The **Linux** version of our patch is only available as a tarball. To install, unpack the tarball **on top of an existing installation** of Unreal Tournament 2004.

Alternatively, to spare you the pain of using Wine to install the Windows version, you can unpack our patch into an empty directory, which we will refer to as the **game directory**. You can then install the rest of the game as follows:

> [!NOTE]
> The directory names below are Case Sensitive!

1) **Mount** the UT2004 cd/image or unpack the GOG distribution with the **innoextract** tool. We will refer to the root directory of your game cd/image or GOG distribution as the **distribution directory**.
2) Copy the **Animations**, **Help**, **KarmaData**, **maps**, **Music**, **Prefabs**, **Sounds**, **Speech**, **StaticMeshes**, **Textures**, and **Web** directories from the distribution directory into the game directory.

> [!CAUTION]
> Please ensure that you do **NOT** copy the contents of the System directory in your cd/GoG image into the game directory, otherwise the game will not launch!

At this point you're all set. No other actions are needed to install the patch.

## macOS Installation

The macOS version of our patch comes as an application bundle. You should drag this bundle into your applications library. If you're installing our macOS patch for the first time, you will also need to copy the data files from an existing UT2004 installation into your Application Support Library. To install the data files, you need to do the following:
1. Open a new Finder window
2. Press ⇧⌘G to bring up the "Go to folder:" dialog
3. Enter "~/Library/Application Support/" (without the quotes!) in the edit box and click ok
4. Within the ~/Library/Application Support/ folder, create a new folder called "Unreal Tournament 2004" (without the quotes!)
5. Copy the **Animations**, **Help**, **KarmaData**, **maps**, **Music**, **Prefabs**, **Sounds**, **Speech**, **StaticMeshes**, **Textures**, and **Web** from your existing UT2004 installation into the folder you've just created

> [!CAUTION]
> Please ensure that you do **NOT** copy the contents of the original game's System directory into ~/Library/Application Support/, otherwise the game will not launch!

After installing the data files, you should be able to launch the UT2004 app!

## Updating Existing Server Installations

> [!CAUTION]
> If you are currently using any mutator or server actor to report to multiple master servers, remove them. They are unlikely to work any longer due to changes in class `MasterServerUplink`, and should not be necessary.
> You should, however, make the following changes to your server configuration file (e.g., UT2004.ini):
> 1. In [Engine.GameEngine] section, you should replace `ServerActors=IpDrv.MasterServerUplink` with `ServerActors=IpDrv.MasterServerLauncher`
> 2. in [IpDrv.MasterServerLink] section, you **must** have at least one entry in the MasterServerList, whether or not you want to be actively listed ([IpDrv.MasterServerUplink]->DoUplink=True/False). Populate the list with each master server you may wish to report to. Examples:
> - `MasterServerList=(Address="utmaster.openspy.net",Port=28902)`
> -	`MasterServerList=(Address="ut2004master.333networks.com",Port=28902)`
> - `MasterServerList=(Address="ut2004master.errorist.eu",Port=28902)`

## System Requirements

Windows and Linux systems need a 64-bit Intel CPU or 64-bit ARM CPU.

Windows systems need to run Windows 7 or later.

Linux systems need to run a fairly recent distribution. The patch was developed on Ubuntu 24.04.

macOS systems need a 64-bit Intel or Apple Silicon CPU and macOS Catalina (10.15) or later. Some rendering features may be unavailable on macOS.

## Features

Besides fixing hundreds of bugs, the OldUnreal UT2004 patches currently also add features such as:
* Full 64-bit support
* SDL3-based window management for the Linux and macOS clients
* UTF-8 support for game ini, int, and log files
* PNG screenshots
* Widescreen fixes
* An updated in-game server browser with lots of quality-of-life improvements

We will update this list as we add more features.

A full list of patch features and changes is available in the [Release Notes](https://github.com/OldUnreal/UT2004Patches/blob/master/ReleaseNotes.md). 

## Malware Warnings

> [!IMPORTANT]
> Our Windows and macOS binaries are digitally signed, but malware/virus scanners may occasionally still flag them as potential malware because our signing certificate is still building up reputation. Additional information can be found [here](https://www.digicert.com/blog/ms-smartscreen-application-reputation/). 

## Donations

> [!NOTE]
> We are all volunteers who work on Unreal, Unreal Tournament, and Unreal Tournament 2004 in our spare time. If you like our work, then please consider making a small donation [here](https://www.oldunreal.com/phpBB3/donate). Please make sure to mention Unreal Tournament 2004 in your donation note!

## Bug Reports

You can use our [issue tracker](https://github.com/OldUnreal/UT2004Patches/issues) to file bug reports. Reasonable feature requests for Unreal Editor, as well as requests for quality-of-life improvements for the game can also be posted there. 

> [!IMPORTANT]
> Before filing a bug report, please use the GitHub search function to see if someone else has already reported the same issue. If you find an issue that looks similar to yours, then please submit a comment in the existing issue report.
> When filing a bug report, please include relevant details about your setup (i.e., your operating system and version, your UT2004 version and build date, mods you are using) and describe how we can reproduce the problem.

## Credits

The primary developers for OldUnreal's Unreal Tournament 2004 patches are (in no particular order): [AnthraX](https://github.com/stijn-volckaert), [Higor](https://github.com/CacoFFF), [Buggie](https://github.com/SeriousBuggie), [Dots](https://github.com/Marco888), [Smirftsch](https://github.com/Smirftsch), [Metallicafan212](https://github.com/Metallicafan212), [Deaod](https://github.com/Deaod), and [Piglet](https://github.com/ukpiglet).

We also want to express our sincerest gratitude to the following people:
* Stacey Conley (aka "Flak"): this project would not have happened without her. Thank you Stacey, you are amazing!
* Wormbo and Shambler: for the multitude of fixes they implemented between versions 3369 and 3374
* Ryan C. Gordon (aka "icculus"): for invaluable advice, bug fixes and improvements, and work on the updated SDLDrv. If you like Ryan's work, then please consider [supporting him](https://www.patreon.com/icculus)
* Rejecht: for the many bug reports on unrealarchive.org