# Compatibility

Each plugin version is released to support the latest engine version only.

New example project versions are sometimes released with plugin versions where applicable.
The example project does not always need to match, but it is recommended to use the most recent example project at the time that plugin version was released.

Plugin | Engine | Example Project
------ | ------ | ------------
1.4    | 4.20   | 1.4
1.3    | 4.19   | 1.3
1.2.4  | 4.19   | 1.2.2
1.2.3  | 4.19   | 1.2.2
1.2.2  | 4.19   | 1.2.2
1.2.1  | 4.18   | 1.2
1.2    | 4.18   | 1.2
1.1.1  | 4.18   | 1.1.1
1.1    | 4.17   | 1.1
1.0    | 4.17   | 1.0

# Release Notes

## 1.4

- UE 4.20 now supported
- Plugin developer config (AutoSettings page in Project Settings) converted to use *Game* category instead of *EditorPerProjectUserSettings* category

**Important note:** Because of the config category change, projects upgrading from older versions of the plugin will have to move or copy the `[/Script/AutoSettings.AutoSettingsConfig]` category, including all of its entries, from `YourProject/Config/DefaultEditorPerProjectUserSettings.ini` to `YourProject/Config/DefaultGame.ini` to retain existing config values.

## 1.3

New:

- Added option to disable automatic player input initialization in plugin settings and call it manually using `InitializePlayerInputOverrides`.
- Added the ability for projects to override how the plugin uniquely identifies players for storing inputs by implementing the AutoSettingsPlayer interface on PlayerController - by default it still uses the Controller ID of the local player.
- Slider setting no longer auto-saves every delta while the handle is being dragged, which was performance heavy as it was writing to config each time. Now it can still auto-apply while the handle is being dragged, but only auto-saves once the handle is released.
- Added option to control sensitivity of mouse-axis binding, specifying how far the mouse must move before it is registered.
- Added the ability to manually add input overrides using `AddPlayerActionOverride` and `AddPlayerAxisOverride`.
- Added the option for projects to specify special escape keys that cancel input binding without capturing anything.
- Added `HasUnappliedChange` to settings. Previously you could only check `HasUnsavedChange`.
- Saving a setting automatically applies it if it hasn't been already. This removes the possibile state of having saved but unapplied changes.

Fixed:

- Setting widgets now read their initial value from their applied console variable if available instead of saved config. This fixes the unintended behaviour of settings showing the saved value instead of the applied value where the two differ.
- Fixed a bug with input binding where left mouse button would register as none / invalid if pressed within a second or so of the prompt opening.
- Fixed bug with some saved settings such as max FPS being overridden by engine initialization. Saved setting values are now applied after engine initialization so that they take precedence over engine values.
- Fixed Cancel reverting the setting to the applied value. It now reverts to the saved value instead.
- Fixed issues while saving settings with masked values (e.g. Resolution / window mode) recombining with applied values instead of saved values.
- Fixed settings with unapplied changes being incorrectly reverted when any console variable is changed, including other settings

Example project:

- Split each page of settings into their own widgets, making them easier to manage.
- Added UI to video settings page to demonstrate manual save / apply / cancel functionality.
- Added gamma setting to video settings.

## 1.2.4

- ComboBox setting now chooses not to apply or save settings when the selection is changed externally - this fixes a crash that could happen when constructing new widgets
- Fixed a crash when external code tries to register CVar change callback delegates that are already registered - warn instead

## 1.2.3

- Fixed crash in multiplayer in 4.19 due to trying to initialize input mappings when a PlayerController does not have a valid PlayerInput
- Fixed "Allow multiple bindings per key" option not taking effect

## 1.2.2

- UE 4.19 now supported

## 1.2.1

- Fixed category-related errors from 1.2 upon packaging the game with the installed plugin
- Fixed crash with extra clients in multiple-process play in editor

## 1.2

New:

- Added the ability to dynamically prioritize between different Key Groups for action and axis labels. Set this by calling "Set Player Key Group", or "UInputMappingManager::SetPlayerKeyGroupStatic" in code. Example usage for this would be automatically switching input prompts between gamepad and keyboard & mouse when the player changes input mode.
- To support dynamic Key Group priorities, an empty tag for Key Group now represents "any" rather than the keys that are not used by any other key group. Projects with a gamepad key group will now also probably want a key group for keyboard and mouse. The keys used for prompts using an empty/any key group will be dynamically selected based on the player's Key Group.
- Similarly, a Mapping Group of -1 represents "any". 0 is still the first mapping group, 1 the next, etc.
- Added an easy "Use non-gamepad keys" option to Key Group so that users don't have to add every single key to a key group for keyboard and mouse.
- Added the ability to bind mouse axes so that users can re-bind "look" inputs. Mouse axes can be blacklisted to revert to old behavior.
- All BindWidget properties are now read-exposed to Blueprint. This means you can now access the internal control of a setting without needing to use code.
- Exposed "Is CVar Registered" function to Blueprint.

Fixed:

- Fixed error logs caused by ActionLabel trying to create widgets at design time.
- Fixed warning logs caused by trying to register a setting for a CVar that already exists when the game is run past the first time in an editor session.
- Converted plugin to IWYU to decrease compile times

Example project:

- Removed the first Input page with Primary/Secondary columns, now there is a single Input page with Keyboard/Gamepad columns. This is still supported by the plugin but there were too many edge cases related to supporting multiple input layouts in the same project in parallel and in the end it was not worth the extra maintenance cost and complication that it would have to add to the plugin.
- Added look and turn inputs to the input menu now that mouse axes can be bound.
- Added more mappings to the "Alternate" preset.
- Gamepad Right Stick Up and Down are now mapped to axis scales -1 and 1 respectively instead of 1 and -1. This is because the right stick Y axis has the opposite values of the left stick and I didn't realise when initially setting it up.
- Added video setting for Max FPS.

## 1.1.1

- UE 4.18 now supported

## 1.1

- Added a function on Slider Setting called when its value changes. This allows users to easily have a text label reflect the value.
- Added tooltip to option value explaining that it falls back to the array index if blank
- Added new settings to example project:
	- View distance quality
	- Foliage quality
	- Field of view
	- Motion blur quality
	- Bloom quality
- LoadingPhase set to Default - previously on PostEngineInit to support logic that has since been changed
- Fixed category errors when packaging
- Fixed crash from widgets attempting to apply or save settings during design time

## 1.0

- Initial plugin release supporting 4.17