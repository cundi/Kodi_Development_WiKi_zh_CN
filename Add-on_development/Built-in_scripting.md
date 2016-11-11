#1 General form of built-in Functions

Built-in functions take the form  

```
 [XBMC.]Function(param1,param2,...).
 ```

The XBMC. prefix is optional. Some parameters are required, depending on the function. In parsing built-in functions, Kodi first treats quoted (using double quotes ") character strings as literal, and drops the quotes. Thus, when inside a quote, any otherwise special characters will be ignored until the quote is complete. Parameters are separated by commas and, given that functions may be parameters to other functions (such as with the AlarmClock function), anything within brackets () are treated as a single block as well. Finally, prior to passing parameters into the function, any initial and trailing spaces are removed. This system allows you to pass in functions as parameters (the commas used for the passed function are ignored as they're within a () block), as well as allowing you to ignore whitespace around parameter separators. If you wish to pass commas in directly as part of a parameter, simply put quotes around the parameter string - Kodi will strip off the quotes prior to passing it in. Lastly, to pass in an actual quote character, make sure it's escaped (using the \ character), as in "\".  

Some examples:  

```
 ActivateWindow(VideoFiles, path_to_some_files )
 ActivateWindow(VideoFiles,path_to_some_files)
 ActivateWindow(VideoFiles,"path_to_some_files")
```

will all produce the exact same functionality, under the assumption that path_to_some_files contains no initial or trailing spaces (unlikely) and no unmatched brackets and commas. The "ActivateWindow" function will be called with two parameters: "VideoFiles" (the window to open) and "path_to_some_files" (a starting path for the browsing). If path_to_some_files contains initial or trailing spaces, or contains commas or brackets, then only the last form will function correctly.  

## 2 Using Built-in Functions from the skin

To have a button (or toggle button) on the skin run a particular function, you just have to add an <onclick> tag (or <onfocus> tag) containing the function you wish to run.  

For example, adding the following to a button control will create a stop button.  

```xml
 <onclick>PlayerControl(Stop)</onclick>
 ```

If you want a button in your skin taking you directly to the movie listing, add a parameter to the Window ID as follows:  

```xml
  <onclick>ActivateWindow(myvideolibrary,movietitles)</onclick>
```

A list of parameters can be found here:  

Opening Windows and Dialogs

## 3 Using Built-in Functions from python

To run a built-in Kodi function from within a python script, you just need to call executebuiltin() with the function name. For example,
 xbmc.executebuiltin('XBMC.RunScript(Q:\Scripts\myscript.py)')
will run the script myscript.py located in the Scripts directory. On 28.11.2011 a optional parameter was added. Normal call will be non-blocking - so it returns before the extraction has been finished. Now it's possible to call built-in functions blocking by doing:
 xbmc.executebuiltin('XBMC.RunScript(Q:\Scripts\myscript.py)', True)

## 4 Using Built-in Functions from keymap.xml

To bind a built-in function to a particular key, you just add the built-in command to the appropriate section and button in keymap.xml  

For example, to map the running of an executeable to the BLACK button, we'd add:  

```xml
  <gamepad>
    ...
    <black>XBMC.RunXBE(E:\Apps\AVALaunch.xbe)</black>
    ...
  </gamepad>
```

to whatever window section of keymap.xml is appropriate.  

For more information on changing the keymapping with keymap.xml see: Changing the keymapping  

## 5 List of built-in functions

See: List of built-in functions
