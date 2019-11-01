***Why don't settings save when running Standalone mode from editor?*** 

By default Unreal disallows saving config from standalone mode, changes are not saved to config (but works fine in editor and packaged). If you go to **Editor Preferences > Level Editor - Play > Play in Standalone Game**, expand the advanced settings, and in **Additional Launch Parameters** put in `-MultiprocessSaveConfig`

This should allow standalone mode to save config and thus your settings will be saved.

***Can I use the menu from the example project? How do I integrate it with my project?***

You can. See the [example project page.](/example-project/#migrating-assets-from-the-example-project)

***Does the example project have gamepad navigation?***

Not yet. I'd like to do this eventually, but haven't had time yet.

***Why does the example project have empty values for the scalability settings, is this okay?***

The value falls back to the index of the array if empty, which makes it a bit faster to create scalability settings as they use 0 for low, 1 for medium, etc.

***Where do settings get saved?***

Settings are saved to the `Settings.ini` config file in the `[Settings]` section. Input bindings are saved in `Input.ini` in the `[/Script/AutoSettings.InputMappingManager]` section.

Unreal saves config files to different directories depending on the configuration:

Context                       | Config directory
----------------------------- | ------------------
Editor:                       |**`<Project directory>\Saved\Config\<Platform>`**
Development and Debug builds: |**`<Package directory>\Saved\Config\<Platform>`**
Shipping builds:              |**`AppData\Local\<Project name>\Saved\Config\<Platform>`**

***Does this work on Linux?***

Linux isn't officially supported or tested as a target platform, but everything in the plugin works across platforms and in fact multiple users have confirmed full compatibility.
To allow the plugin to compile on Linux, you need to add Linux to the WhitelistPlatforms in the `AutoSettings.uplugin` file.