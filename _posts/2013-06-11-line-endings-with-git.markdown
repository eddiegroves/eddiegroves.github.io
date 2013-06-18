---
layout: post
title:  Line Endings with Git
date:   2013-06-11 00:00:00
---

Line endings have caused me a lot of frustration in the past, not just with
**git** but also using various editors and different operating systems.

### Line Endings

The reason line endings in files are such a bother is because there are
different representations.

| OS      | Characters |
| ------- | ----------:|
| Linux   | LF         |
| OS X    | LF         |
| Windows | CR+LF      |

This can cause havoc when opening the same files across different systems,
sharing files with others and especially when line endings are mixed in 
the same file.

### Using Git

Git has the ability to inspect and convert line endings when files are 
added to the git repository. These are the settings I use, which work
perfectly for my **personal** repositories.

|             |                         |
| ----------- | ----------------------- |
| Linux/OS X  | `core.autocrlf = input` |
| Windows     | `core.autocrlf = true`  |

On Linux/OS X this will ensure all line endings are `LF`. On Windows
it will convert `CR+LF` into `LF` on commit, but in the working
directory they will be checked out as `CR+LF`.

### File Command

The `file` command in Linux (see also [File for Windows][3]) is a handy
way to check that line endings are working as expected.

On Linux:

    $ file *
    CNAME:       ASCII text
    _config.yml: ASCII text
    index.html:  HTML document, ASCII text

On Windows:

    > file *
    CNAME:       ASCII text, with CRLF line terminators
    _config.yml: ASCII text, with CRLF line terminators
    index.html:  HTML document text

This setup works well for my repositories because I know that I'll have the
`autocrlf` setting the way I need it. However it is a bit more involved with
public repositories.


### Further Information

* [Newline Wikipedia][1]
* [Tim Clem - Mind the End of Your Line][2]

[1]: http://en.wikipedia.org/wiki/Newline
[2]: http://timclem.wordpress.com/2012/03/01/mind-the-end-of-your-line/
[3]: http://gnuwin32.sourceforge.net/packages/file.htm
