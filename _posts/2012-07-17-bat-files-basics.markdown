---
layout: post
title:  Bat Files Basics
date:   2012-07-17 00:00:00
---

A basic boilerplate for simple bat files which execute some task, for example run unit tests or kick off a build.

    @echo off
    pushd "%~dp0"

    :: a comment
    if "%*" == "" (
      :: default action with no params
    ) else if "%*" == "some_param" (
      :: do something else which some_param is passed in
    ) else (
      :: something else passed in, output help
      echo usage test.bat ^<command^>>CON
      echo.>CON
      echo commands:>CON
      echo 	^<default^>	Run test>CON

    )

    popd

### Explanation

* `@echo off` prevents the commands in the file from being repeated (echoed) in the console.
* `pushd "%~dp0"` saves the current path (for returning to) and changes the current path to where the script is located. This is essential as the rest of the script can be path agnostic.
* `popd` returns to the original current path.
* `%*` any arguments are in this variable, it can be used for simple command switching.

Bat files can get pretty complicated, so usually if I need anything more than the above I'd prefer to switch to Powershell.

#### Aside - .bat vs .cmd

If you're interested in the differences between a .bat and a .cmd file, then this StackOverflow page is interesting: <http://stackoverflow.com/questions/148968/windows-batch-files-bat-vs-cmd>.
Basically in modern Windows there is no difference, just name the file whatever you're comfortable with.

