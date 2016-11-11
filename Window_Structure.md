## 1 About the Window XML Files

Each window in an Kodi skin is represented by a single .xml file. See here for a list of the standard windows and links to their .xml files.  

The important thing to remember is that each window has a unique identifying name. This is how Kodi identifies the window from within the source code. The window names are all listed in the Appendix I: List of Windows.  

Each .xml file has the same basic structure – it starts with some heading information that pertains to the window as a whole, and then contains a <controls> block within which all the controls that describe the window are defined. Many of the controls within each window should have a unique id's, unless they're just used as images or labels where navigation is unimportant and Kodi does not need to be able to identify them uniquely.  

## 2 Window Header

```xml
<?xml version="1.0" encoding="UTF-8"?>
<window>
  <onload>RunScript(script.foobar)</onload>
  <onunload>SetProperty(foo,bar)</onunload>
  <defaultcontrol always="false">2</defaultcontrol>
  <menucontrol>9000</menucontrol>
  <backgroundcolor>0xff00ff00</backgroundcolor>
  <views>50,51,509,510</views>
  <visible>Window.IsActive(Home)</visible>
  <animation effect="fade" time="100">WindowOpen</animation>
  <animation effect="slide" end="0,576" time="100">WindowClose</animation>
  <zorder>1</zorder>
  <coordinates>
    <left>40</left>
    <top>50</top>
    <origin x="100" y="50">Window.IsActive(Home)</origin>
  </coordinates>
  <previouswindow>MyVideos</previouswindow>
  <controls>
    <control>
    </control>
    ....
  </controls>
</window>
```

One thing to note is that all tag names are lower case. XML tag names are case sensitive!  

The header contains the following tags:  

**onload**  
Optional: the build-in function to execute when the window opens  

**onunload**  
Optional: the build-in function to execute when the window closes  

**defaultcontrol**  
This specifies the default control of the window. This is the id of the control that will receive focus when the window is first opened. Note that most Kodi windows save the current focus when you leave the window, and will return to the last focused item when you return to a window. This behaviour can be stopped by specifying the attribute always="true".  

**menucontrol**  
This specifies the control that will be focused when the users presses the 'menu' / 'm' button.  

**backgroundcolor**  
Specifies whether the window needs clearing prior to rendering, and if so which colour to use. Defaults to clearing to black. Set to 0 (or 0x00000000) to have no clearing at all. If your skin always renders opaque textures over the entire screen (eg using a backdrop image or multiple backdrop images) then setting the background color to 0 is the most optimal value and may improve performance significantly on slow GPUs.  

**visible**  
Specifies the conditions under which a dialog will be visible. Kodi evaluates this at render time, and shows or hides a dialog depending on the evaluation of this tag. See here for more details. Applies only to type="dialog" windows.  

**animation**  
Specifies the animation effect to perform when opening or closing the window. See here for more details.  

**zorder**   
This specifies the “depth” that the window should be drawn at. Windows with higher zorder are drawn on top of windows with lower z-order. All dialogs by default have zorder 1, so if you have a particular dialog that you want underneath all others, give it a zorder of 0. (Note that the normal render order is: The base window, then the overlays (music + video), then dialogs. <zorder> only effects the rendering of the dialogs.  

**coordinates**  
This block is used to specify how Kodi should compute the coordinates of all controls.  

**left**  
Sets the horizontal “origin” position of the window. Defaults to 0 if not present.  

**top**  
Sets the vertical “origin” position of the window. Defaults to 0 if not present.  

**origin**  
Sets a conditional origin for the window. The window will display at (x,y) whenever the origin condition is met. You can have as many origin tags as you like – they are evaluated in the order present in the file, and the first one for which the condition is met wins. If none of the origin conditions are met, we fall back to the <left> and <top> tags.  

**previouswindow**  
This can be used to specify a window to force Kodi to go to on press of the Back button. Normally Kodi keeps a “window stack” of previous windows to handle this. This tag allows you to override this behaviour. The value is the name of the window.  

**views**   
This tag lets you use view id's beyond 50 to 59 it also lets you set the order in which they cycle with the change view button in the skin. Only useful in My<Foo>.xml windows.  

**controls**  
This is the block the defines all controls that will appear on this window.

## 2.1 The Different Types of Controls
Kodi supports many different types of controls.  

[Click here for the control types and what they all do.](http://kodi.wiki/view/Controls)  

Some of these controls are required on specific windows, as they're necessary for that window to perform it's duty, or, the contents of the control are only valid on a particular window. The mandatory controls for each window are listed [here](http://kodi.wiki/view/List_of_Built_In_Controls). While the controls are mandatory, you can ofcourse move them about and change their appearance within the windows to your hearts content!  

## 2.2 Adding Extra Windows
All of the windows in the [window list](http://kodi.wiki/view/Window_IDs) are defined within the executable of Kodi itself, as most of them have a specific purpose. However, the skinner may add extra windows as and when they are needed or wanted. The only restriction to this is that only controls that do not require specific source code to operate can be used. This is not too much of a restriction though, as many skinners have found out.  

To add an extra window, all you need to do is design up the window's .xml file in the usual way, assign it an <id> within the 1100–1199 range (see window list), and then name the file customN.xml, where N is a number or name. You can have as many as you like, as long as they have unique <id>'s, and are named differently. Then just define the type of window you want, the coordinate system and so on, add the controls and setup the navigation. To activate your window, you can do it by adding a button control elsewhere in the skin, or you can get it to popup on a press of the controller or remote via keymap.xml and so on. Basically you just need to run ActivateWindow(id) from a suitable place.  

