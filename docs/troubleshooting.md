# General troubleshooting

**Check the FAQ**

The [FAQ](/faq/) page might already have a solution for your issue.

**Check the output log**

Unless the editor is crashing, open the *Output Log* panel in the editor and try to reproduce the issue.
The output log may show warnings, errors, or other clues that may help resolve the problem.

# Project won't build or package

When the project won't build or package, check the log for errors.

**Error:** ***Expecting to find a type to be declared in a module rules named 'AutoSettings' in UE4Rules***

This is a known bug in Unreal 4.25.2 detailed [here](https://issues.unrealengine.com/issue/UE-95865).
Try updating Unreal or one of the workarounds from the issue page.

# Project is crashing

When the project is crashing, you should look for clues in the crash log or saved log file.

**Error in crash log:** ***Could not find SuperStruct SomeClass to create SomeClass_C***

This usually means you are running on a non-Windows platform that has not been whitelisted in the .uplugin file.
See [FAQ on enabling other platforms](/faq/#does-auto-settings-work-on-platforms-other-than-windows).

**Error in crash log:** ***DXGI_ERROR_INVALID_CALL***

This is a known crash in Unreal 4.23.1 due to a bug in Unreal detailed [here](https://issues.unrealengine.com/issue/UE-81742).
The only known way to fix this is to change to another engine version.

# Settings are not working

**Check if the auto-apply and auto-save properties on the setting are set up correctly**

This could be a simple oversight causing settings to not apply or save when you might expect them to.

**Check the CVar can be modified directly in the console**

Open the console by pressing **~**, then enter the CVar name followed by a space and the value, such as `r.vsync 1`.
If the CVar can be updated this way, there could be a problem with the configuration of the Setting.
If updating the CVar this way also doesn't work, the problem is likely with CVar itself.

[Troubleshooting CVars](/troubleshooting/#console-variables-are-not-working)

**Check that the setting is modifying the CVar value**

Open the full console by pressing **~** twice, then enter the CVar name without any value, such as `r.vsync`.
The current value of the CVar should be outputted to the console. Modify the setting, and check the value in the console again to see if it has updated correctly.
If the CVar value does not update correctly, there could be a problem with the configuration of the Setting.
If the CVar does update correctly, then the problem is likely with CVar itself.

[Troubleshooting CVars](/troubleshooting/#console-variables-are-not-working)

**Check the output log**

Open the *Output Log* panel in the editor, and modify the setting, applying and saving if applicable.
This should create logs like the following:
```
LogAutoSettings: Applying setting r.vsync with value 1
LogAutoSettings: Saving setting r.vsync with value 1
LogAutoSettings: Applying setting r.vsync with value 0
LogAutoSettings: Saving setting r.vsync with value 0
```
If the logs are appearing correctly, then the problem is likely with the CVar itself.

[Troubleshooting CVars](/troubleshooting/#console-variables-are-not-working)

# Console variables are not working

If a specific CVar is not working as you'd expect, the problem is likely not with the Auto Settings plugin itself.

**If the CVar is custom for your project, check the implementation**

A mistake or oversight in the implementation could explain the issue.

**If the CVar is part of Unreal Engine, make sure you really understand what it does**

Many CVars do not make an obvious visual difference in the viewport and an incomplete understanding could be causing you to think it's not working when it actually is.

# Further troubleshooting

**Check the example project**

See if the issue occurs in the [example project.](/example-project/)
If the issue does not happen in the example project, this could point to a configuration or implementation issue in your own project.

**Get support**

If still unable to fix the issue, read how to [get support.](/support/)
Make sure to provide all of the information listed on the support page.