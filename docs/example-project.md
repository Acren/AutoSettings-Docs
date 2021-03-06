The example project contains a fully configured menu showing off a typical integration of the plugin.

[All versions of the project are available here](https://goo.gl/qHDb2Y)

In general you should use the example project that is the same version as the plugin, or if there if that doesn't exist, the next lowest.
For example if you had plugin version *1.2.1*, there is no example project with that exact version so the correct example project to use would be *1.2*.

[View compatibility of specific versions here](/versions)

# Migrating assets from the example project

If you want to use assets or the entire menu from the example project, you can migrate them to your own project.

[The entire process is shown in this video](https://www.youtube.com/watch?v=eL02UKsATZ4)

1. With your own project closed, copy the `[/Script/AutoSettings.AutoSettingsConfig]` category in the following config file, including all of its entries, from the example project to your own.
	- If UE 4.20 or later: **Config/DefaultGame.ini**
	- If UE 4.19 or earlier: **Config/DefaultEditorPerProjectUserSettings.ini**
2. Also copy tag definitions in **Config/DefaultGameplayTags.ini** to your own project.
3. In the example project, right click and Migrate the **SettingsUI** widget to your project. This will also copy all of the styled widgets that are used.
4. Also migrate the **ButtonIcons** directory if you want to use the icons from the example project.
5. Open your project and ensure the AutoSettings plugin is enabled
6. Place the SettingsUI widget in your existing menu or add a way to open it. (See the **DemoPlayerController** Blueprint in the Example Project)
7. Configure inputs on the **InputSettingsPage** for the input actions and axes in your own project.

# Example project custom settings and CVars

While the example project exposes a lot of CVars that are part of Unreal Engine by default (such as the scalability settings), the following settings in the example project are game-specific and not part of Unreal Engine by default, so if you want to use any of them in your own project the functionality needs to be integrated, otherwise the settings in the UI won't do anything.

These are all implemented in the example project for demonstration purposes and are not required to use the plugin, they are fully optional.

**All of the different custom CVars in the example project are registered in the DemoGameInstance Blueprint. Some of them are also implemented in DemoGameInstance, and some in other Blueprints.**

[View documentation about registering and implementing custom CVars here](/settings/#console-variables)

## Audio Levels
CVars: `GameAudio.MasterVolume`, `GameAudio.MusicVolume`, `GameAudio.SFXVolume`  
Implemented in: ***DemoGameInstance***

These settings are an example of how to control audio levels. Your project might have different categories, but the fundamentals will be the same. They need to be hooked up to the appropriate **Sound Class** and **Sound Mix** assets for your project. 
[Read more about audio levels](/settings/#audio-levels)

## Icon Set
CVar: `Game.IconSet`  
Implemented in: ***DemoGameInstance***

This setting globally controls the key icon sets used for the game, using the Auto Settings input systems. This can be used to allow PC players to choose what type of Gamepad icons they see.

## Sensitivity
CVars: `Input.Sensitivity`  
Implemented in: ***DemoPlayerController***

This setting controls input sensitivity by setting Input Scale variables on the Player Controller.

## Field of View
CVar: `Camera.FOV`  
Implemented in: ***DemoCharacter***

This settings controls Field of View on the Character's camera. If you have multiple cameras on different Blueprints, you may want to apply the FOV settings to each of them, or on a base class, or use separate settings. (For example, you could have a Vehicle FOV setting as well)

## Character debug settings
CVars: `Character.GravityScale`, `Character.WalkSpeed`  
Implemented in: ***DemoCharacter***

These are example settings showing how control arbitrary gameplay variables. You likely wouldn't want these in your own project unless they are for debugging.


