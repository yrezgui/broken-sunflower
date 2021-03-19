# UXR Study
This study will help us improve the developer experience of Compose integration inside Android 
Studio.
Specifically today, you are going to test different scenarios around Layout Inspector and Live 
Literals.

## Task
This Sunflower is a gardening app illustrating Android development best practices with Jetpack 
libraries. This specific version is a fork of the original one, with one modified screen using 
Jetpack Compose, available [here](https://github.com/android/sunflower/tree/compose), with several 
UI bugs introduced. The goal is to use Layout Inspector and Live Literals to help you fix them.

### Layout Inspector

#### Disappearing toolbar buttons
When opening a flower page, we see two toolbar buttons at the top but they disappear as soon as the 
flower image get loaded.

**Hint**
It's not clear if the buttons are removed or not. Try to hide the rest of the page subtree in Layout 
Inspector to verify if they are still here.

**Solution**
Inside `PlantDetails`, `PlantToolbar` should be placed after `PlantDetailsContent` within `Box`.

#### Overlapping Snackbar
When opening a flower page, a snackbar should appear once you add the flower to your garden. Its 

**Hint**
The flower page content is overlapping the snackbar. Set the snackbar duration to 
`SnackbarDuration.Indefinite` during debugging to help you. Use the 3D view to figure out the bug

**Solution**
Inside `TextSnackbarContainer`, move `content` above `MaterialTheme` within `Box`.


#### Hidden Title
In the flower page, each plant should have a title, but it's not there. Can you figure out what's 
the issue?

**Hint**
Check which component is displaying the title, filter to see its children only in the Layout 
Inspector. You can click on the items to see their positioning on the right panel. You can zoom out 
the view in Layout Inspector and see the title at the bottom.

**Solution**
Change the `y` parameter of `placeable.place` inside the `VisibleModifier` to 0.

#### Different Mode
Have you tried the dark mode on this screen? Could you spot the difference and fix it?

**Hint**
Filter out piece by piece the UI elements of the screen in the Layout Inspector, starting from the 
background to make dark elements more visible

**Solution**
The third `Text` element in `PlanInformation` is using `Color.Black` instead of using alpha or a 
color depending on the MaterialTheme (which changes based on the light/dark mode).
Replace with `MaterialTheme.colors.primaryVariant` or remove the color attribute (the composable 
will use the current text color, which will be already adapted to a dark mode).

### Live Literals