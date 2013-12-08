---
layout: post
title: Use EditorConfig to Maintain Consistent Coding Styles between Different Editors and IDEs
date: 2012-03-14 21:46
comments: true
categories: [Software Development, Editor, IDE, Coding Style]
---

Usually for a project with more than one developer involved, it is essentially
important for the project to define and maintain a consistent [coding style][].
Most code editors and IDEs, such as [Vim][], [Emacs][], [Code::Blocks][],
provide settings related to coding styles, such as the width of tab, the size of
indentation, [end of line][EOL], etc. However, it is hard to provide the same settings
for different Editors and IDEs: we have to maintain many config files for
different editors and IDEs, such as [.vimrc][] for [Vim][], [.emacs][] for
[Emacs][]. In order to solve this, [EditorConfig][] was born. By defining coding
style in files named `.editorconfig`, the [EditorConfig plugins][] for different
editors and IDEs will automatically adjust your coding style.

<!-- more -->

## Download EditorConfig Plugin for Your Editor/IDE

To use EditorConfig, you have to download the corresponding
[EditorConfig plugins][] for your Editor or IDE. Follow the installation
instructions to install them.


## Create an `.editorconfig` File for Your Project

An `.editorconfig` file is an [INI][] format file, which contains the settings
of your coding style. You could use one or more `.editorconfig` files to
indicate the coding style of your project. Let's try a simple example. Create a
file named `.editorconfig` at the root of your project source tree (if you are
working on Windows and using Windows Explorer, you will find Window Explorer
reports such file name as illegal. Don't worry, just create a file named
`.editorconfig.`, which will be renamed to `.editorconfig` automatically by
Windows Explorer):

```ini .editorconfig
; indicate this is the root of the project
root = true

[*]
indent_style = space
end_of_line = lf

[*.c]
indent_size = 4

[Makefile]
indent_style = tab
indent_size = 8
```

Let's check this file line by line.

```ini
; indicate this is the root of the project
```

This is a [comment line][comment]. All lines starting with a `#` or `;` will be
regarded as comment lines.

{% codeblock lang:ini start:2 %}
root = true
{% endcodeblock %}

This line tells EditorConfig this is the root of the project, thus EditorConfig
won't apply the settings of `.editorconfig` outside this directory.

{% codeblock lang:ini start:4 %}
[*]
indent_style = space
end_of_line = lf
{% endcodeblock %}

These 3 lines indicates for all files, if not specially specified, we use spaces
for indentation, and use `lf` as the [EOL][] marker for all files.

{% codeblock lang:ini start:8 %}
[*.c]
indent_size = 4
{% endcodeblock %}

These two lines means, for any C source files, the size of indentation is 4.

{% codeblock lang:ini start:11 %}
[Makefile]
indent_style = tab
indent_size = 8
{% endcodeblock %}

These 3 lines tell EditorConfig that, for any file named `Makefile`, we use tab
for indentation, and the size of indentation is 8.

After saving this file, open a C source file and a Makefile in your source tree
with your editor/IDE. If everything goes well, you will find that the
buffer-local coding style settings have been adjusted. (Note: EditorConfig is
not a code formatter. That is to say, the existing codes in your source files
will not be reformatted. Only the style of your newly input code is adjusted.)


## More

This is just a simple introduction of [EditorConfig][]. If you find this
useful, you may want to visit [EditorConfig homepage][EditorConfig] to see more
about it.


_related article:_

[**Maintaining Consistent Coding Conventions With EditorConfig**](http://treyhunner.com/2012/02/editorconfig) by [_Trey Hunner_](http://treyhunner.com)


[.emacs]: http://www.gnu.org/software/emacs/manual/html_node/emacs/Init-File.html
[.vimrc]: http://vim.wikia.com/wiki/Open_vimrc_file
[Code::Blocks]: http://www.codeblocks.org
[EOL]: http://en.wikipedia.org/wiki/Newline
[EditorConfig plugins]: http://editorconfig.org/#download
[EditorConfig]: http://editorconfig.org
[Emacs]: http://www.gnu.org/software/emacs
[INI]: http://en.wikipedia.org/wiki/INI_file
[Vim]: http://www.vim.org
[coding style]: http://en.wikipedia.org/wiki/Programming_style
[comment]: http://en.wikipedia.org/wiki/Comment_(computer_programming)
