---
layout: post
title: Convert Windows PC to Linux (Ubuntu)
metatitle: Convert a PC With Windows 10 to Linux (Ubuntu) Dev Environment
description: Learn how to transform your Windows 10 machine into a Linux powerhouse.
metadescription: Learn how to convert your Windows 10 machine to Linux utilizing Windows Subsystem for Linux (WSL) and Ubuntu. Create a Mac-like development environment on your PC.
date: 2019-03-06 12:13
category: Developers, Deep Dive, WSL
post_length: 3
auth0_aside: true
community_topic_id: 22223
author:
  name: Steve Hobbs
  url: https://twitter.com/elkdanger
  mail: steve.hobbs@auth0.com
  avatar: https://en.gravatar.com/userimage/3841188/bc8fc1f1ebb326d59bab456cac894bdf.jpeg
design:
  bg_color: "#214873"
  image: https://cdn.auth0.com/blog/working-on-windows/windows10-logo.png
tags:
- windows
- linux
- wsl
- ruby
- node
- development
- ubuntu
- docker
related:
- 2019-02-26-use-docker-to-create-a-node-development-environment
- 2018-05-17-ruby-on-rails-killer-workflow-with-docker-part-1
---

Imagine for a moment that you're stranded on a desert island. You're a software developer and have been using Linux systems or an Apple Mac ever since you were old enough to type on a keyboard. Yet the only things that you were able to bring with you to your desert island was a Windows machine, and enough tea and biscuits to last a lifetime. Luckily the island already has an internet connection — what do you do?

Okay, you _could_ just [download Ubuntu](https://www.ubuntu.com/#download) and install it onto a Virtual Machine, but there is another way. Which as it happens, also involves installing Ubuntu...

<!-- TOC -->

<div id="toc-container">

<span>Table of Contents</span>

<ul id="toc">
<li><a class="toc-link" href="#a-week-without-my-macbook" target="_self">A Week Without My Macbook</a></li>
<li><a class="toc-link" href="#cross-platform-applications" target="_self">Cross-Platform Applications</a></li>
<li><a class="toc-link" href="#terminal-velocity" target="_self">Terminal Velocity</a></li>
<li><a class="toc-link" href="#enter-the-windows-subsystem-for-linux" target="_self">Enter the Windows Subsystem for Linux</a></li>
<li><a class="toc-link" href="#developers-developers-developers" target="_self">Developers, Developers, Developers</a></li>
<li><a class="toc-link" href="#ive-now-sold-my-macbook" target="_self">I've Now Sold My Macbook!</a></li>
</ul>
</div>

<!-- /TOC -->

## <a class="toc-target" id="a-week-without-my-macbook"></a>A Week Without My Macbook

I was in a very similar situation recently, although instead of being stranded on a desert island I was forced to leave my MacBook with the Apple Store while they fixed a [weird issue with my touch bar](http://www.youtube.com/watch?v=bvU1FIJ0daU).

I had to find a way to keep working while my development machine was in the shop. I love using a Unix command line and tools such as [ZSH](http://www.zsh.org/) and [Oh-my-zsh!](https://ohmyz.sh/). In my day job, I have to use [Ruby](https://www.ruby-lang.org/en/) and [Node](https://nodejs.org/en/) on a regular basis, and I love using [iTerm2](https://www.iterm2.com/) as my main terminal emulator. I also primarily use desktop tools like [Visual Studio Code](https://code.visualstudio.com/), [Docker](https://www.docker.com/products/docker-desktop), and [Slack](https://slack.com/).

One option would be to simply install Docker and [set up a containerized development environment](https://auth0.com/blog/use-docker-to-create-a-node-development-environment/), but that would be _too easy_.

Could I continue using my normal development tools and my workflow without my MacBook? I set out to find out!

{% include tweet_quote.html quote_text="Learn how to install Windows Subsystem for Linux, turning your Windows 10 machine into a full-blown Linux powerhouse" %}

## <a class="toc-target" id="cross-platform-applications"></a>Cross-Platform Applications

Of course, a lot of the applications I just mentioned are available cross-platform, with many of them being HTML, CSS, and JavaScript applications wrapped up using [Electron](https://electronjs.org/). This covers apps like Visual Studio Code and Slack, which are the two main tools I use day-to-day.

I occasionally dip into using [Intellij](https://www.jetbrains.com/idea/) for [Scala development](https://auth0.com/blog/build-and-secure-a-scala-play-framework-api/) and again this runs cross-platform. So it looks like all the desktop applications I need are available, which is great!

For my main development and blog writing activities, I primarily use [Git](https://git-scm.com/), [Ruby](https://www.ruby-lang.org/en/) and [NodeJS](https://nodejs.org/en/). Fortunately, there are Windows installers for all of these that ultimately work, but they all feel a bit _Windows-y_. For example, the best way to use Git on Windows is to use [Git for Windows](https://gitforwindows.org/), which provides a Git Bash application that drops you into a terminal running Git. Or you can use a desktop application like [GitHub Desktop](https://git-scm.com/), or the built-in Git interface inside Visual Studio Code.

![Windows desktop running Visual Studio Code, GitHub Desktop and WSL](https://cdn.auth0.com/blog/working-on-windows:desktop-01.png)

As for Ruby, I enjoy using [RVM](https://rvm.io/), which makes the installation and management of different Ruby versions very easy and relatively painless. Windows is supported using something like [Cygwin](https://cygwin.com/), but again it's not really a native solution and I ran into issues getting it to work the way I'm used to.

All of these are good solutions (if you can get them working) but seeing as the goal of this exercise is to figure out a way to work just like I have been doing on my MacBook, I wanted to explore further.

## <a class="toc-target" id="terminal-velocity"></a>Terminal Velocity

I really enjoy using the terminal for the speed and ability to get things done concisely and quickly. Using a terminal that supports features such as tabs, horizontal and vertical splitting, and Unix command utilities and features like piping and output redirection is very important to me.

Unfortunately, this is where Windows starts to break down. Windows has Command Prompt, which doesn't support any of those nice UI features that I like, and with me not being familiar with Windows shell script, I find it cumbersome. There is also Powershell and, as the name suggests, is very powerful but it's something new I'd have to learn. Ultimately, it would take time until I'm as productive as before. Interestingly for the Powershell users, [posh-git](https://github.com/dahlbyk/posh-git) gives you adornments in the terminal as the Git status of the current folder, which is one of the features I like about Oh-my-zsh.

![Screenshot of posh-git with Powershell on Windows](https://cdn.auth0.com/blog/working-on-windows:posh-git.png)

I'm in love with [iTerm2](https://www.iterm2.com/) on the Mac for its ability to use tabs, split windows, profiles, and theming, so is there anything that gets me close?

[Hyper](https://hyper.is/) is a terminal emulator that supports at least the UI features of being able to use tabs and window splitting. It's based on Electron and so is cross-platform, and supports more advanced features like [themes](https://hyper.is/themes) and [plugins](https://hyper.is/plugins). I do like theming my applications so that they look more pleasing to the eye, but I was willing to forget about that for this short-lived exercise.

However, it's just an emulator and therefore is still just using Windows shell script. Something more fundamental under the hood would have to change.

## <a class="toc-target" id="enter-the-windows-subsystem-for-linux"></a>Enter the Windows Subsystem for Linux

[Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/about) (WSL) is a way to run native Linux commands and tools alongside your existing Windows apps. It doesn't use a virtual machine and is as easy to access as opening a terminal window. To quote directly from the documentation:

> The Windows Subsystem for Linux lets developers run GNU/Linux environment -- including most command-line tools, utilities, and applications -- directly on Windows, unmodified, without the overhead of a virtual machine.

Sounds good, doesn't it? In theory, I should be able to use all the command-line tools that I'm used to without leaving my Windows desktop environment.

To install WSL, you need to be on the Windows 10 Fall Creator's Update (build 16215). Then, you can install the feature by using the "Turn Windows features on or off" facility and ticking "Windows Subsystem for Linux":

![Screenshot of the Add Windows Features dialog](https://cdn.auth0.com/blog/working-on-windows:installing-wsl.png)

It can also be installed by running this Powershell command:

```powershell
# Run this inside Powershell to enable the WSL feature
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

> **Note**: The machine may need to be restarted once WSL is installed

One of the many [Linux distributions on the Windows Store](https://www.microsoft.com/en-gb/search/shop/apps?q=linux&devicetype=pc&Price=0) can then be installed as a Windows App. I chose [Ubuntu](https://www.microsoft.com/en-gb/p/ubuntu-1804-lts/9n9tngvndl3q?activetab=pivot:overviewtab) as it's the one I'm most familiar with. An Ubuntu app becomes available once it's installed, but the normal Windows Command Prompt app can be used in its place if you so wish.

Then, to enter a Linux terminal, open Command Prompt (or your terminal emulator of choice) and type `wsl` to get started. The next thing you will see is your Linux command prompt.

```bash
# My WSL command prompt inside the Command Prompt application
/c/Users/steve >
```

So what can be done from here? Supposedly anything that can normally be done from an Ubuntu terminal. Let's check what release of Ubuntu I'm using:

```bash
> lsb_release -a

No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 18.04.2 LTS
Release:        18.04
Codename:       bionic
```

Use `curl`?

```bash
> curl -i google.com

HTTP/1.1 301 Moved Permanently
Location: http://www.google.com/
Content-Type: text/html; charset=UTF-8
Date: Tue, 26 Feb 2019 10:42:51 GMT
Expires: Thu, 28 Mar 2019 10:42:51 GMT
Cache-Control: public, max-age=2592000
Server: gws
Content-Length: 219
X-XSS-Protection: 1; mode=block
X-Frame-Options: SAMEORIGIN

```

Install Vim?

```bash
> sudo apt-get install vim

Reading package lists... Done
Building dependency tree
Reading state information... Done
The following package was automatically installed and is no longer required:
  libfreetype6
Use 'sudo apt autoremove' to remove it.
0 upgraded, 0 newly installed, 1 reinstalled, 0 to remove and 3 not upgraded.
Need to get 1152 kB of archives.
After this operation, 0 B of additional disk space will be used.
Get:1 http://archive.ubuntu.com/ubuntu bionic/main amd64 vim amd64 2:8.0.1453-1ubuntu1 [1152 kB]
Fetched 1152 kB in 0s (2468 kB/s)
(Reading database ... 39405 files and directories currently installed.)
Preparing to unpack .../vim_2%3a8.0.1453-1ubuntu1_amd64.deb ...
Unpacking vim (2:8.0.1453-1ubuntu1) over (2:8.0.1453-1ubuntu1) ...
Setting up vim (2:8.0.1453-1ubuntu1) ...
```

As you can see, `apt-get` is available and can be used to install any software that would normally be available on a native instance of Ubuntu.

Can something like NVM be installed the same way as on a native Linux distribution?

> For the purposes of this recording and in the interest of time, I had already installed NVM on this machine, but not Node itself. Take a look and see what happens!

<video controls="controls">
  <source type="video/mp4" src="https://cdn.auth0.com/blog/working-on-windows:nvm-video.mp4"></source>
</video>

Thankfully, nothing unremarkable happens! I get Node 10 and NPM installed just as happily as I would have done on a native Ubuntu install. I can also confirm that I was able to install RVM perfectly well, by following [the installation instructions](https://rvm.io/) that I would have normally followed on Linux.

Furthermore, I was able to install ZSH and Oh-my-zsh without any issues, again using the instructions provided for Linux. With this in place, I'm already most of the way towards working the way I'm used to on my Macbook!

## <a class="toc-target" id="developers-developers-developers"></a>Developers, Developers, Developers

Now that I have the tools installed, what is the actual development experience like?

I can happily report that it is fairly unintrusive to the point where I almost forget I'm working on a Windows machine. Thanks to the fact that Windows drives are automatically mounted into your Linux environment, I still get access to my files and folders from within my Ubuntu environment. This means I can use Git and all the other command-line utilities that I'm used to, but still manipulate those files using whatever editor on the host Windows machine I want. By default, your host drives are available in the `/mnt` folder. So a Windows path of `D:\Development\auth0` would be available in your Linux environment as `/mnt/d/Development/auth0`.

At the moment, it's not possible to get access to the Linux filesystem from the Windows host, but [that will change in Windows 10 build 1903](https://blogs.msdn.microsoft.com/commandline/2019/02/15/whats-new-for-wsl-in-windows-10-version-1903/). In a nutshell, WSL will start a <a href="https://en.wikipedia.org/wiki/9P_(protocol)">9P file server</a> on bootup with Windows as the client, serving Linux files over an internal network protocol.

### Windows UI features

For me, the operating system shell is just as part a part of the development experience as the software I use to do my job. For example, I'm a heavy user of OSX's [Spotlight](https://support.apple.com/en-gb/HT204014) feature, and I regularly navigate through my operating system simply by using text search; it's very easy to press `Cmd+Space` and search for what I want.

Windows 10 supports just the same functionality and allows me to move around the operating system very easily, opening programs and manipulating windows simply by using the keyboard. Pressing `Windows Key` opens the Windows Start Menu, where I can just start typing what I want. Admittedly this is not obvious, as there is no focussed text box to indicate to the user that they're able to type a search term.

<video controls="controls">
  <source type="video/mp4" src="https://cdn.auth0.com/blog/working-on-windows:startmenu-video.mp4"></source>
</video>

Another feature of OSX that I often use is [multiple desktops](https://support.apple.com/en-gb/HT204100), or _Spaces_. This is part of the Mission Control feature that can partition applications into different Spaces, allowing you to easily swipe between them. I use this feature to organize my work better. As an example, with every instance of Visual Studio Code that I have open, I tend to have a corresponding instance of iTerm2 open at my working directory for the project I'm working on. Using multiple desktops, I can group these instances together so that I have different desktops set up for different projects. I can switch between different desktops using a trackpad gesture, or by using `Ctrl+Left/Right Arrow` to move between them.

Luckily for me, Windows 10 supports this exact feature! Just like on OSX, different desktops can be created that play host to different instances of running applications, and I can switch between them using simple keyboard commands. Pressing `Win Key+Tab` gives me a Mission Control-like overview of my available desktops and applications. I can even specify that an instance of an app is available across _all_ my desktops (it's handy to have my favorite music player available wherever I need it!).

![Screenshot of Windows' multiple desktops feature](https://cdn.auth0.com/blog/working-on-windows:multi-desktops.png)

{% include tweet_quote.html quote_text="With WSL, I love that I have all the command-line tools that I'm used to available to me, as well as the ability to use multiple desktops, search, and use all my favorite desktop applications." %}

### A word about Docker

I wanted to touch on my experience using Docker with this setup. I already have [Docker Desktop](https://www.docker.com/products/docker-desktop) installed on my host Windows machine, and I was concerned that I may have had to uninstall that in order to get it working inside WSL. Either that, or I would have to live with having _two_ instances of Docker on my machine taking up valuable hard-drive space; one for the Windows host, and another inside WSL.

Thankfully, I didn't have to do either of those things and following [these instructions on setting Docker up](https://nickjanetakis.com/blog/setting-up-docker-for-windows-and-wsl-to-work-flawlessly) to work on WSL (flawlessly, as the article title puts it) was very easy and painless. The basic principle is that Docker running on the Windows host can also be used by the Docker client running inside WSL, as the two are interfaced by a REST API. The key piece of configuration is to tell the Docker client inside WSL where the host is. By default, it connects to a Docker instance running on the same machine, but in this case, we can point it to the instance running on the Windows host.

After having gone through the setup myself, I can confirm that Docker from inside WSL works as expected!

### SSH keys

As you might expect from reading through this post, generating SSH keys works exactly the same way as on any other Linux distro. I followed the [SSH key guide on GitHub.com](https://help.github.com/en/enterprise/2.14/user/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) and it just works. The caveat is that the SSH key will be generated for your WSL install, and so the key will need to be added to any services you use that require SSH keys.

This is fine for me, but if you already have an SSH key for your Windows profile then you can [symlink your `.ssh` folder into your WSL install](https://florianbrinkmann.com/en/3436/ssh-key-and-the-windows-subsystem-for-linux/) if you wish to use the same keys.

## <a class="toc-target" id="ive-now-sold-my-macbook"></a>I've Now Sold My Macbook!

I haven't actually sold my Macbook. However, given everything that I've experienced getting my development environment _pretty close_ to what I'm used to, I'm pretty certain that I would be able to live without it for a while longer. I love that I have all the command-line tools that I'm used to available to me, as well as the ability to use multiple desktops, search, and use all my favorite desktop applications.

So far I haven't found an instance where Windows Subsystem for Linux has provided an obstacle where I can't get working, although I admit that even the use-case I present here is probably quite simplistic compared to how some other people would like to use it.

Are you a WSL user? Have your experiences been good or bad? Tell us about it in the comments below!

{% include asides/about-auth0.markdown %}
