---
title: "Motion Capture Tools via the Inspector"
author: twitter|andgokevin|Kevin Ngo
date: 2017-7-18
layout: blog
---

[components]: https://github.com/dmarcos/aframe-motion-capture/

Earlier, we showed how [motion capture can supercharge VR
development](./motion-capture.md). After importing the [motion capture
components][components], taking a recording of the headset and controller
movements and events, and setting up the replayer, we can develop room scale VR
without needing to get into the headset nor grab controllers.

The only problem is that it takes some work getting all of that setup. We'd
have to find the motion capture components, include as a script tag, add the
`avatar-recorder` component, take a recording, save the recording, possibly
transfer it to another computer, and set up the `avatar-replayer` component.

To put this handy tool more at our fingertips, we've integrated motion capture
components into the A-Frame Inspector. The Inspector now has a UI for motion
capture development tools that:

- Injects and sets up the motion capture components (`avatar-recorder` and `avatar-replayer`).
- Can take recordings
- Can select between previously stored recordings for replay
- Can save recordings as a file
- Can upload recordings to myjson.com and get back a URL
- Can save and store recordings from the file system
- Can save and store recordings from a URL

The process of record and replay becomes:

1. Open the Inspector (`<ctrl> + <alt> + i`).
2. Open the motion capture tools (the film camera icon in the top-left, or hit `m`).
3. Type in a recording name and hit record.
4. Record (move around in the headset, interact with the scene with controllers).
5. Replay!

A couple of extra features are we can use the Inspector during a recording.
Imagine tweaking or moving boxes in front of a replaying avatar for it to grab.
We also have increase selection of cameras to view the recording from
(Inspector camera, first-person camera, or motion capture's spectator camera
toggled by hitting `q`).

As a bonus, we'll throw in a few free recordings! The Inspector will come with
several sample recordings to be available to replay on any A-Frame scene
including just a headset looking around, an avatar swinging its arms around, or
an avatar reaching out and grabbing something. These might be handy if those
recordings do it for us or we're away from our headset.

I mostly did this for myself since motion capture driven VR development has
become an indispensable part of my workflow. Having to get into the headset for
every single little code change is impossible, and I desperately wanted to
reduce the friction in setting up the tools, transferring recordings, or
selecting between recordings. Having to import the components was an obstacle
for a lot of people that might not yet realize the benefit of this; people
should now try motion capture driven development and see the light.
