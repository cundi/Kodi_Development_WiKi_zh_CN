# Kodi Add-on, Skin
目前主要做皮肤教程方面的译文

`Skinin Manual Preview: 4 Window, 5 Includes`


## 4 Windows 窗口

### 4.1 Window Structure 窗口结构

### 4.2 About the Window XML Files  窗口XML文件

Each window in an Kodi skin is represented by a single .xml file. [See here for a list of the standard windows and links to their .xml files](http://kodi.wiki/view/Window_IDs).  

Kodi皮肤中的每个窗口都由单个的.xml文件表示。[此处参见标准窗口列表和](http://kodi.wiki/view/Window_IDs)。  

The important thing to remember is that each window has a unique identifying name. This is how Kodi identifies the window from within the source code. The window names are all listed in the Appendix I: List of Windows.  

要记住的重要事情是每个窗口都拥有一个唯一的标识名称。这就是Kodi如何从源码中识别窗口的依据。窗口名称全部在附录I中列出：窗口列表。  

Each .xml file has the same basic structure – it starts with some heading information that pertains to the window as a whole, and then contains a <controls> block within which all the controls that describe the window are defined. Many of the controls within each window should have a unique id's, unless they're just used as images or labels where navigation is unimportant and Kodi does not need to be able to identify them uniquely.  

每个xml文件都具有相同的基本结构——以可以应用到窗口全局的一些头信息开始，然后是窗口的全部控制描述定义包含在<controls>块中。每个窗口的多个控制应该拥有一个唯一的id，除非他们刚好被用做图片或者label，同时导航不是那么重要而且Kodi也不需要标识它们的唯一性。  

### 4.3 Window Header 窗口首部

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

One thing to note is that all tag names are lower case. **XML tag names are case sensitive!**  

要注意的一点是所有的标签名称都是小写的。**XML标签名称是大小写敏感的！**

The header contains the following tags:  

header包含以下标签：  

**onload**  
Optional: the build-in function to execute when the window opens  
可选：窗口打开时要执行的内建函数

**onunload**  
Optional: the build-in function to execute when the window closes  
可选：窗口关闭时会执行的内建函数

**defaultcontrol**  
This specifies the default control of the window. This is the id of the control that will receive focus when the window is first opened. Note that most Kodi windows save the current focus when you leave the window, and will return to the last focused item when you return to a window. This behaviour can be stopped by specifying the attribute always="true".  

该标签为窗口执行的默认控制。这是一个窗口在第一次被打开时会接受聚焦的控制id。注意大多数的Kodi窗口会在你离开窗口时保留当前的聚焦，而且会在你回到窗口时返回上次的聚焦。这个行为可以通过指定属性 always="true 来停止。  

**menucontrol**  
This specifies the control that will be focused when the users presses the 'menu' / 'm' button.  
该标签指定了在用户按下‘菜单’／‘m'按钮时需要被聚焦的control。  

**backgroundcolor**  
Specifies whether the window needs clearing prior to rendering, and if so which colour to use. Defaults to clearing to black. Set to 0 (or 0x00000000) to have no clearing at all. If your skin always renders opaque textures over the entire screen (eg using a backdrop image or multiple backdrop images) then setting the background color to 0 is the most optimal value and may improve performance significantly on slow GPUs.  

该标签指定了窗口是否需要清空之前的设置以便进行渲染，如果需要的话，应该使用哪一种色彩。默认清空为黑色。设置为0（或者or 0x00000000）不执行任何清空。如果你的皮肤一直都是在整个屏幕（比如，使用背景图片或者多个背景图片）上渲染不透明材质，那么可以设置背景色彩为0为最优值，这也可以在慢速GPU上显著提高性能。  

**visible**  
Specifies the conditions under which a dialog will be visible. Kodi evaluates this at render time, and shows or hides a dialog depending on the evaluation of this tag. [See here for more details](http://kodi.wiki/view/Conditional_Visibility). **Applies only to type="dialog" windows**.  

指定对话框可见的条件。Kodi在渲染时对此标签进行计算，并基于对该标签计算的结果显示或者隐藏对话框。[此处有更多详细说明](http://kodi.wiki/view/Conditional_Visibility).**仅在对窗口应用type="dialog"**。  

**animation**  
Specifies the animation effect to perform when opening or closing the window. [See here for more details.](http://kodi.wiki/view/Animating_Your_Skin)  

指定在打开或者关闭窗口时要执行的动画效果。[此处有更多详细说明](http://kodi.wiki/view/Animating_Your_Skin)  s

**zorder**  
This specifies the “depth” that the window should be drawn at. Windows with higher zorder are drawn on top of windows with lower z-order. All dialogs by default have zorder 1, so if you have a particular dialog that you want underneath all others, give it a zorder of 0. (Note that the normal render order is: The base window, then the overlays (music + video), then dialogs. <zorder> only effects the rendering of the dialogs.  

该标签指定了窗口应该被放置的“景深”。更高zorder的窗口放置于低z-order之上。所有的对话框的默认zorder为1，所以如果你有一个想要放置在其他所有窗口之下的特殊对话框，那么可以zorder设置为0.（注意，常规的渲染顺序是：首先是基本窗口，然后是覆盖层（音乐＋视频））

**coordinates 坐标**  
This block is used to specify how Kodi should compute the coordinates of all controls.  
此标签块用来指定Kodi如何计算所有控制的坐标。  

**left**  
Sets the horizontal “origin” position of the window. Defaults to 0 if not present.  
设置窗口的水平“原始”位置。如果该标签为设置默认坐标值为0.  

**top**  
Sets the vertical “origin” position of the window. Defaults to 0 if not present.  
设置窗口的垂直“原始”位置。如果该标签为设置默认坐标值为0.  

**origin**  
Sets a conditional origin for the window. The window will display at (x,y) whenever the origin condition is met. You can have as many origin tags as you like – they are evaluated in the order present in the file, and the first one for which the condition is met wins. If none of the origin conditions are met, we fall back to the <left> and <top> tags.  

为窗口设置有条件的origin。不论origin是什么窗口都会显示在（x，y）。你可以按照个人喜好设置多个origin——它们被计算以出现在文件中，遇到的第一个标签被选中。如果没有碰到origin条件，则回滚到 <left> 和 <top>标签。  

**previouswindow**  
This can be used to specify a window to force Kodi to go to on press of the Back button. Normally Kodi keeps a “window stack” of previous windows to handle this. This tag allows you to override this behaviour. The value is the name of the window.  

该标签用来指定按下返回按钮时Kodi所执行的窗口。通常Kodi保存一个前面“窗口”的栈来处理这个问题。该标签允许你重写默认行为。值为窗口的名称。  
**views**  
This tag lets you use view id's beyond 50 to 59 it also lets you set the order in which they cycle with the change view button in the skin. Only useful in My<Foo>.xml windows.  

该标签让你使用大于50到59点视图id，而且你还可以

**controls**  
This is the block the defines all controls that will appear on this window.  
该标签定义了所有会出现当前窗口的标签块。  

### 4.3.1 The Different Types of Controls
Kodi supports many different types of controls.  
Kodi 支持多种类型的控制。  

[Click here for the control types and what they all do.](http://kodi.wiki/view/Controls)  
[点击此处查看控制类型，以及它们所实现的内容](http://kodi.wiki/view/Controls)  

Some of these controls are required on specific windows, as they're necessary for that window to perform it's duty, or, the contents of the control are only valid on a particular window. The mandatory controls for each window are listed here. While the controls are mandatory, you can ofcourse move them about and change their appearance within the windows to your hearts content!  

其中部分控制需要特定的窗口，

### 4.3.2 Adding Extra Windows 添加额外窗口
All of the windows in the [window list](http://kodi.wiki/view/Window_IDs) are defined within the executable of Kodi itself, as most of them have a specific purpose. However, the skinner may add extra windows as and when they are needed or wanted. The only restriction to this is that only controls that do not require specific source code to operate can be used. This is not too much of a restriction though, as many skinners have found out.  

所有的窗口列表中的窗口都定义在可执行的Kodi内部，它们中的大部分都用于特定的目的。不过，

To add an extra window, all you need to do is design up the window's .xml file in the usual way, assign it an <id> within the 1100–1199 range (see window list), and then name the file customN.xml, where N is a number or name. You can have as many as you like, as long as they have unique <id>'s, and are named differently. Then just define the type of window you want, the coordinate system and so on, add the controls and setup the navigation. To activate your window, you can do it by adding a button control elsewhere in the skin, or you can get it to popup on a press of the controller or remote via keymap.xml and so on. Basically you just need to run ActivateWindow(id) from a suitable place.  

要添加额外的窗口，你所需要的就是依照常规设计窗口的xml文件，并对窗口赋予一个1100-1199范围内的 <id>，然后把文件命名为customN.xml，这里N是一个数字或者名称。随便你写多少个窗口都可以，只要它们都有唯一的<id>，并且使用不同的命名。再然后定义你所希望的窗口类型，添加控制、设置导航、以及坐标系统等等。为了激活你的窗口，你可以通过在皮肤中其它地方添加一个按钮控制来实现它，或者

## 5 Includes 继承

The other special (and arguably the most important skinning file of all) is includes.xml. This is, as its title suggests, a place from which you can define the default look, size, and positioning of controls, to save you replicating many of the control's attributes throughout the window .xml files. For instance, you can setup the size, and textures used for a button control, thus allowing you to leave those details out in the rest of the skin files, unless of course you want to override the default look or size etc. in a particular window.  

比较特别（可以说是所有皮肤文件中最为重要的）的是includes.xml。就像标题所暗示的那样，这是一个允许你定义默认外观、吃顿、以及控制位置的地方，它能够通过窗口的.xml文件免去你去重复很多的控制属性。例如，你可以为按钮控制设置size、用于按钮控制的texture，这样就允许你在剩余的皮肤文件中把这些细节暴露出来，当然除非你想要在部分窗口中重写默认的外观和尺寸等等。  

This is extremely valuable as it allows you to greatly simplify a lot of the work in building a skin. For one thing, it means that once you have include files setup, many of the default parameters for a different resolution can be done by just altering the parameters within the include file(s) for the different resolution.  

这种机制非常有价值，因为它让你极大的简化了很多的构建皮肤工作。要说明的一点是，它意味着你一旦你设置了include文件，很多的不同分辨率的默认参数就可以在include文件中为不同的分辨率

You can infact have more than one include file - you can specify the file attribute when including from a different file, allowing you to have an include file dedicated to a particular set of attributes.  

事实上你可以拥有不止一个include文件——你可以在继承不同的文件时指定文件属性，

The layout of an includes file is as follows.  

include文件的布局如下。  

```
  <?xml version="1.0" encoding="UTF-8"?>
  <includes>
    <include name="whitetext">
      <textcolor>ffffffff</textcolor>
    </include>
    <include file="listdefaults.xml" />
    <include condition="Skin.HasSetting(extras) file="includes_extras.xml" />
    <default type="button">
      <include>whitetext</include>
    </default>
    <constant name="leftedge">50</constant>
  </includes>
```

You'll notice in the above example that we have 4 different types of includes. The first <include> tag basically allows a substitution of the tags underneath it whenever it occurs. For instance, if in a window .xml file you have this:  

你会注意到上面的例子中我们拥有4个不同类型的include。第一个<include> 标签允许你在不论它在何时出现都可以在标签下进行替换。例如，假设你的 window .xml文件包含以下内容：  

```xml
  <control type="togglebutton">
    <include>whitetext</include>
    ... other tags go here
  </control>
```

Then it would substitute the <textcolor> tag for where the include tag is. You can have as many includes as you like, and as many tags can be inside an include - even complete controls, or complete control groups.  

那么它会在include标签出现的地方替换掉<textcolor>标签。随便你用多少个include都可以，

The second <include> tag in the example demonstrates how to include from a different file. As there is no include name specified, it will include the contents of the entire file at that point.  

例子中的第二个<include> 标签说明了从一个不同文件执行继承。

The <default> tag is similar to an include, except that it is used in every control of that type - even if you don't specify that the control is to use includes. Thus every buttoncontrol will have the whitetext include in it. Note that you can override this by specifying the <textcolor> tag in the buttoncontrol.  

<default>标签类似于include，除了它可以用在每一种类型的控制——即使你没有指定控制用于include。因此每一个按钮控制都会用在include中使用whitetext。注意你可以通过指定按钮控制中的 <textcolor> 标签来重写

And finally, the <constant> tag allows you to define a numeric (floating point) constant by name for use in place of numeric values (<left>, height="" etc.) would otherwise be used. This allows alignment of items using the same position values which can then easily be altered in one place.   

最后，<constant> 标签允许你

## 5.1 Use params in includes 在继承中使用参数

As of Kodi 15.0 Isengard you get is the ability to pass arbitrary parameters to your includes and then use these values anywhere within the include body. Just so you don't have to copy/paste huge chunks of XML anymore in order to change just a value or two. Includes are now roughly equivalent to "procedures" in programming languages. Here's the final syntax that has been included in Kodi.  

从Kodi 15.0 Isengard开始你就可以传递任意参数到继承中，然后在继承到主体内部任何地方使用这些值。

Include definitions are still written within <includes> tag, usually in includes.xml. But they can now accept parameters:  

继承的定义依旧可以写在<includes>标签中，通常位于includes.xml中。现在它们能够接受参数了：  

```xml
<include name="MyControl">
    <param name="id"/>
    <param name="left" default="120"/>
    <param name="top">225</param>
    <definition>
        <control type="image" id="$PARAM[id]">
            <left>$PARAM[left]</left>
            <top>$PARAM[top]</top>
            <width>370</width>
            <height>40</height>
            <texture>foo.png</texture>
        </control>
    <definition>
</include>
```

Here, the first part is called parameter list and is specified using <param> tags. When it is present, include body that follows it should be enclosed within <definition> tag. At the moment, parameter list is optional and is mainly used for specifying default values for parameters (such as 120 and 225 above), but is otherwise not mandatory.  

这里，第一部分称作参数列表，而且通过使用 <param> 标签指定。当 <param> 出现时，其后的include主体应该包含在<definition> 标签内。此刻，参数列表可供选用，而且这些参数主要用来为参数指定默认值（比如上面的120到225），反之则是强制的。  

The above include can be called like this:  

上面的继承可以像这样调用：  

```xml
<include content="MyControl">
    <param name="id" value="52"/>
    <param name="left">300</param>
</include>
```

This has the exact same effect as if you've written this instead:  

如果你写的是下面这种结构，其效果仍旧是一样的：  

```xml
<include content="MyControl">
    <control type="image" id="52">
        <left>300</left>
        <top>225</top>
        <width>370</width>
        <height>40</height>
        <texture>foo.png</texture>
    </control>
</include>
```

and called it (old-style) like this:  

并如此（旧式风格）调用这个继承：

```xml
<include>MyControl</include>
```

only without added benefits.  
这样做只是丢失了加入到新版本特性的好处。  

Any appropriate value can be passed as parameter in the new **include call**, including $INFO labels, $LOCALIZE, $VARs, constants, etc. Empty string (value="") can also be passed, for example to override a non-empty default value set in the include definition.  

任何适当的值都可以作为参数传递到新的**继承调用**中，导入 $INFO 标记，$LOCALIZE, $VAR，常量等等。还可传递空字符串（value=""），例如在重写一个设置在继承定义中的非空默认值。  

Default values are used as replacement when their parameters are not passed in the include call.  

当它们的值在include调用汇中没有传递时，默认值被替换。  

$PARAM references can be specified within both tag values and attributes inside include body, and are expanded to either actual value passed (if it was passed), default value (if set) or empty string, in that order.  

$PARAM的引用可以同时在标签值和include主体内部的属性指定，

Parameters without default values (such as id above) are specified for better readability and documentation purposes only, but are otherwise not necessary and can be omitted. This is really a matter of style, and some skinners might prefer writing explicit parameter lists to specify all parameters referenced in the include body. It's a good practice though, as explicit parameter lists might be better utilized in the future versions of Kodi.  

没有默认值的参数（比如上面的id）的指定仅仅基于更好的可读性和文档的考虑，否则就是没有必要，而且会被忽略掉。这真的只是一种风格问题而已，有些皮肤开发者更愿意编写显示参数列表，

If there are no <param> tags at all, <definition> can be omitted too. This leads to even shorter syntax:  

如果根本没有<param>标签，定义也会被忽略。

```xml
<include name="MyControl">
    <control type="image" id="$PARAM[id]">
        <left>$PARAM[left]</left>
        <top>$PARAM[top]</top>
        <width>370</width>
        <height>40</height>
        <texture>foo.png</texture>
    </control>
</include>
```

Includes can call other (nested) includes and even pass them exact parameter values that they've got themselves. This is called **parameter forwarding**.  

继承可以调用其它的（嵌套）继承，设置是将它们完全做为参数值进行传递，

```xml
<include name="MyControl">
    ...
    <include name="MyOtherControl">
        <param name="label">$INFO[Player.Title]</param>
        <param name="label2" value="x:$PARAM[left]; y:$PARAM[top]"/>
        <param name="color" value="$PARAM[color]"/>     <!-- forwarding -->
        <param name="id" value="$PARAM[scrollbarid]"/>  <!-- forwarding -->
    </include>
    ...
</include>
```

Here, $PARAM[color] and $PARAM[scrollbarid] will be forwarded to MyOtherControl only if parameters color and scrollbarid have actually been passed to MyControl, otherwise the default values for color and id (if set in MyOtherControl) will be used instead in the body of MyOtherControl. Composite values containing other characters (such as label2) are not considered as "true" forwarding and always override any default value set in the nested include, even when they expand to empty strings.  

这里，$PARAM[color] 和 $PARAM[scrollbarid] 仅在参数的color和scrollbarid实际被传递到MyControl时，才会转发到MyOtherControl，否则color到默认值和id（如果设置在MyOtherControl中的话）将会被使用，而不是MyOtherControl主体中所定义的。合成值包含其它字符（比如label2）

## 5.2 Variables 变量

Variables make it easier to use conditional infolabels. You can define them in Includes.xml, or to keep them separate, you can place them in another file which is included in Includes.xml. You can include a file in Includes.xml by adding a line like this:  

变量让包含条件的信息标记更易于使用。你可以在Includes.xml中定义它们，或者让它们保持独立，你可以把它们放到继承在Includes.xml中的另外一个文件。你可以通过添加这样的一行继承一个文件：  

```xml
<include file="Variables.xml" />
```

Variables can be used in any tag that supports infolabels, like the texture, label and visible tags. Instead of having to include two whole controls with a condition, they allow you to just apply the condition to the actual texture or label. Meaning less controls to maintain ect. The values in the variable are read from top to bottom and the first condition that is met gets used. The last value usually has no condition and it's content acts as a fallback. The following example shows the album label if the player has audio, the year if there is no audio and no fallback is used (because there either is or is not any audio).  

variable可以用在任何支持信息标记的标签中，比如texture，label和visible标签。与应用两个完整的带有条件的控制相反，它们允许你把条件应用到实际的texture或者label上。同时也意味着更少的标签维护。variable中的value从上至下进行读取，使用第一个遇到的条件。最后一个value通常没有条件，其内容作为回滚。在下面的例子中，如果播放器中没有音频会显示album标记，如果没有音频也没有使用回滚的则显示year标记（因为此处要么有音频要么没有音频）。  

```xml
<variable name="Example">
        <value  condition="Player.HasAudio">$INFO[ListItem.Album]</value>
        <value  condition="!Player.HasAudio">$INFO[ListItem.Year]</value>
        <value>-</value>
</variable>
```

You can use a variable in a label control like this:  

你可以在标记控制中像这样使用变量：  

```xml
<label>$VAR[Example]</label>
```

or when the viariable value is likely to contain commas (,) and/or quotes ("):  

或者在变量的值包含逗号，或者双引号时急性转义：  

```xml
<label>$ESCVAR[Example]</label>
```

(see $ESCINFO[] for more info on the need to escape strings: http://kodi.wiki/view/Label_Parsing)   
更多关于需要转移字符串的

## 5.3 Constants

In case you want to re-use a certain value multiple times in your skin, you can define a constant for it:  

某些情况下你想要在皮肤中重复多次使用某些值，因此你可以定义一个constant：  

```xml
<constant name="FanartCrossfadeTime">300</constant>
<constant name="IconCrossfadeTime">300</constant>
```

you can now reference this value by it's name elsewhere in your skin:  

现在你可以皮肤中的其他地方通过名称引用这个值：  

```xml
<control type="image">
        <left>0</left>
        <top>0</top>
        <width>256</width>
        <height>256</height>
        <texture background="true">$INFO[ListItem.Icon]</texture>
        <fadetime>IconCrossfadeTime</fadetime>
</control>
```

## 5.4 Defaults
for every control type, you can define a default template. for instance here's a template for a button control:  

对于每一种控制类型，你都可以定义一个默认模板。例如，这里是一个按钮控制的模板：  

```xml
<default type="button">
        <left>0</left>
        <top>0</top>
        <width>700</width>
        <height>40</height>
        <label>-</label>
        <texturefocus border="20">list-focus.png</texturefocus>
        <texturenofocus border="20">list-nofocus.png</texturenofocus>
        <font>font20</font>
        <textcolor>white</textcolor>
        <focusedcolor>blue</focusedcolor>
        <disabledcolor>darkgrey</disabledcolor>
        <invalidcolor>red</invalidcolor>
        <textoffsetx>10</textoffsetx>
        <aligny>center</aligny>
        <pulseonselect>true</pulseonselect>
</default>
```

the benefit of defining defaults is that kodi will use the template everywhere in you skin where a button is used, so you don't have to code all of the tags for each and every button. you only have to code the tags that you want to differ from the default template.   

定义default的好处在于，Kodi会在皮肤中的使用了按钮的所有地方使用模板，所以你没有必要为每个按钮编写全部的标签。你唯一必须要做的是编写想要使用的标签不能和默认模板相同。  

## 5.5 Expressions 表达式

expressions are useful if you need to use a certain boolean expression several times throughout your skin. they can be defined in your includes file like this:  

如果你想要对整个皮肤多次使用某些布尔值表达式时，expression就显得很有用了。它们在继承中可以如此定义：  

```xml
<expression name="HasInfoDialog">Window.IsActive(musicinformation) | Window.IsActive(movieinformation) | Window.IsActive(addoninformation)</expression>
<expression name="PluginAdvancedLauncher">substring(Container.FolderPath,plugin://plugin.program.advanced.launcher/,left)</expression>
```

to use an expression in your skin, you can reference them using $EXP[]  

要在皮肤中使用expression，捏可以使用$EXP[]引用它们：  

```xml
<animation condition="$EXP[HasInfoDialog]" effect="fade" start="100" end="0" time="200" tween="sine">Conditional</animation>
<visible>$EXP[PluginAdvancedLauncher] + !Window.IsActive(Home)</visible>
```

expressions can be used in the following tags/attributes:  
expressions可以用在以下标签／属性中：  

- visible
- enable
- usealttexture
- selected
- condition
