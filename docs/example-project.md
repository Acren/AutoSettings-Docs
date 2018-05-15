The example project contains a fully configured menu showing off a typical integration of the plugin.

[All versions of the project are available here](https://goo.gl/qHDb2Y)

In general you should use the example project that is the same version as the plugin, or if there if that doesn't exist, the next lowest.
For example if you had plugin version *1.2.1*, there is no example project with that exact version so the correct example project to use would be *1.2*.

[View compatibility of specific versions here](/versions)

# Migrating assets from the example project

If you so wish, you can migrate assets or the entire menu from the example project to your own.

1. Open the example project for the version of the plugin that your project is using
2. Right click and Migrate the **SettingsUI** widget to your project. This will also copy all of the styled widgets that are used.
3. You should then place the SettingsUI widget in your existing menu or add a way to open it. (See the **DemoPlayerController** Blueprint in the Example Project)

Also be aware that project settings won't be copied with the menu assets, so it's worth comparing the **AutoSettings** configuration page with your own.