Settings are saved to the `Settings.ini` config file in the `[Settings]` section. Input bindings are saved in `Input.ini` in the `[/Script/AutoSettings.InputMappingManager]` section.

Unreal saves config files to different directories depending on the configuration:

Context                       | Config directory
----------------------------- | ------------------
Editor:                       |**`<Project directory>\Saved\Config\<Platform>`**
Development and Debug builds: |**`<Package directory>\Saved\Config\<Platform>`**
Shipping builds:              |**`AppData\Local\<Project name>\Saved\Config\<Platform>`**