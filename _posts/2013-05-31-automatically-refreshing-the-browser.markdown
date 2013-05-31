---
layout: post
title:  Automatically Refreshing The Browser
date:   2013-05-31 00:00:00
---

A common workflow I like to use is having a browser window and code editing window open 
side by side. This dramitcally reduces the tedious Alt-Tab, F5, Alt-Tab steps by 
automatically refreshing the browser window when ever changes are made.

There are plenty of tools available that can do this, but the set that I've settled on
works best for me because of the following.

* It's free
* Works on any platform
* Minimal depencencies
* Simple command line setup

### Requirements

* Chromium based browser
* Livereload extension
* Nodejs
* Gruntjs

## Initial Setup

Using Chrome (for example), install the free [LiveReload extension][1] and also install
[nodejs][2] if you don't have it. Finally, open your favourite terminal and install
[Gruntjs][3].

    npm install -g grunt-cli

## Setup watch and LiveReload for your code

Create a package.json file:

    npm init

Install [grunt watch][4], a grunt plugin with file watching and LiveReload features.

    npm install grunt-contrib-watch --save-dev

Add a `Gruntfile.js` file, this is where grunt is configured.

### Configure Gruntfile

Inside the Gruntfile is where the files to watch are added. Start by adding the basic 
grunt wrapper function:

    module.exports = function(grunt) {
      grunt.initConfig({
      });
    };

Now we'll enable the watch plugin.

    module.exports = function(grunt) {
      grunt.initConfig({
        watch: {
          options: { livereload: true }
        }
      });

      grunt.loadNpmTasks('grunt-contrib-watch');
    };

Finally we add the files/directories to watch and notify livereload when they change.
Below we're adding an object 'myFiles' which contains an array of files to watch, in
this case a relative path to a single file.

    module.exports = function(grunt) {
      grunt.initConfig({
        watch: {
          options: { livereload: true },
          myFiles: {
            files: ['public/index.html']
          }
        }
      });

      grunt.loadNpmTasks('grunt-contrib-watch');
    };

You can add more than one set of files and specify wildcards such as:

    watch: {
      options: { livereload: true },
      html: {
        files: ['public/index.html']
      },
      css: {
        files: ['public/assets/**/*.css']
      }
    }

## Try it out

Run `grunt watch` and try changing a watched file. You should see a message indicating 
the file change was seen.

Open the page in a browser and enable live reload by using the extension's button. If
everything is working it should change, otherwise it'll display an error dialog.

Overall I'm really happy with this setup because it shortens the feedback loop considerably,
keeps my hands on the home keys longer and it works great across different platforms.

## Problems I Encountered

> Errors running watch

Check json syntax is correct.

> Watch not showing file after change

Double check configured file paths.

> Page not reloading

Hovering over the LiveReload button should say `LiveReload is connected`. If it doesn't 
try manually refreshing the page or opening/closing the browser.

## .NET project example:

    watch: {
      options: { livereload: true },
      bin: {
        files: ['src/FoodCompare.Web/bin/FoodCompare.Web.dll']
      },
      html: {
        files: ['src/FoodCompare.Web/Views/**/*.cshtml']
      }
    }

[1]: https://chrome.google.com/webstore/detail/livereload/jnihajbhpnppcggbcgedagnkighmdlei?hl=en
[2]: http://nodejs.org
[3]: http://gruntjs.com
[4]: https://github.com/gruntjs/grunt-contrib-watch
