# MapBasic_SimpleRibbonButtons
An attempt at a simple, but inflexible, wrapper around Peter Horsbøll Møller's Ribbon Library. 

# Explanation
`FULL_RIBBON.mb` is a full compilation of all modules used in Peter's Ribbon library. The reason why I created FULL_RIBBON in the first place was because each time you wanted to compile a simple program to have ribbon buttons, you would need to include a bunch of libraries, and then you'd get compilation errors because you hadn't linked stuff properly.

I wanted a 1 stop location / dumping ground for all the code. That's what this is. For that reason it's also very difficult to maintain, however my original intention was to assemble this file automatically using AHK (something I am yet to do). I've already created the `additions.mb` in `src` for this.

# How to use the library:

## The basic shell:

When making ribbon based applications you need to make sure you have all the pre-requisites in order to support the library. In order to make sure you have everything you need to get going it is advised you use the following shell:

```
Include "FULL_RIBBON.DEF"
Include "Enums.def"
Declare Sub Main				'Required for compilation of projects
Declare Sub EndHandler			'Required for button activity
Global mbxPath as String

'BUTTON HANDLER DECLARES
'*************************


Sub Main()
    mbxPath = ApplicationDirectory$()
    mbxPath = PathToDirectory$(mbxPath)
    
    'MAKE RIBBON BUTTONS
    '*******************
    
      
End Sub

'BUTTON HANDLERS
'****************



'Required for easy EndHandling
Sub EndHandler
    Call RBNEndHandler
End Sub
```

------------------------------------------------------------------------------------------------------------------------

## `RIBBON_AddTab(sTabName, sKeyTip)`

`RIBBON_AddTab`, quite simply, adds a tab to the ribbon.

### Arguments

*string* **sTabName** : This is the name of the tab which you want to create. If the tab already exists, the function will do nothing. 

*string* **sKeyTip**  : The [keytip](http://www.accessribbon.de/images/EN_AccDB1_False.JPG) which will be assigned to this control (key tips appear when you tap the alt key in MapInfo). 

### Usage:

```
Call RIBBON_AddTab("My Tab","M")
```

------------------------------------------------------------------------------------------------------------------------

## `RIBBON_AddGroup(sTabName, sGroupName)`

`RIBBON_AddGroup`, adds a group to an existing tab.

### Arguments

*string* **sTabName**   : This is the name of the tab which will contain the given group. 
*string* *sGroupName** : The name of the group to create. 

### Usage:

```
Call RIBBON_AddTab("My Tab","M")
Call RIBBON_AddGroup("My Tab", "My Group")
```

------------------------------------------------------------------------------------------------------------------------

## `RIBBON_AddButton(sTabName, sGroupName, sButtonName,	 sKeyTip, sIconPath, sDescription, sSubName)`

`RIBBON_AddButton`, adds a button to an existing group.

### Arguments

*string* **sTabName**     : This is the name of the tab which will contain the given group. 

*string* **sGroupName**   : This is the name of the group which will contain the given button. 

*string* **sButtonName**  : This will be the name displayed on your button. 

*string* **sKeyTip**      : This is the keytip of your button. 

*string* **sIconPath**    : This is the path to a picture which contains the image you want to display on your button. 

*string* **sDescription** : This is the description of the buttons action. It will be displayed whenever you hover the mouse over the ribbon button. 

*string* **sSubName**     : This is the name of the sub routine which will be called when your button is clicked. 

### Usage:

```
Declare Sub BUTTON

'... other code

Call RIBBON_AddTab("My Tab","M")
Call RIBBON_AddGroup("My Tab", "My Group")
Call RIBBON_AddButton("My Tab","My Group", "My Button 1", "Y", mbxPath & "Buttons\1.png", "My first button", "BUTTON")

'... other code

Sub BUTTON()
	Note "Button"
End Sub
```

------------------------------------------------------------------------------------------------------------------------

## `RIBBON_AddSimpleButton(sTabName, sGroupName, sButtonName,	 sKeyTip, sIconPath, sDescription, sSubName)`

`RIBBON_AddSimpleButton`, create a button. This is a wrapper method which wraps around the function of `RIBBON_AddTab`, `RIBBON_AddGroup` and `RIBBON_AddButton`. You can call this method without calling any of the other methods. This method is slightly less efficient though, however in general that shouldn't affect performance.

### Arguments

*string* **sTabName**     : This is the name of the tab which will contain the given group. If the tab doesn't exist, it will be created. 

*string* **sGroupName**   : This is the name of the group which will contain the given button. If the group doesn't exist, it will be created. 

*string* **sButtonName**  : This will be the name displayed on your button. 

*string* **sKeyTip**      : This is the keytip of your button. 

*string* **sIconPath**    : This is the path to a picture which contains the image you want to display on your button. 

*string* **sDescription** : This is the description of the buttons action. It will be displayed whenever you hover the mouse over the ribbon button. 

*string* **sSubName**     : This is the name of the sub routine which will be called when your button is clicked. 

### Usage:

```
Declare Sub BUTTON

'... other code

Call RIBBON_AddButton("Tab","Group", "Button 1", "1", mbxPath & "Buttons\1.png", "My first button", "BUTTON1")
Call RIBBON_AddButton("Tab","Group", "Button 2", "2", mbxPath & "Buttons\2.png", "My first button", "BUTTON2")
Call RIBBON_AddButton("Tab","Group", "Button 3", "3", mbxPath & "Buttons\3.png", "My first button", "BUTTON3")

'... other code

Sub BUTTON1()
	Note "Button1"
End Sub
Sub BUTTON2()
	Note "Button2"
End Sub
Sub BUTTON3()
	Note "Button3"
End Sub
```

------------------------------------------------------------------------------------------------------------------------

> **A brief note about split buttons**
>
> The hierarchy of a split button is as follows:
>  SplitButton
>
>      SplitGroup
>
>          SplitControl
>
>          SplitControl
>
>          SplitControl
>
> The Split button contains the current state of the button. The split group contains all the possible states of the button. And each split control, is 1 state of the split button.

------------------------------------------------------------------------------------------------------------------------

## `RIBBON_AddSplitButton(sTabName, sGroupName, sSplitButtonName, sKeyTip, sDefaultButtonName, sDefaultIconPath, sDefaultDescription, sDefaultSubName)`

`RIBBON_AddSplitButton` is a WIP function for creating split buttons. Currently it isn't declared correctly.

### Arguments

*string* **sTabName**            : This is the name of the tab which will contain the given group.

*string* **sGroupName**          : This is the name of the group which will contain the given button.

*string* **sSplitButtonName**    : This is the name of the split button which will contain the given button.

*string* **sKeyTip**             : This is the keytip of your button, displayed when the split button is open.

*string* **sDefaultButtonName**  : This is the name of the default control.

*string* **sDefaultIconPath**    : This is the icon of the default control.

*string* **sDefaultDescription** : This is the description of the default control.

*string* **sDefaultSubName**     : This is the handler of the default control.

### Usage:

To be confirmed...

------------------------------------------------------------------------------------------------------------------------

## `RIBBON_AddSplitGroup(sTabName, sGroupName, sSplitButtonName, sSplitGroupName)`

`RIBBON_AddSplitGroup` is a WIP function for creating split buttons. Currently it isn't declared correctly.

### Arguments

*string* **sTabName**        : This is the name of the tab which will contain the given group.

*string* **sGroupName**      : This is the name of the group which will contain the given button.

*string* **sSplitButtonName**: This is the name of the split button which will contain the given button.

*string* **sSplitGroupName** : This is the name of the split button group to be created.

### Usage:

To be confirmed...

------------------------------------------------------------------------------------------------------------------------

## `RIBBON_AddSplitControl(sTabName, sGroupName, sSplitButtonName, sSplitGroupName, sButtonName, sKeyTip, sIconPath, sDescription, sSubName)`

`RIBBON_AddSplitControl` is a WIP function for creating split buttons. Currently it isn't declared correctly.

### Arguments

*string* **sTabName**        : This is the name of the tab which will contain the given group.

*string* **sGroupName**      : This is the name of the group which will contain the given button.

*string* **sSplitButtonName**: This is the name of the split button which will contain the given button.

*string* **sSplitGroupName** : This is the name of the split button group  which will contain the given button.

*string* **sButtonName**     : This name of your button.

*string* **sKeyTip**         : This is the keytip of your button, displayed when the split button is open.

*string* **sIconPath**       : An image file path, to be the icon of your button.

*string* **sDescription**    : This is the description of the buttons action. It will be displayed whenever you hover the mouse over the ribbon button.

*string* **sSubName**        : This is the name of the sub routine which will be called when your button is clicked.

### Usage:

To be confirmed...
