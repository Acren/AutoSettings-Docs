The example project contains a fully configured menu showing off a typical integration of the plugin.

[All versions of the project are available here](https://goo.gl/qHDb2Y)

In general you should use the example project that is the same version as the plugin, or if there if that doesn't exist, the next lowest.
For example if you had plugin version *1.2.1*, there is no example project with that exact version so the correct example project to use would be *1.2*.

[View compatibility of specific versions here](/versions)

# Migrating assets from the example project

If you so wish, you can migrate assets or the entire menu from the example project to your own.

[The entire process is shown in this video](https://www.youtube.com/watch?v=eL02UKsATZ4)

1. With your own project closed, copy the `[/Script/AutoSettings.AutoSettingsConfig]` category, including all of its entries, in **Config/DefaultGame.ini** from the example project to your own.
2. Also copy tag definitions in **Config/DefaultGameplayTags.ini** to your own project.
3. In the example project, right click and Migrate the **SettingsUI** widget to your project. This will also copy all of the styled widgets that are used.
4. Also migrate the **ButtonIcons** directory if you want to use the icons from the example project.
5. Open your project and ensure the AutoSettings plugin is enabled
6. Place the SettingsUI widget in your existing menu or add a way to open it. (See the **DemoPlayerController** Blueprint in the Example Project)
7. Configure inputs on the **InputSettingsPage** for the input actions and axes in your own project.

Any implementations of project-specific custom settings that you want to use should also be implemented in or copied to your own project as the CVars are not included in the engine by default.
These are all implemented in the Example Project for demonstration purposes and are not required to use the plugin, they are fully optional.

In the example project the following setting CVars are custom:

Registered and implemented in DemoGameInstance:

- Game.IconSet
- GameAudio.MusicVolume
- GameAudio.SFXVolume

Registered in DemoGameInstance and implemented in DemoCharacter:

- Camera.FOV
- Character.GravityScale
- Character.WalkSpeed

[View documentation about registering and implementing custom CVars here](/settings/#console-variables)
