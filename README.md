# Auto Settings Documentation

**Auto Settings** is a game options and input binding toolkit for **Unreal Engine 4** that supports a range of functionality that is standard in modern PC and console games.

It is designed be as fast and simple as possible to use, building on top of and enhancing Unreal's systems so that it is painless to integrate with existing projects.

![Image](/images/image12.png)

## Current Features

- Using this plugin to create settings and input binding menus requires no c++ and even no blueprint nodes, simply add the plugin to your project and start placing setting widgets in your UMG menus
- Example menu with common settings that you can copy to your own project if you choose
- Settings and input mappings load, save and apply automatically using Unreal's built in config .ini system, console variable system, and input system
- UI is modular can can be substituted with your own widgets and styling, preserving the functionality underneath

Settings:
- Built on top of Unreal's console variable system
- Defining a new setting is as simple as placing a new widget in your menu and choosing which console variable it is for
- Choose from any of the hundreds of built in console variables such as VSync, resolution, window mode, scalability settings, etc - these hook up automatically, no c++ or blueprint nodes are required for engine console variables
- Ability to define new console variables, access their values, and bind events that are called when they change, in c++ or in blueprint - so that you can create any additional settings you need that Unreal doesn't have by default
- Choose whether settings should automatically save when they are changed, or allow the user to manually apply, save, or cancel changes
- Multiple ready-to-use widgets such as Radio Select, Slider, ComboBox, Spinner, and CheckBox which can be dragged into your menu, link with the settings automatically, and can be restyled to match your game's theme
- Ability to make your own widgets that extend the system for more specific cases

Input mapping and binding:
- Actions and axis can be rebound by players at runtime
- Built on top of Unreal's input system and will work out of the box with your project - keep defining and using actions and axis like you are used to
- Adding a new input to your menu is as simple as placing a new widget and choosing which action or axis it is for
- Inputs can be mapped and stored separately for each local player in a single game instance
- Supports multiple bindings for the same action (such as "Primary" and "Secondary"), which can also be separated by key groups such as Keyboard and Gamepad
- Ability to create multiple presets which players can switch between
- Ability to whitelist or blacklist specific keys from being bound
- Supports key modifiers (Yes, you could let the player bind Jump to Ctrl + Shift + Mouse Wheel Down if you really want)
- Supports inverting axes
- Choose whether binding a new key should keep or remove other bindings with the same key

Input key icons:
- Key icon system for optionally displaying inputs as icons instead of text
- Easily access icon or text label for an input anywhere in your project so that your UI and prompts always shows the correct inputs
- Ability to define different icon sets for different platforms or gamepad types such as XBox and PlayStation and switch between them on the fly
- Ability to define different variants of icons such as small and large that can be used in different places in your project

## UMG Widgets

After the Auto Settings plugin has been added to your project and enabled in the Plugins menu, the only step required to create basic setting and input binding menus is to add widgets to your menu.

![Image](/images/image21.png)

If the Auto Settings plugin is installed correctly, you’ll find new categories in the UMG widget palette: 

- **AutoSettings Generic Controls** contains custom controls that are later extended to be usable as settings. These widgets are independent of any settings-specific logic and might be useful anywhere in your project, not just in your settings menu.

- **AutoSettings Input** contains widgets used for runtime input binding.

- **AutoSettings Setting Controls** contains controls (Both native UMG controls and also custom controls) that have been extended to be used in a settings menu. These can be tied to Console Variables to automatically apply when changed, and can save to config to be loaded and applied when the game is launched again.

Different settings controls with basic styling applied:
![Image](/images/image8.png)

## Settings

To add a setting to your menu, place the widget for the desired control type from the **AutoSettings Setting Controls** category anywhere in your menu.

> Tip: It can be nice for layout purposes to wrap settings in a new *Setting Row* widget which consists of label text and a Named Slot to contain the control widget itself (See example project) but you are free to set up the layout of your menu whichever way works best for you.

![Image](/images/image15.png)

All settings have the following editable properties:

- **CVar Name** is the name of the console variable to expose - this can be a built-in Unreal console variable such as a scalability setting or vsync, one declared specifically for your project, or even one declared in another plugin if applicable.
*See **Console Variables** section.*

- **Value Mask** (optional) is a subclass of the **SettingValueMask** class used to split console variables into multiple independent settings in your menu.
*See **Value Masks** section.*

- **Auto Apply** - If true, the setting will automatically apply and call the console variable with the new value when the user changes the selection. If false, will need to be done manually with the Apply function.

- **Auto Save** - If checked, the setting will automatically update the config with the new value when the user changes the selection. If false, will need to be done manually with the Save or Cancel functions. Saved settings are stored in the **Settings.ini** config file.

### Select Controls

**Select** controls are controls with multiple named options for the user to select from.
These include the **ComboBox**, **Radio Select**, and **Spinner**.

![Image](/images/image22.png)

These settings have properties to determine which options they should allow.

- The **Options** property allows options to be predefined at design time, the **Label** being the text that the user sees and the **Value** being the internal value that is set on the console variable when selected. 
If an option has no Value, it instead defaults to use the index of the option, which is useful when creating settings for scalability variables which take integers.

- The **Options Factory** property (optional) is a subclass of the **SettingOptionFactory** class which can be used to dynamically construct a list of options for the setting by overriding the **ConstructOptions** function. For example, **ResolutionOptionFactory** constructs a list of all fullscreen resolutions that are supported by the system running the game.

### Applying and Saving Manually

You might not want to have your settings automatically apply or save when the user changes them.

In this case, you can uncheck the **Auto Apply** and **Auto Save** properties on the settings, and instead call the **Apply**, **Save**, and **Cancel** functions on the setting widgets manually.

You would likely want to call these functions when other buttons in your UI are pressed.

![Image](/images/image14.png)

There is also a pure function called **HasUnsavedChange** which can be used to determine if a save button should be clickable, or to display a prompt to the user asking if they want to discard unsaved changes.

To make life easier, there are also versions of these functions that operate on multiple settings at the same time.

![Image](/images/image16.png)

These functions operate on all the child settings in the layout of the User Widget (Blueprint widget) they are being called from, including settings in Named Slots. You can specify a User Widget to use instead, and also filter for settings that are underneath a specific parent widget, which might be useful if your menu has separate pages in the same User Widget which should be applied and saved independently from each other.

### Console Variables

Auto Settings is built on top of Unreal’s Console Variable (CVar) system, so adding a new setting always requires a CVar to exist for that setting. Unreal has hundreds of CVars built in which can be exposed with Auto Settings.
For a full list, check **Help > Console Variables** in the editor.

There are cases in which you might want to expose something as a setting that isn’t built into Unreal by default, for example audio levels.

There are a few components to doing this:
1. Registering the CVar
2. Using the CVar to control something in the game
3. Adding a setting for the CVar (already covered)

Registering and using CVars in c++ is covered in Epic’s documentation [here](https://docs.unrealengine.com/latest/INT/Programming/Development/Tools/ConsoleManager/index.html).

There are also functions in this plugin to expose this to Blueprint, so I’ll outline them here.

Registering CVars is best done as early as possible, so unless you can use c++ I would suggest doing it in your GameInstance class in the **Init** event.

![Image](/images/image10.png)

Here you can call functions to register float, integer, or string CVars.
It’s also worth noting that these functions also check the settings config to see if there is a value stored, in which case that value is loaded instead of the default value parameter.

You can call these functions anywhere, but Init is the earliest point in Blueprint.
To actually make your new CVar do something, you’ll need to make your game check the CVar or respond to it in some way.

To check the value you can use the getter functions like this anywhere in your game:

![Image](/images/image13.png)

However in most cases you will want to have your game respond to the CVar and execute something when it changes, such as updating the audio volume.

This can be done by adding callback events which are fired when the CVar changes so that your game can respond to them.

![Image](/images/image17.png)

In this case we’re setting a sound mix’s volume to the value of the CVar whenever it is changed. If **Callback Immediately** is checked, the event will be fired with the current CVar value as soon as the callback is added, making it easier to apply the correct value when the game is launched or an object is constructed.

You can also register and bind a callback for a CVar at the same time, making it easier to organise your Blueprint if the CVar is being used in the same place it is being registered.

![Image](/images/image9.png)

If this is set up correctly, the CVar should be registered, loading it’s value from the config if it is saved, and having some effect on the game when it is changed through the console. The only other thing that needs to be done is adding a menu setting to let the user control it as explained in the **Adding Settings** section.

Check the example project for full implementation of custom CVars to control gameplay elements and audio levels.

### Value Masks

**Value Masks** can be used to split console variables into multiple independent settings in your menu.

Any Auto Settings setting control can optionally use a Value Mask by setting the **Value Mask** property to a subclass of the **SettingValueMask** class that determines how the value of the console variables should be split and recombined.

![Image](/images/image4.png)

Example usage might be splitting the **r.SetRes** console variable - which contains both resolution and window mode in the form of *1920x1080wf* - into two separate settings, one controlling the resolution and the other controlling the window mode.

The plugin includes subclasses for splitting r.SetRes into resolution and window mode called **ResolutionValueMask** and **WindowModeValueMask**, but more subclasses can be created in either c++ or Blueprint to handle other cases.

The subclass should override the following two functions:

1. The first is the **Mask Value** function, which determines how to convert the console variable value into a format that the setting cares about.

For example the Mask Value function of ResolutionValueMask would take the input value of *1920x1080wf* and return *1920x1080*.
WindowModeValue Mask would just return *wf* (short for windowed fullscreen).

![Image](/images/image2.png)

2. The second function is the **Recombine Values** function, which determines how to integrate the setting value back into the console variable value.

In the case of ResolutionValueMask, this would take the current r.SetRes console value, for example *1920x1080wf*, and substitute in a modified resolution value, such as *2560x1440*, combining them into *2560x1440wf* which would form the new console value.

In the WindowModeValueMask subclass, this would take the *1920x1080wf* console value, and substitute a modified setting value for window mode such as *f* (fullscreen), creating the final console value of *1920x1080f*.

![Image](/images/image19.png)
