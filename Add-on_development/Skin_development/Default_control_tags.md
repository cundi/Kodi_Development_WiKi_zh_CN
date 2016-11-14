# Default control tags
Here are the tags and attributes available for all controls. Note that they're all lowercase, as XML is case sensitive.  


## 1 Tags available to all controls
|Tag(s) 标签 | Definition 定义|
|:-----:|:---------:|
|description| Only used to make things clear for the skinner. Not read by Kodi at all. 仅用来做皮肤的说明。对Kodi来说完全无法读取。|
|type |   The type of control. 控制的类型|
|id | Specifies the control's id. The value this takes depends on the control type, and the window that you are using the control on. There are special control id's that must be present in each window. Any other controls that the skinner adds can be any id they like. Any controls that the skinner specifies content needs not have an id unless it's needed for animation purposes. For instance, most image and label controls don't need an id if the skinner specifies they're content.  指定控制的id。该值的赋予基于控制类型，以及你目前正在控制的窗口。特殊控制id必须出现在每个窗口。|
|left  |  Specifies where the left edge of the control should be drawn, relative to it's parent's left edge. If an "r" is included (eg 180r) then the measurement is taken from the parent's right edge (in the left direction).  指定控制的左边应有的拉动方位，该标签和它的父标签左边有关联。|
|top |Specifies where the top edge of the control should be drawn, relative to it's parent's top edge. If an "r" is included (eg 180r) then the measurement is taken from the parent's bottom edge (in the up direction).|
|right |  Specifies where the right edge of the control should be drawn|
|bottom | Specifies where the bottom edge of the control should be drawn|
|centerleft | Aligns the control horizontally at the given coordinate measured from the left side of the parent control|
|centerright | Aligns the control horizontally at the given coordinate measured from the right side of the parent control|
|centertop |  Aligns the control vertically at the given coordinate measured from the top side of the parent control|
|centerbottom  |  Aligns the control vertically at the given coordinate measured from the bottom side of the parent control|
|width  | Specifies the width that should be used to draw the control. You can use <width>auto</width> for labels (in grouplists) and button/togglebutton controls.|
|height | Specifies the height that should be used to draw the control.|
|visible | Specifies a condition as to when this control will be visible. Can be true, false, or a condition. See Conditional Visibility for more information. Defaults to true.|
|animation  | Specifies the animation to be run when the control enters a particular state. See Animating your skin for more information.|
|camera | Specifies the locaion (relative to the parent's coordinates) of the camera. Useful for the 3D animations such as rotatey. Format is <camera x="20" y="30" />|
|depth |  Specifies the 3D stereoscopic depth of a control. possible values range from -1.0 to 1.0, which brings control "to back" and "to front".</code>|
|colordiffuse  |  This specifies the color to be used for the texture basis. It's in hex AARRGGBB format. If you define <colordiffuse>FFFF00FF</colordiffuse> (magenta), the image will be given a magenta tint when rendered. Defaults to FFFFFFFF (no tint). You can also specify this as a name from the colour theme.|

[img](../Control-positioning.jpg)

## 2 Tags available to focusable controls
In addition, any control that is focusable (e.g. a buttoncontrol) will have the following tags available.  

此外，对于任何可以聚焦的控制都拥有下列标签可用。  

|Tags  标签 |  Definition 定义|
|:----:|:----------:|
|onup  |  Specifies the <id> of the control that should be moved to when the user moves up off this control. Can point to a control group (which remembers previous focused items).|
|ondown | Specifies the <id> of the control that should be moved to when the user moves down off this control. Can point to a control group (which remembers previous focused items).|
|onleft | Specifies the <id> of the control that should be moved to when the user moves left off this control. Can point to a control group (which remembers previous focused items).|
|onright | Specifies the <id> of the control that should be moved to when the user moves right off this control. Can point to a control group (which remembers previous focused items).|
|onback | Specifies the <id> of the control that should be focussed when the user presses the back key. Can point to a control group (which remembers previous focused items).|
|oninfo | Specifies the built-in function that should be executed when the user presses the info key.
onfocus Specifies the built-in function that should be executed when the control is focussed.|
|onunfocus |  Specifies the built-in function that should be executed when the control is loses focus.
hitrect Specifies the location and size of the "focus area" of this control (relative to the parent's coordinates) used by the mouse cursor. Format is <hitrect x="20" y="30" w="50" h="10" />|
|hitrectcolor |   This adds the ability to visualize hitrects for controls. When visible and there's a <hitrectcolor> tag, it will paint a colored rectangle over the actual control. Colors can be specified in AARRGGBB format or a name from the color theme.|
|enable | Specifies a condition as to when this control will be enabled. Can be true, false, or a condition. See Conditional Visibility for more information. Defaults to true.|
|pulseonselect |  This specifies whether or not a button type will "pulse" when it has focus. This is done by varying the alpha channel of the button. Defaults to true.|

## 3 Similar page names

- Video library tags - A tag/keyword system for XBMC v12 (Frodo) and up
- Audio file tags
- Tags available for files
- **Default control tags**

## 4 See also

Development:  

- Add-on development
- Skinning
