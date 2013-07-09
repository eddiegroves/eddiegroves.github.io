---
layout: post
title:  Connect to GitHub with SSH on Windows using PuTTY
date:   2013-07-09 00:00:00
---

These are the steps I've used for connecting to GitHub with SSH on Windows using the PuTTY tools.

### Summary

1. Download `PuTTY` tools
2. Add `GIT_SSH` environment variable to point to `plink`
3. Create a SSH key with `puttygen`
4. Add key to **GitHub**
5. Run `pageant`

### Step 1 - Download Putty Tools

Download these three [PuTTY tools][1]:

1. [plink.exe](http://the.earth.li/~sgtatham/putty/latest/x86/plink.exe)
2. [pageant.exe](http://the.earth.li/~sgtatham/putty/latest/x86/pageant.exe)
3. [puttygen.exe](http://the.earth.li/~sgtatham/putty/latest/x86/puttygen.exe)

Move them to some place permanent, for example `c:\bin`.

### Step 2 - Add GIT_SSH Environment Variable

<img src="images/github-ssh-tutorial/windows-control-panel-environment-var.png" width="521" height="251" alt="Find Windows enviornment variable settings in Control Panel" />

Set name to `GIT_SSH` and value to the location of `plink.exe`.

<img src="images/github-ssh-tutorial/windows-new-user-variable.png" width="357" height="154" alt="Add new environment variable" />

### Step 3 - Create a Key

Use `puttygen.exe` to **generate** and public/private key.

<img src="images/github-ssh-tutorial/putty-key-generator.png" width="493" height="478" alt="Putty key generator example" />

Save the **private key** somewhere with a passphrase and then **copy** the public key text to the clipboard.

<img src="images/github-ssh-tutorial/putty-key-generator-copy-key.png" width="498" height="234" alt="Select and copy the public key text" />

### Step 4 - Add Key to GitHub

Login to **GitHub** and under `Account settings` > `SSH Keys` add a new key and paste your key.

<img src="images/github-ssh-tutorial/add-key-to-github.png" width="501" height="206" alt="Add new SSH key to GitHub" />

### Step 5 - Use Pageant

Open a new *command prompt* and enter:

    plink git@github.com

You should receive an error message containing:

> No supported authentication methods available

Run `pageant.exe`, this will add an icon into the taskbar. Add your SSH key to the agent
by **right clicking** the icon.

<img src="images/github-ssh-tutorial/pageant-taskbar-icon.png" width="168" height="240" alt="Pageant taskbar icon" />
Try connecting again:

    plink git@github.com

If all went to plan, you should now see a message containing:

> Hi username! You've successfully authenticated

Git should now be able to connect to GitHub using SSH.

[1]: http://www.chiark.greenend.org.uk/~sgtatham/putty/

