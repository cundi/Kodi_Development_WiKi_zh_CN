Every skin, script, or plugin in Kodi contains an addon.xml file which describes the add-on, providing credits, version information and dependencies. Below, we will explain how this file is structured and which elements must be used to create an add-on for Kodi. You can also consult the examples at the end to see how this file is laid out depending on if you are developing a skin or script.  

Every addon.xml file has the same basic structure, this example is for a video plugin:  

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<addon id="plugin.addon.id" name="Your Add-on" version="1.2.3" provider-name="You">
  <requires>
    <import addon="xbmc.python" version="2.1.0"/>
  </requires>
  <extension point="xbmc.python.pluginsource" library="addon.py">
    <provides>video</provides>
  </extension>
  <extension point="xbmc.addon.metadata">
    <summary lang="en_gb">Your add-on's summary</summary>
    <description lang="en_gb">Your add-on's description</description>
    <disclaimer lang="en_gb"></disclaimer>
    <language></language>
    <platform>all</platform>
    <license></license>
    <forum></forum>
    <website></website>
    <email></email>
    <source></source>
    <news></news>
    <assets>
        <icon></icon>
        <fanart></fanart>
        <screenshot></screenshot>
    </assets>
  </extension>
</addon>
```

There are a few important things to note in the above sample:  

- The <addon> element must be present, and be the root node. It presents data about the add-on package as a whole.
- Inside the <addon> element is a <requires> element, listing all the dependencies that this add-on needs in order to function.
- Then there are one or more <extension> elements, each of which describes a part of Kodi that the add-on extends.
- Finally, there is a specific <extension> element that extends "xbmc.addon.metadata". This describes the add-on to the user.

# 1 Elements

## 1.1 <addon>

The <addon> element has 4 attributes, all required: id, version, name, and provider-name. For example:  

```xml
<addon id="script.hello.world" name="Hello World" version="0.0.1" provider-name="Dev1, Dev2">
```

### 1.1.1 id attribute
The id attribute is the unique identifier used for this add-on. It must be unique, and must use only lowercase characters, periods, underscores, dashes and numbers. This identifier is also used as the name of the folder that contains the add-on, so for ease of searching, we suggest you use something like <type>.<uniquename>.  

### 1.1.2 version attribute
The version attribute is used by Kodi to determine whether updates are available. This should be use a version scheme like x.y.z (major.minor.patch). For example: version="0.0.1". Generally, you'll start with a version of 0.y.z for test releases and once you feel it is ready for a full release, you'd bump the version to 1.0.0.  

#### 1.1.2.1 How versioning works
- 2.2.9 is newer than 2.2.1
- 2.2.10 is newer than 2.2.1
- 2.3.0 is newer than 2.2.9
- 2.2.1 is newer than 2.2.1~alpha
- 2.2.1 is newer than 2.2.1~beta
- 2.2.1~beta is newer than 2.2.1~alpha
- 2.2.1~beta3 is newer than 2.2.1~beta2
- 2.2.1~beta10 is newer than 2.2.1~beta1

Text should only be added for a beta version. In other cases version number should only contain numbers.  

### 1.1.3 name attribute
The name attribute is the name of the add-on as it appears in the UI. This should be in English where it makes sense for it to be so, and is not translatable.  

### 1.1.4 provider-name attribute
The provider-name attribute is used as the author field. This could be a team of authors or a single author. If the add-on is maintained by multiple people please separate them with a comma (,).  

## 1.2 <requires>

The <requires> element contains one or more <import> elements which specify which other add-ons this particular add-on requires, and which version of those add-ons it requires. These add-ons may be part of Kodi itself, or may be parts of other third-party add-ons.  

Kodi will only allow the add-on to be run if suitable versions of the (non-optional) add-ons on which this add-on depends are installed. When a user installs your add-on from an online repository via Kodi's add-on manager, Kodi attempts to resolve these dependencies, and install anything that your add-on relies on first. The dependency must be provided with the minimum version number your script/skin requires.  

### 1.2.1 Examples
Here is a sample <requires> block that imports two required modules:  

```xml
<requires>
  <import addon="xbmc.python"                 version="2.14.0"/>
  <import addon="script.module.elementtree"   version="1.2.7"/>
  <import addon="script.module.simplejson"    version="2.0.10"/>
</requires>
```

Here's another example, which will only install on OpenELEC:  

```xml
<requires>
  <import addon="os.openelec.tv" version="2.0"/>
</requires>
```

## 1.3 <import>

Each <import> element describes one dependency for an add-on, with two required attributes: addon and version. There is also an optional attribute called, fittingly, optional.  

If your add-on relies on other third-party add-ons, Kodi will automatically install them as well, provided they are available on an existing add-on repository. If they aren't available on any existing repository, the user must install the other add-ons themselves. Note that you need to include any Python libraries you need directly in your add-on; these can't be loaded with an <import> element, since Kodi wouldn't know what to do with them.  

### 1.3.1 addon attribute
The addon attribute specifies the id of the required add-on, e.g. script.module.elementtree.  

### 1.3.2 version attribute
The version attribute specifies the minimum version of the required add-on to be installed.  

#### 1.3.2.1 Dependency versions
Each different Kodi version might require you to use a higher version of the xbmc.* add-on dependencies to control on which version of Kodi the add-on can be installed.  

#### Current versions
|Kodi version|xbmc.python xbmc.gui|xbmc.json|xbmc.metadata|xbmc.addon|
|:----------:|:------------------:|:-------:|:-----------:|:--------:|
|Dharma 10.1 Deprecated|1.0 |2.11 |2.0| 1.0| 0.1|
|Eden 11.0 Deprecated|    2.0 3.0 4.0 1.0 11.0
|Frodo 12.x Deprecated   2.1.0   4.0.0   6.0.0   2.1.0   12.0.0
|Gotham 13.x 2.14.0 (ABI 2.1.0)  5.0.1   6.6.0 (ABI 6.0.0)   2.1.0   13.0.0 (ABI 12.0.0)
|Helix 14.x  2.19.0 (ABI 2.1.0)  5.3.0   6.20.0 (ABI 6.0.0)  2.1.0   14.0.0 (ABI 12.0.0)
|Isengard 15.x   2.20.0 (ABI 2.1.0)  5.9.0 (ABI 5.3.0)   6.25.1 (ABI 6.0.0)  2.1.0   15.0.0 (ABI 12.0.0)
|Jarvis 16.x 2.24.0 (ABI 2.1.0)  5.10.0  6.32.4 (ABI 6.0.0)  2.1.0   16.0.0 (ABI 12.0.0)
|Krypton 17.x    2.25.0 (ABI 2.1.0)  5.12.0  6.32.4 (ABI 6.0.0)  2.1.0   17.0.0 (ABI 12.0.0)

Each Kodi version contain a certain backwards compatibility. For example add-ons made for Gotham 13.x can still work ion Jarvis 16.x. Do note that this might change in the future. The ABI version you see in the table above is the backwards compatibility version for which add-ons are still marked "working".  

### 1.3.3 optional attribute
The dependency may be made optional by setting the optional attribute to true. This will only install the dependency when the add-on actually needs it. Even if this dependency is missing, the add-on can still be installed.  

## 1.4 <extension>

The <extension> element describes the technical aspects of this add-on. It will have at least a point attribute which will give the part of Kodi that the add-on extends. For instance, the addon.xml file for the Confluence skin extends the xbmc.gui.skin part of xbmc. All available extension points are given below.
The various extension points that Kodi provides are given in the list below.  

|Extension point |Add-on Category|
|:--------------:|:-------------:|
|xbmc.gui.skin   |Skin|
|xbmc.webinterface   |Web interface|
|xbmc.addon.repository   None
xbmc.service    Services
xbmc.metadata.scraper.albums    Album information
xbmc.metadata.scraper.artists   Artist information
xbmc.metadata.scraper.movies    Movie information
xbmc.metadata.scraper.musicvideos   Music video information
xbmc.metadata.scraper.tvshows   TV information
xbmc.metadata.scraper.library   None
xbmc.ui.screensaver Screensaver
xbmc.player.musicviz    Visualization
xbmc.python.pluginsource    Music Add-ons (audio) / Picture Add-ons (image) / Program Add-ons (executable) / Video Add-ons (video)
xbmc.python.script  Music Add-ons (audio) / Picture Add-ons (image) / Program Add-ons (executable) / Video Add-ons (video)
xbmc.python.weather Weather
xbmc.subtitle.module    Subtitle service module
xbmc.python.lyrics  Lyrics
xbmc.python.library None
xbmc.python.module  These don't show up in the addon browser and are purely as support for other scripts.
xbmc.addon.video    Video Add-ons (video)
xbmc.addon.audio    Music Add-ons (audio)
xbmc.addon.image    Picture Add-ons (image)
kodi.resource.images    Additional image files
|kodi.resource.language  Additional language files|

Add-ons that don't correspond to a specific add-on category can not be installed by users. These are usually supporting or shared add-ons that are installed automatically by the add-ons that require them.  

### 1.4.1 xbmc.python.pluginsource
*See also: Plugin sources*
The most common extension point that will be used by plugin addon developers is xbmc.python.pluginsource.  

#### 1.4.1.1 library attribute
The <extension point="xbmc.python.pluginsource"> element has an extra attribute: library. This is the name of the Python script (startup script) that will be run when the add-on is activated. This file must exist in the root of your add-on directory.  

#### 1.4.1.2 <provides> element
The extension has an additional child element named <provides>, which contains a whitespace separated list of image, video, audio, and/or executable. This determines in what area (or context) of the Kodi system your addon will make itself visible in (please note that this applies only to plugin extension points):  

|Provides  |  Appears in|
|:--------:|:----------:|
image   Pictures
audio   Music
video   Video
executable  Programs
(blank) Not visible

#### 1.4.1.3 Example

```xml
<extension point="xbmc.python.pluginsource" library="gpodderxbmc.py">
  <provides>audio video</provides>
</extension>
```

### 1.4.2 xbmc.addon.metadata
This special extension point must be provided by all add-ons, and is the way that your add-on is described to users of the Kodi add-on manager.  

#### 1.4.2.1 Required elements
There are several elements that this should contain and all are compulsory (except the broken tag). Each of the elements below must always be present in English as a minimum.  

Many of these elements can be translated into multiple languages and should be added once for each supported language. The lang attribute should contain a locale identifier. If omitted, it defaults to en_GB. (Note: Kodi v14 and older uses ISO-639 code. See List of language codes (ISO-639:1988)).  

##### 1.4.2.1.1 <summary>
One or more <summary> elements provide a short summary of what the add-on does. This should be a single sentence. It may be translated into multiple languages.  

```xml
<summary lang="en_GB">Hello World script provides some basic examples on how to create your first script.</summary>
```

##### 1.4.2.1.2 <description>
One or more <description> elements provide a more detailed summary of what the add-on does. It may be translated into multiple languages.  

```xml
<description lang="en_GB">Hello World script provides some basic examples on how to create your first script
 and hopefully will increase the number of Kodi users to start creating their own addons.</description>
```

##### 1.4.2.1.3 <disclaimer>
One or more <disclaimer> elements that indicate what (if any) things the user should know about the add-on. There is no need to have a disclaimer if you don't want one, though if something requires settings, or only works in a particular country then you may want to state this here. It may be translated into multiple languages.  

```xml
<disclaimer lang="en_GB">Feel free to use this script. For information visit the wiki.</disclaimer>
```

##### 1.4.2.1.4 <news>
`Note: Used in Kodi v17 Krypton and later only. Older versions are forward compatible.`  

The <news> element should contains a simple description of the major changes made to the add-on (new functionality, big fixes, etc). This is displayed in the Kodi addon installation/update system. (In the author's opinion, too many add-ons skip this piece of information, making it difficult for users to determine whether a particular problem that they may have been having has been fixed or not.)  

Here is an example:  

><news>v0.1.2  (2014-1-15)
>- Added notification for Ubuntu users checking through apt command</news>

##### 1.4.2.1.5 <platform>
The <platform> tag specifies which platforms (operating systems, hardware) this add-on runs on. Many add-ons will run on all platforms, so all is an option. If the platform tag is missing, we assume the add-on runs on all platforms. A combination of these is also possible. Currently available options are:  

all
linux
osx
osx64
osx32
ios
windx
android

```xml
<platform>all</platform>
```

##### 1.4.2.1.6 <language>
The <language> elements indicate the language(s) of the content provided by your add-on. It applies to plugins, scripts, scrapers etc. This allows browsing the add-on list by language. When there is no specific language provided in your content, leave it blank.  

```xml
<language>en de fr</language>
    or
<language></language>
```

##### 1.4.2.1.7 <license>
The <license> element indicates what license is used for this add-on.  

```xml
<license>GNU GENERAL PUBLIC LICENSE. Version 2, June 1991</license>
```

##### 1.4.2.1.8 <forum>
The <forum> element provides the forum thread URL for this specific add-on. Leave this blank if there is no forum thread.  

```xml
<forum>http://www.myaddonwebsite.com/forum.php?thread=12345</forum>
```

##### 1.4.2.1.9 <website>
The <website> element provides the website URL for this specific add-on.  

```xml
<website>http://www.myaddonwebsite.com/</website>
```

##### 1.4.2.1.10 <source>
The <source> element provides the URL for the source code for this specific add-on.  

```xml
<source>http://github.com/someone/myaddon</source>
```

##### 1.4.2.1.11 <email>
The <email> element provides the email address of the author if he wishes to do so for this specific add-on. Here are two examples of how you can make it look (the second one it harder for spambots to use). This can be left blank if you do not want to make your email address public.  

```xml
<email>foo@bar.com</email>
    or
<email>foo at bar dot com</email>
```

##### 1.4.2.1.12 <broken>
The <broken> tag will mark the add-on as broken in the Kodi repo and provide the reason why. You don't need to do a version bump for this to work. However a bump is recommended as you could also add this to the changelog.  

```xml
<broken>deprecated</broken>
```

##### 1.4.2.1.13 <assets>
>Note: Kodi v17 Krypton and later.

The <assets> element is a manifest that describes the various assets the add-on provides and where they are located. Supported sub-elements are:  

- <icon> See Add-on_structure#icon.png
- <fanart> See Add-on_structure#fanart.jpg
- <screenshot>

If some elements are empty or not specified, it will be treated as non-existing/not provided.
Example:  

```xml
<assets>
    <icon>resources/icon.png</icon>
    <fanart>resources/fanart.jpg</fanart>
    <screenshot>resources/screenshot-01.jpg</screenshot>
    <screenshot>resources/screenshot-02.jpg</screenshot>
    <screenshot>resources/screenshot-03.jpg</screenshot>
    <screenshot>resources/screenshot-04.jpg</screenshot>
</assets>
```

With the above example definition, the files must be placed in the resources folder.  

## 1.5 Skin specific elements 皮肤专用元素

### 1.5.1 Overview 概览

|:-----------:|:--------------:|
|effectslowdown|  A multiplier that is applied to all <animation> effect lengths in the skin. Useful to slow down all animations globally so that you can better configure timings and see interactions between animating controls.
debugging   When set to true, it'll display onscreen debug information (xml filename, mouse position and focused control type and name) in the skin.
|res |Support for arbitrary skin resolutions.|

### 1.5.2 How window xml files are found 窗口xml文件是如何被发现的
Kodi can run in many differing resolutions, and a skin should try and cater to all these resolutions. The easiest way is to develop for one specific resolution and make sure that all controls contain <width> and <height> tags. That way, Kodi can scale the controls to the new screen resolution.  

Kodi可以运行在很多不同的分辨率中，

However, you may choose to develop alternative window xml files for differing resolutions (such as for HDTV resolutions, or for widescreen versus 4x3 resolutions).  

不过，你可以选择为不同分辨率开发不同的窗口xml文件（比如，）

The order that Kodi looks for it's skin files are as follows:  

如下是Kodi查找皮肤文件的顺序：  

1. It first looks in the current screenmode folder (one of 1080i, 720p, NTSC16x9, NTSC, PAL16x9 or PAL)
2. If the current screenmode is 1080i and there's no 1080i folder, it then looks in the 720p folder.
3. Finally, it looks in the res folder.

This allows you to just put any window files that do not require special treatment for 16x9 resolutions etc. in the <defaultresolution> folder, preventing needless repetition.  

# 2 Examples 示例

## 2.1 addon.xml for skins

```xml
﻿<?xml version="1.0" encoding="UTF-8"?>
<addon
 id="skin.confluence"
 version="2.1.3"
 name="Confluence"
 provider-name="Jezz_X, Team Kodi">
  <requires>
    <import addon="xbmc.gui" version="4.0.0"/>
  </requires>
  <extension
   point="xbmc.gui.skin"
   debugging="false"
   effectslowdown="0.75">
    <res width="1280" height="720" aspect="16:9" default="true" folder="720p" />
  </extension>
  <extension point="xbmc.addon.metadata">
    <summary lang="en">Confluence skin by Jezz_X. (Kodi's default skin)</summary>
    <description lang="en">Confluence is the default skin for Kodi 9.11 and above. It is a combination of concepts from many popular skins, and attempts to embrace and integrate their good ideas into a skin that should be easy for first time Kodi users to understand and use.</description>
    <disclaimer lang="en">Confluence is the default skin for Kodi, removing it may cause issues</disclaimer>
    <platform>all</platform>
    <license>GNU GENERAL PUBLIC LICENSE. Version 2, June 1991</license>
    <forum></forum>
    <website></website>
    <email></email>
    <source></source>
    <news></news>
    <assets>
        <icon></icon>
        <fanart></fanart>
        <screenshot></screenshot>
    </assets>
  </extension>
</addon>
```

One thing to note is that all tag names are lower case. XML tag names are case sensitive!  

## 2.2 addon.xml for scripts

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<addon
   id="script.artwork.downloader"
   name="Artwork Downloader"
   version="12.0.12"
   provider-name="Martijn">
  <requires>
    <import addon="xbmc.python"                 version="2.1.0"/>
    <import addon="xbmc.json"                   version="6.0.0"/>
    <import addon="xbmc.addon"                  version="12.0.0"/>
    <import addon="script.module.elementtree"   version="1.2.7"/>
    <import addon="script.module.simplejson"    version="2.0.10" optional="true"/>
    <import addon="script.common.plugin.cache"  version="1.3.0"/>
  </requires>
  <extension point="xbmc.python.script"         library="default.py">
    <provides>executable</provides>
  </extension>
  <extension point="xbmc.service" library="service.py" start="login"/>
  <extension point="xbmc.addon.metadata">
    <summary lang="en">Downloads Artwork for TV shows, Movies and Musicvideos in your library</summary>
    <description lang="en">Downloads all available artwork for TV shows, Movies and Musicvideos in your library. Check the options for supported artwork[CR]Artwork sources:[CR]www.fanart.tv[CR]www.thetvdb.com[CR]www.themoviedb.org[CR]Remark:[CR]Check your skin to see what type of artwork is supported![CR]Each TV Show/Movie must have its own folder![CR]Skin integration:[CR]See readme file</description>
    <disclaimer lang="en">For bugs, requests or general questions visit the Artwork Downloader thread on the Kodi forum.</disclaimer>
    <language></language>
    <platform>all</platform>
    <license>GNU GENERAL PUBLIC LICENSE. Version 2, June 1991</license>
    <forum></forum>
    <website></website>
    <email></email>
    <source></source>
    <news></news>
    <assets>
        <icon></icon>
        <fanart></fanart>
        <screenshot></screenshot>
    </assets>
  </extension>
</addon>
```

# 3 Schema Definition

The XML schema definition for addon.xml is located [here](https://github.com/xbmc/xbmc/blob/master/addons/xbmc.addon/metadata.xsd).  


