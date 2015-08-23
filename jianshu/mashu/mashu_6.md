# 我的sublime

分享我的`Sublime Text`编辑器的设置。

> version=2.0.2

## Theme

> Primer

使用`package control`安装`Theme-Primer`。`Setting-User`配置：

```
{
    "color_scheme": "Packages/Theme - Primer/primer.light.tmTheme",
    "theme": "Primer.sublime-theme"
}
```

## Font
> Monaco

等宽字体，大小根据屏幕分辨率和习惯设置。

```
{
    "font_face": "Monaco",
    "font_size": 11
}
```

## Format

我习惯于用空格缩进，所以用了下面的配置。

```
{
    "draw_white_space": "all",  // 显示空格
    "translate_tabs_to_spaces": true //用空格替代Tab
}
```

## Markdown
> Markdown Preview & markdownEditting

`Markdown Preview`的打开浏览器预览的快捷键默认是`Ctrl+Shift+P`。已被占用，所以改用`Alt+m`。

```
{
    { "keys": ["alt+m"], "command": "markdown_preview", "args": {"target": "browser", "parser":"markdown"} }
}
```
`MarkdownEditting`可以辅助编辑，如果已对语法料如执掌，可以不用。
