# JETModUpdater

[Jump to download link](#Download)

# Functionality:
* Configurable update settings per-mod.
* Easy to understand configuration.
* Logs errors and warnings to the console for update debugging.
* Clears the cache before starting the JET server.


# Installation:
1. Download the latest version using the link at the bottom of this post.
2. Place the exe file in your JET server folder (the same location as the Server.exe file).
3. Run Launcher.exe and watch the magic happen!


# Configuration:
**<ins>For Chads (players)</ins>**

Mods configured to auto update using this program will have at least the following two extra options in the mod.config.json file.
```
"autoUpdate": true,
"checkUpdateUrl": "https://example.com/mymod/updater.json"
```

**autoUpdate:** If set to true, the mod will automatically update when an update is detected. Set to false if you would like to disable automatic updates for the specific mod.

**checkUpdateUrl:** Set by the creator of the mod. This is the file the program will reference to determine if the mod is up to date, and where to download the new version if it requires an update.


**<ins>For Rats (mod creators)</ins>**

To configure your mod for automatic updates, you will need to add a couple things to your mod.

First thing's first, let's create a file named "updater.json" and place it inside your mod folder. Inside of this file, we need to put some parameters that will give the program information that is important for determining if the mod is up to date and where to download the update if it's not. This file is not needed on the client, so it may be separate from the mod or added to the "excludeFromUpdate" property if desired.

```
{
	"name": "Mod Name",
	"author": "Author Name",
	"version": "1.0.0",
	"forceDowngrade": false,
	"downloadUpdateUrl": "https://example.com/",
	"excludeFromUpdate": [
		"readme.md"
	]
}
```
**name:** The name of your mod. This must be the same name that is specified in your mod.config.json

**author:** Your author name. This must be the same author that is specified in your mod.config.json

**version:** The current version of the mod. This is what the program checks to determine if the mod needs updated. The version can not contain any letters or symbols. This parameter can be anywhere from 1 to 4 numbers separated by a period. Each number can be any positive value under 214483647.

**forceDowngrade:** If set to true, the program will download the version specified in this file even if it's lower than the installed version. If the version specified in this file is the same as the installed version, the program will not download the file.

**downloadUpdateUrl:** Direct download link to the zip file containing the updated version of the mod. The structure of the zip file does not matter, as long as there is only one mod.config.json file and all files required by the mod are either in the same folder as the mod.config.json file or in a deeper subfolder.

**excludeFromUpdate:** This is a list of files to exclude when updating. Each of the specified paths are appended to the root folder of your mod, which is where your mod.config.json is stored. For example, if I have a folder named Config in my mod folder that contains a file named settings.json that I do not want to overwrite during the update process, I can add "Config/settings.json" as an entry to "excludeFromUpdate". You can exclude both files and entire folders.



After you've done that, it's time to add the following lines to your mod.config.json file:

```
"autoUpdate": true,
"checkUpdateUrl": "https://example.com/mymod/updater.json"
```

**autoUpdate:** This should be set to the user. If set to false, the program will not update the mod even if a newer version exists.

**checkUpdateUrl:** The URL to the raw "updater.json" file you just created. This URL should always stay the same. It is crucial that this link is accurate for the program to work. If you are hosting your mod on GitHub, you will need to go to the file and click the "raw" button in order to get a working link.

For debugging purposes I have added a "-debug" argument that pauses the program right before starting the JET server to make it easier to read the output. To use this feature, either open a command prompt or PowerShell window in the same directory as your "Launcher.exe" folder and type the command "launcher.exe -debug", or create a batch (.bat) file in same directory and paste the same command into the file.

Note: Although it is recommended for these 2 files to be separate, all of the options can be in the mod.config.json as long as "checkUpdateUrl" is pointed to it, and "downloadUpdateUrl" is accurate.

For support, join the [ConfigFreaks Discord server](https://discord.gg/5jf5aaB).

# Download
[Latest Update (1.0, initial release)](https://github.com/AppeazeTheCheese/JETModUpdater/releases/download/1.0.0/Launcher.exe)

Patch Notes:
* Initial release
