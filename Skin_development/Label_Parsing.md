# Label Parsing
In label controls, fadelabel controls, built-in functions as well as in the LCD label definition files you can specify more than one piece of information to be displayed in a single line of text (or across multiple lines of text) by using the $INFO, $ESCINFO[] and $LOCALIZE keywords in a <label> tag. In addition to this, you can use the Label Formatting syntax to specify color and style information for the text (changeable within a single label).  

## 1 Example

```xml
  <label>A good example of a $INFO[MusicPlayer.Title,song title: , $COMMA and a]$INFO[MusicPlayer.Artist, song artist:]</label>
  <label>$LOCALIZE[31005]</label>
  <label>The following will be localized from an addons strings - $ADDON[addon.id.here 32001]</label>
```

## 2 How the parsing works 标记解析的工作原理

1. Kodi runs through and replaces any $LOCALIZE[number] blocks with the real string from strings.xml.  
2. Kodi then runs through and translates the $INFO[infolabel,prefix,postfix] blocks from left to right.
3. If the Info manager returns an empty string from the infolabel, then nothing is rendered for that block.
4. If the Info manager returns a non-empty string from the infolabel, then Kodi prints the prefix string, then the returned infolabel information, then the postfix string. Note that any $COMMA fields are replaced by real commas, and $$ is replaced by $.
5. Any pieces of information outside of the $INFO blocks are rendered unchanged.

1. Kodi运行并使用来自strings.xml中的真实字符串来替换任何出现的 $LOCALIZE[number] 块。
2. 
3. 
4. 
5. 

So, in the above example, if nothing is playing then the label will print: A good example of a  

所以就上面例子而言，如果如果什么也没有播放，那么lable的打印内容为：A good example of a  

If a song is playing but it has no Title (ie MusicPlayer.Title? returns an empty string) but does have an artist, it will return: A good example of a song artist: <Artist>  

如果歌曲正在播放虽然缺少标题（比如，MusicPlayer.Title? 返回一个空字符串）但是却有演唱者的话，那么返回内容为： A good example of a song artist: <Artist>  

If a song is playing that has title and artist information, it will return: A good example of a song title: <Title>, and a song artist: <Artist>  

如果播放的歌曲同时拥有标题和演唱者信息的话，返回内容为：A good example of a song title: <Title>, and a song artist: <Artist>  

$ESCINFO[] should be used when passing an infolabel to a built-in function, when this infolabel is likely to contain commas (,) and/or quotes (").  

$ESCINFO[] 应该在传递一个infolabel到内建函数时被使用，当

eg: PlayMedia($INFO[ListItem.Path]) might return: PlayMedia(/some/path/with_a_file_that_includes,a_comma.avi)  

例如：PlayMedia($INFO[ListItem.Path])返回：PlayMedia(/some/path/with_a_file_that_includes,a_comma.avi)  

This will be read by the builtin function generator as PlayMedia called with 2 parameters: "/some/path/with_a_file_that_includes" and "a_comma.avi".  

当PlayMedia使用了两个参数（ "/some/path/with_a_file_that_includes" 和 "a_comma.avi"）去调用时，其内容将由内建函数生成器读取。

If you use PlayMedia($ESCINFO[ListItem.Path]) however, it will make sure that whatever is returned by the infolabel is sent on to the builtin as a single parameter.  



## 3 See also

**Development**:  

- Add-on development
- Skinning
