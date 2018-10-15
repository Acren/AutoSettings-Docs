Auto Settings was designed keeping in mind the fact that most developers will want to use their own UI style for UMG widgets and not be locked into having widgets look a certain way. 

All of the layout and styling for Settings and Input Binding widgets is done on a separate layer from the logic underneath which makes it easy to customize how they look without breaking their functionality. This is done by having the layout and styling defined in widget blueprints that inherit from their respective c++ base classes which handle the functionality.

All of the widgets included in the plugin prefixed with **Default** handle very basic layout and styling for their c++ base classes without the prefix. For example, the Blueprint widget class **DefaultComboBoxSetting** inherits from the c++ class **ComboBoxSetting**.

The best way to re-style Auto Settings widgets in most cases would be make a new blueprint widget class in your project for the widget you want to re-style, as modifying the plugin content might cause you grief later on if you want to update the plugin to a newer version and it overwrites your changes.
This new class would be a child of the c++ class it needs to get its functionality from, and a sibling of the Default version that comes with the plugin. For example if you might make a new **MyGameComboBoxSetting** which inherits from **ComboBoxSetting**. 

You can also copy and paste the Default version from the plugin into your project and modify that, which would accomplish similar results.

The example project also contains versions of the widgets prefixed with **Styled**, which go a little bit further as an example of making them look nicer. If you have migrated the menu from the example project, you can modify these in your own project instead of creating new ones.

