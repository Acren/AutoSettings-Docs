***Why don't settings save when running Standalone mode from editor?*** 

By default Unreal disallows saving config from standalone mode, changes are not saved to config (but works fine in editor and packaged). If you go to **Editor Preferences > Level Editor - Play > Play in Standalone Game**, expand the advanced settings, and in **Additional Launch Parameters** put in `-MultiprocessSaveConfig`

This should allow standalone mode to save config and thus your settings will be saved.

***Can I use the menu from the example project? How do I integrate it with my project?***

You can. Open the example project for the version of the plugin that your project is using, right click and Migrate the **SettingsUI** widget to your project. This will also copy all of the styled widgets that are used. You should then place the SettingsUI widget in your existing menu or add a way to open it. (See the **DemoPlayerController** Blueprint in the Example Project)
You should also be aware that project settings won't be copied with the menu assets, so it's worth comparing the **AutoSettings** page with your own.

***Does the example project have gamepad navigation?***

Not yet. I'd like to do this eventually, but haven't had time yet.