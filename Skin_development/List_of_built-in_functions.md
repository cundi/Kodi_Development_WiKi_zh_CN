Skins can use built-in functions with the <onclick> or <onfocus> tag. Scripts can call built-in functions with xbmc.executebuiltin(function, block).  

The latest up-to-date list of built-in functions can be found in the source code files in [1].  

In addition to the following list, for most <onclick> and <onfocus> button actions in the skin you can also use the functions from Keyboard.xml.  

Example:  

```xml
<onclick>VolumeUp</onclick>
<onclick>VolumeDown</onclick>
```

You can use parameters with all media windows, as can be seen here:  

[Opening Windows and Dialogs](http://kodi.wiki/view/Opening_Windows_and_Dialogs)  

## 1 List of functions


|Function  |  Description | Version|
|:---------|:-------------|:-------|
Action(action[,window]) Executes an action (same as in keymap) for the given window or the active window if the parameter window is omitted. The parameter window can either be the window's id, or in the case of a standard window, the window's name. See Action IDs for a list of window names, and their respective ids.   
ActivateScreensaver Starts the screensaver  v13 Addition
ActivateWindow(window[,dir,return]) Opens the given window. The parameter window can either be the window's id, or in the case of a standard window, the window's name. See Window IDs for a list of window names, and their respective ids. If, furthermore, the window is Music, Video, Pictures, or Program files, then the optional dir parameter specifies which folder Kodi should default to once the window is opened. This must be a source as specified in sources.xml, or a subfolder of a valid source. For some windows (MusicLibrary and VideoLibrary), the return parameter may be specified, which indicates that Kodi should use this folder as the "root" of the level, and thus the "parent directory" action from within this folder will return the user to where they were prior to the window activating.    
ActivateWindowAndFocus(id1, id2,item1, id3,item2)   Activate window with id1, first focus control id2 and then focus control id3. if either of the controls is a container, you can specify which item to focus (else, set it to 0).    v12 Addition
Addon.Default.OpenSettings(extensionpoint)  Open a settings dialog for the default addon of the given type (extensionpoint) 
Addon.Default.Set(extensionpoint)   Open a select dialog to allow choosing the default addon of the given type (extensionpoint) 
Addon.OpenSettings(id)  Open a settings dialog for the addon of the given id    
AlarmClock(name,command,time[,silent,loop]) Pops up a dialog asking for the length of time (mm:ss) for the alarm (unless the parameter time is specified), and starts a timer. When the timer runs out, it'll execute the built-in command (the parameter command) if it is specified, otherwise it'll pop up an alarm notice. Add silent to hide the alarm notification. Add loop for the alarm to execute the command each time the specified time interval expires.  
AllowIdleShutdown   Allow the system to shutdown on idle.   v12 Addition
CancelAlarm(name[,silent])  Cancel a running alarm. Set silent to true to hide the alarm notification.  
CECActivateSource   Wake up playing device via a CEC peripheral v13 Addition
CECStandby  Put playing device on standby via a CEC peripheral  v13 Addition
CECToggleState  Toggle state of playing device via a CEC peripheral v13 Addition
|CleanLibrary(database) | This funtion will perform a number of 'cleanup' tasks on your video database and can be run if you have moved, deleted or renamed files. Takes either "video" or "music" as a parameter to begin cleaning the corresponding database. | |
|ClearProperty(key[,id]) | Clears a window property for the current focused window/dialog(key), or the specified window (key,id). | |
Container.NextSortMethod    Change to the next sort method. 
Container.NextViewMode  Select the next view mode.  
Container.PreviousSortMethod    Change to the previous sort method. 
Container.PreviousViewMode  Select the previous view mode.  
Container.Refresh   Refresh current listing.    
Container.SetSortMethod(id) Change to the specified sort method. (For list of ID's see List of sort methods below)  
Container.SetViewMode(id)   Set the current view mode (list, icons etc.) to the given container id. 
Container.SetSortDirection  Toggle the sort direction.  
Container.Update    Update current listing. Send Container.Update(path,replace) to reset the path history.  
Control.Message(id,message,[windowid])  Sends a given message to a control in a given window (or active window if omitted). Messages can be movedown, moveup, pagedown, pageup, click.  
Control.Move(id,offset) Will make a Container with the "id" specified in the command move focus by "offset".    
Control.SetFocus(id,position)   Will make a list with the "id" specified in the command gain focus at "position" number in its list. Alias SetFocus(id,position)    
Dialog.Close(dialog[,force])    Close a dialog. Set force to true to bypass animations. Use (all,true) to close all opened dialogs at once. 
EjectTray() Either opens or closes the DVD tray, depending on its current state 
exportlibrary(music,false,filepath) The music library will be exported to a single file stored at filepath location.    
exportlibrary(video,true,thumbs,overwrite,actorthumbs)  The video library is exported to multiple files with the given options. Here thumbs, overwrite and actorthumbs are boolean values (true or false).  
Extract Extracts a specified archive to an optionally specified 'absolute' path.    
Help    This help message (??? probably broken) 
Hibernate   Hibernate (S4) the System   
InhibitIdleShutdown(true/false) Prevent the system to shutdown on idle. v12 Addition
InstallAddon(id)    Will install the addon with the given id.   
LIRC.Send(command)  Sends a command to LIRC, syntax is the lirc protocol without the newline. Example: LIRC.Send(SEND_ONCE Onkyo_RC-453S2 volup)    
LIRC.Start  Adds Kodi as a LIRC client. 
LIRC.Stop   Removes Kodi as a LIRC client.  
LoadProfile(profilename,[prompt])   Load the specified profile. If prompt is not specified, and a password would be required for the requested profile, this command will silently fail. If promp' is specified and a password is required, a password dialog will be shown.    
Mastermode  Runs Kodi in master mode    
Minimize    Minimizes Kodi  
Mute    Mutes (or unmutes) the volume.  
NextChannelGroup    Navigate to the next PVR channel group (in DialogPVRChannelsOSD.xml)    v13 Addition
NextStereoMode  Changes the stereo mode of the GUI to the next available mode.  v13 Addition
Notification(header,message[,time,image])   Will display a notification dialog with the specified header and message, in addition you can set the length of time it displays in milliseconds and a icon image.  
NotifyAll   Notify all connected clients    v13 Addition
PageDown    Send a page down event to the pagecontrol with given id.    
PageUp  Send a page up event to the pagecontrol with given id.  
PlayDVD Will play the inserted CD or DVD media from the DVD-ROM drive.  
PlayerControl(command)  Allows control of music and videos. The command may be one of Play, Stop, Forward, Rewind, Next, Previous, BigSkipForward, BigSkipBackward, SmallSkipForward, SmallSkipBackward, TempoUp, TempoDown, Random, RandomOn, RandomOff, Repeat, RepeatOne, RepeatAll, RepeatOff, Partymode(music) or Partymode(video) or Partymode(path to .xsp file), and Record. Play will either pause, resume, or stop ffwding or rewinding. Random toggles random playback and Repeat cycles through the repeat modes (these both take an optional second parameter, Notify, that notifies the user of the new state). Partymode(music/video) toggles the appropriate partymode, defaults to music if no parameter is given, besides the default music or video partymode you can also pass a path to a custom smartplaylist (.xsp) as parameter.    
Playlist.Clear  Clear the current playlist  
Playlist.PlayOffset Start playing from a particular offset in the playlist  
PlayMedia(media[,isdir][,1],[playoffset=xx])    Plays the media. This can be a playlist, music, or video file, directory, plugin or a url. The optional parameter ",isdir" can be used for playing a directory. ",1" will start a video in a preview window, instead of fullscreen. If media is a playlist, you can use playoffset=xx where xx is the position to start playback from.  
PlayWith()  Play the selected item with the specified player core.  
Powerdown   Powerdown system    
PreviousChannelGroup    Navigate to the previous PVR channel group (in DialogPVRChannelsOSD.xml)    v13 Addition
PreviousStereoMode  Changes the stereo mode of the GUI to the previous available mode.  v13 Addition
PVR.SearchMissingChannelIcons   Will start a search for missing channel icons   v16 Addition
Quit    Quits Kodi  
Reboot  Cold reboots the system (power cycle)   
RecursiveSlideShow(dir) Run a slideshow from the specified directory, including all subdirs 
RefreshRSS  Reload RSS feeds from RSSFeeds.xml  
ReloadSkin()    Reloads the current skin – useful for Skinners to use after they upload modified skin files (saves power cycling)   
ReplaceWindow(window,dir)   Replaces the current window with the given window. This is the same as ActivateWindow() but it doesn't update the window history list, so when you go back from the new window it will not return to the previous window, rather will return to the previous window's previous window.  
ReplaceWindowAndFocus(id1, id2,item1, id3,item2)    Replace window with id1, first focus control id2 and then focus control id3. if either of the controls is a container, you can specify which item to focus (else, set it to 0). v13 Addition
Reset   Reset the system (same as reboot)   
Resolution  Change Kodi's Resolution.   
RestartApp  Restarts Kodi (only implemented under Windows and Linux)    
RipCD   Will rip the inserted CD from the DVD-ROM drive.    
RunAddon(id)    Runs the specified plugin/script    
RunAppleScript(script[,args]*)  Run the specified AppleScript command   
RunPlugin(plugin)   Runs the plugin. Full path must be specified. Does not work for folder plugins  
RunScript(script[,args]*)   Runs the python script. You must specify the full path to the script. One way to specify the full path is through the special protocol. If the script is an add-on, you can also execute it using its add-on id. As of 2007/02/24, all extra parameters are passed to the script as arguments and can be accessed by python using sys.argv  
Seek(seconds)   Seeks to the specified relative amount of seconds within the current playing media. A negative value will seek backward and a positive value forward.   v15 Addition
SendClick(windowid,id)  Sends a click to a control in a given window (or active window if omitted). 
SetFocus(id,position)   Will make a container with the "id" specified in the command gain focus at "position" number in its list. Alias SetFocus(id,position)   
SetGUILanguage  Set GUI Language    v13 Addition
|SetProperty(key,value[,id])| Sets a window property for the current window (key,value), or the specified window (key,value,id). | |
SetStereoMode   Changes the stereo mode of the GUI. Params can be: toggle, next, previous, select, tomono or any of the supported stereomodes (off, split_vertical, split_horizontal, row_interleaved, hardware_based, anaglyph_cyan_red, anaglyph_green_magenta, monoscopic)   v13 Addition
settingslevelchange Toggles the visible settings (in SettingsCategory.xml) between 'basic', 'standard', 'advanced and 'expert'  v13 Addition
SetVolume(percent[,showvolumebar])  Sets the volume to the percentage specified. Optionally, show the Volume Dialog in Kodi when setting the volume.    
ShowPicture(picture)    Show a picture by its file path/url.    v13 Addition
ShutDown    Trigger default Shutdown action defined in System Settings  
Skin.Reset(setting) Resets the skin setting ?setting?. If ?setting? is a bool setting (i.e. set via SetBool or ToggleSetting) then the setting is reset to false. If ?setting? is a string (Set via SetString, SetImage, or SetPath) then it is set to empty.   
Skin.ResetSettings  Resets all the above skin settings to their defaults (toggles all set to false, strings all set to empty.)  
Skin.SelectBool(header, label1|setting1, label2|setting2)   Pops up select dialog to select between multiple skin setting options. Skin.SelectBool(424, 31411|RecentWidget, 31412|RandomWidget, 31413|InProgressWidget) 
Skin.SetAddon(string,type)  Pops up a select dialog and allows the user to select an add-on of the given type to be used elsewhere in the skin via the info tag Skin.String(string). The most common types are xbmc.addon.video, xbmc.addon.audio, xbmc.addon.image and xbmc.addon.executable.  
Skin.SetBool(setting)   Sets the skin setting ?setting? to true, for use with the conditional visibility tags containing Skin.HasSetting(setting). The settings are saved per-skin in settings.xml just like all the other Kodi settings.   
Skin.SetFile(string,mask,folderpath)    Pops up a folder browser and allows the user to select a file off the hard-disk to be used else where in the skin via the info tag Skin.String(string). If the mask parameter is specified, then the file browser will only search for the extension specified (.avi,.mp3,.m3u,.png,.bmp,etc.,etc.). To use multiple extensions separate them using "|" (minus quotes). If the folderpath parameter is set the file browser will start in that folder.  
Skin.SetImage(string[,value,path])  Pops up a file browser and allows the user to select an image file to be used in an image control elsewhere in the skin via the info tag Skin.String(string). If the value parameter is specified, then the file browser dialog does not pop up, and the image path is set directly. the path option allows you to open the file browser in the specified folder.   
Skin.SetNumeric(numeric[,value])    Pops up a keyboard dialog and allows the user to input a numerical. 
Skin.SetPath(string[,folderpath])   Pops up a folder browser and allows the user to select a folder of images to be used in a multi image control else where in the skin via the info tag Skin.String(string). If the folderpath parameter is set the file browser will start in that folder.   
Skin.SetString(string[,value])  Pops up a keyboard dialog and allows the user to input a string which can be used in a label control elsewhere in the skin via the info tag Skin.String(string). If the value parameter is specified, then the keyboard dialog does not pop up, and the string is set directly. 
Skin.Theme(1)   Cycles the skin theme. Skin.Theme(-1) will go backwards.    
Skin.ToggleDebug    Toggles skin debug info on/off  
Skin.ToggleSetting(setting) Toggles the skin setting ?setting? for use with conditional visibility tags containing Skin.HasSetting(setting).    
SlideShow(dir [,recursive, [not]random])    Starts a slideshow of pictures in the folder dir. Optional parameters are "recursive", and "random" or "notrandom" parameters. The "recursive" parameter starts a recursive slideshow, adding images from sub-folders. The "random" and "notrandom" parameters override the Randomize setting found in the pictures media window.   
|StartAndroidActivity(package,[intent,dataType,dataURI]) |Launch an Android native app with the given package name. Optional parms (in order): intent, dataType, dataURI. example: StartAndroidActivity(com.android.chrome,android.intent.action.VIEW,,http://kodi.tv/)  | v13 Addition|
StartPVRManager (Re)Starts the PVR manager  v12 Addition
StereoModeToMono    Toggle the stereoscopic mode to 2D. v13 Addition
StopPVRManager  Stops the PVR manager   v12 Addition
StopScript(id)  Stop the script by ID or path, if running   v12 Addition
Suspend Suspends (S3 / S1 depending on bios setting) the System 
System.Exec Execute shell commands. 
System.ExecWait Execute shell commands and freezes Kodi until shell is closed.  
System.LogOff   Log off current user.   
TakeScreenshot([filenameandpath,sync])  Takes a Screenshot. You can optionally specify the filename (including the path). Note: only .png files are supported. Add "sync" parameter to run synchronously (slow).    
ToggleDebug Enables/disables debug mode v12 Addition
ToggleDirtyRegionVisualization  makes dirty regions visible for debugging proposes. v16 Addition
ToggleDPMS  Toggle DPMS mode manually   
ToggleStereoMode    Toggle the stereoscopic mode of the GUI (on/off).   v13 Addition
UnloadSkin()    Unloads the current skin    
UpdateAddonRepos    Triggers a forced update of enabled add-on repositories.    
UpdateLibrary(database,[path])  Takes either "video" or "music" as a parameter to begin updating the corresponding database. For "video" you can additionally specify a specific path to be scanned.    
UpdateLocalAddons   Triggers a scan of local add-on directories.    
VideoLibrary.Search Brings up a search dialog which will search the library 
WakeOnLan(mac)  Sends the wake-up packet to the broadcast address for the specified MAC address (Format: FF:FF:FF:FF:FF:FF or FF-FF-FF-FF-FF-FF).   
Weather.LocationNext    Switch to next weather location 
Weather.LocationPrevious    Switch to previous weather location 
Weather.LocationSet Switch to given weather location (parameter can be 1-3) 
Weather.Refresh Force weather data refresh  

|函数     |描述     |版本     |
|:-------|:--------|:-------|
|ClearProperty(key[,id])|清除当前聚焦窗口／对话框（key）的窗口属性，或者是指定的窗口（key, id）||
|SetProperty(key,value[,id])|设置当前窗口(key, value)的窗口属性，或者指定的窗口(key, value, id)||
|StartAndroidActivity(package,[intent,dataType,dataURI]) |应用给定包名运行一个原生的安卓应用。可选参数为（按序排列）：intent, dataType, dataURI。例如：|tartAndroidActivity(com.android.chrome,android.intent.action.VIEW,,http://kodi.tv/)  | v13加入|
