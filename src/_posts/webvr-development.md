---
title: "WebVR Development Workflows on OS X or Linux"
author: twitter|andgokevin|Kevin Ngo
date: 2017-02-15
layout: blog
image:
  src: https://cloud.githubusercontent.com/assets/674727/23008498/d78adf04-f3c4-11e6-9b09-89436c5dfc07.png
---

Many web developers develop on OS X or Linux, not on Windows. Web development
tools and workflows today center around Unix shells. Windows does not have a
Unix-like environment, which can leave web developers feeling naked.

There is Bash on Ubuntu on Windows (i.e., Windows Subsystem for Linux), but
it's very much a work-in-progress with difficulties scrolling,
copying-and-pasting, lack of good terminal colors, and inability to use web
development tools such as Karma, JavaScript test runner. There is also Cygwin,
but it doesn't work out of the box with Node and npm. There is also Powershell,
but it's a completely different environment than Unix.

Windows development can totally work. Some developers on the A-Frame team use
Windows full-time. But for many web developers, we'd like to not have to change
our tools and environment.

But VR and WebVR today *only* works on Windows. When it comes time to test
and debug room scale VR with positional tracking, controllers, and interaction,
Windows is unavoidable. The good news is that with the power of the cloud, we can
develop full-time within OS X and Linux (even laptops) while testing on a
Windows desktop:

[ngrok]: https://ngrok.io

- Tunneling to a laptop with [ngrok.io].
- Developing within a Linux virtual machine (VM).

<!-- more -->

## Tunneling with ngrok.io

![ngrok](https://cloud.githubusercontent.com/assets/674727/23008497/d737b388-f3c4-11e6-8317-06417f4f6a23.png)

> I want to expose a local server behind a NAT or firewall to the internet.

[ngrok.io] is a secure tunneling service that allows requests to punch through
firewalls and into your local network. On a laptop (e.g., Macbook or Linux
laptop), we can have a local web server watching and serving our project files.
Then from a Windows desktop, a browser can access that local web server through
a provided URL. We don't have to search and plug in the computer's local IP
address. And this works even if the desktop is not on the same network as the
laptop. And ngrok will stand up SSL/HTTPS in front of the server, which will
seem to be a requirement for the WebVR API if not on `localhost`.

### Steps

[boilerplate]: https://github.com/aframevr/aframe-boilerplate

1. [Download and unzip ngrok](https://ngrok.com/download) on your OS X or Linux machine.
2. Start a local web server within your project (e.g., `python -m SimpleHTTPServer 8080`, `npm install -g live-server && live-server`).
3. Run ngrok, providing `http` and the port. (i.e., `./ngrok http 8080`).
4. In the console, ngrok will provide a randomly-generated URL (e.g.,
`https://abcdefg.ngrok.io`)
5. On your Windows machine, navigate to the ngrok URL in the browser.
6. The Windows machine should be able to access the project's local web server
running on the OS X or Linux machine. Develop in OS X or Linux, test on Windows!

### Custom Subdomains

[basic]: https://ngrok.com/product#pricing

It is cumbersome to type in the randomly-generated ngrok URL every time.
Especially the current state of WebVR involves restarting browsers often. If
you find this workflow is useful to you, I recommend upgrading to [ngrok's
Basic Plan][basic] to reserve custom subdomain names. You can create clean URLs
that are easy to remember and easy to type (e.g., `tomato.ngrok.io`).

[signup]: https://dashboard.ngrok.com/user/login
[token]: https://dashboard.ngrok.com/get-started
[domains]: https://dashboard.ngrok.com/reserved

1. [Sign up on ngrok][signup].
2. [Install your ngrok authentication token][token].
3. [Create your reserved domains][domains].
4. Point to the domain when starting ngrok (e.g., `./ngrok http
-subdomain=tomato 8080`)
5. Navigate to the ngrok URL in the browser (e.g., `https://tomato.ngrok.io`).

To make this even easier, create a Bash alias to make it quick to start up
different instances of ngrok wherever on whatever port:

```
# ~/.bash_aliases
alias ngrok="~/path/to/ngrok http -subdomain=tomato"
alias ngrok2="~/path/to/ngrok http -subdomain=potato"
```

Then invoke the aliases:

```
ngrok 8080
ngrok2 9090
```

[pro]: https://ngrok.com/product#pricing


I personally upgraded to [ngrok's Pro Plan][pro] so I could have more than
instance of ngrok running at once, where I was serving an A-Frame project but
also a locally-served A-Frame component.

ngrok works great if you have multiple machines. At home, I have a Macbook with
Windows machine hooked up to an HTC Vive and one Windows laptop hooked up to an
Oculus Rift, making it easy to test across multiple headsets while developing
from one Macbook. But if we're working with just one machine, a Linux VM works
just as well.

## Linux VM

[vbox]: https://www.virtualbox.org/wiki/Downloads

[VirtualBox] lets us install and run a guest operating system within our host
operating system (i.e., a Virtual Machine, VM). Primarily, we'll be installing
an Ubuntu VM within a Windows machine. From that Ubuntu VM, we can develop with
in a Unix-like environment and run a local server that can be accessed from the
host Windows machine.

This is the development workflow I use when I'm traveling with just a Windows
laptop and a Vive. As a former full-time Linux user, it feels great to be using
Ubuntu again!

### Steps

[ubuntu]: https://www.ubuntu.com/download/desktop

1. [Install VirtualBox][vbox].
2. [Download the latest Ubuntu Desktop image][ubuntu].
3. Within VirtualBox, create a new virtual machine. Select *Linux* and *Ubuntu
(64-bit)*.
4. Allocate how much RAM to give the VM. Give it a good chunk so it runs
smoothly. With 24GB of RAM available on my machine, I gave my VM 6GB of RAM.
5. Create a virtual hard disk using VirtualBox Disk Image (VDI). Make it
dynamically allocated. Allocate how much disk space to give the VM. Since I
work on a lot of projects and assets or `node_modules/` take up space I gave my
VM 64GB.
6. Hit *Create* to finish the creation of the VM.
7. In *Settings -> General -> Advanced*, set *Shared Clipboard* and
*Drag'n'Drop* to *Bidirectional*. This might come in handy in general.
8. In *Settings -> System -> Processor*, configure the number of processor
cores to give the VM. VirtualBox defaults to 1. Since I was going to spend the
majority of my time in the VM, I gave my VM 4 cores out of the 8 available on
my machine.
9. In *Settings -> Display -> Screen*, allocate how much Video Memory to give
the VM. I gave my VM 32MB out of the 128MB available on my machine. Since
you're developing VR, save a good amount of Video Memory for the host machine.
Also check *Enable 3D Acceleration*.
10. In *Settings -> Network -> Adapter 1*, attach to *Bridged Adapter* instead
of *NAT*. This will let the host machine access local web servers on the guest
machine.
11. Start the VM.
12. Select the Ubuntu Desktop image downloaded earlier as the boot image. Go
through the process of installing Ubuntu.
13. Once Ubuntu is installed, set up your development environment and start a
local server.
14. Run *ifconfig* to see what the local IP of the VM is. On the host machine,
navigate to the local IP in a browser. The host machine's browser should be
able to be served files from the guest machine's local server!

Below is my VM configuration:

![VirtualBox Config](https://cloud.githubusercontent.com/assets/674727/23010992/3aa0a5d4-f3d3-11e6-87e7-6b253b65f840.PNG)

And here it is in action:

![VirtualBox Development](https://cloud.githubusercontent.com/assets/674727/23011801/cace6e3a-f3d7-11e6-9b6a-d140b4c940f6.gif)

Alternatively, instead of pointing directly to the IP, we could tunnel through
using ngrok as described in previous section.  This might become more of a
requirement as SSL becomes a requirement for WebVR. Although direct access is
much faster, and the IP method currently works for WebVR on Firefox Nightly.

I've also found that the VM sometimes loses internet connection (but still
connected to the host machine) when the network adapter is connected to
*Bridged Adapter* instead of *NAT*. So the ngrok method becomes a fallback in
this case as well.

## Record and Replay Tools

There will be an upcoming blog post dedicated to record and replay tools that,
for some use cases and scenarios, would let us develop WebVR on the go without
Windows nor a VR headset! This would be another WebVR workflow that would work
perfectly fine on OS X or Linux.

The A-Frame team is currently developing motion capture tools for A-Frame that
will let you record actions in room scale VR, output them to a file, and later
replay everything back without a headset.  Record some test cases in VR then
develop on them from the coffee shop!

![Motion Capture Tools Preview](https://aframe.io/images/blog/v0.5.0.gif)
