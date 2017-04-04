---
title: "Rapid Room Scale VR Development with Record & Replay"
author: twitter|andgokevin|Kevin Ngo
date: 2017-4-03
layout: blog
image:
  src:
---

> Read about [the initial release of the A-Frame Motion Capture Components and
> A-Saturday-Night](https://blog.mozvr.com/a-saturday-night/).

On the A-Frame team, we focus our development on experimentation and innovation
with the HTC Vive. But room scale VR can be cumbersome to develop. Every change
to the code, we have to:

- Open a web page (often running on a separate computer)
- Enter VR
- Put on the headset
- Grab the controllers (often having to turn them back on)
- Do our test run with the headset and controllers
- Take off the headset and controllers and pop open the browser development tools
- Restart the browser if necessary since they're currently experimental and buggy
- Repeat

Room scale VR development becomes molasses. But we've come up with a workflow
to supercharge VR development so we can automate, develop rapidly, and on the
go: **[A-Frame Motion Capture Components](https://github.com/dmarcos/aframe-motion-capture-components/).**

With the motion capture components, we can record VR actions (e.g., headset and
controller movement, controller button presses), and repeatedly replay those VR
actions, on any device from anywhere without a headset.

## Rapid Development

Rather than having to re-enter the headset and VR every time we want to test
something, we can take our recording, send it to, say, a Macbook, head out to a
coffee shop, and continue developing our VR application using the recording on
a stable browser.

Or we can record a bunch of different recordings as regression test cases and
QA.  Store the recordings, do some development, and occasionally click through
the recordings to make sure everything still works.

## How to Record

Here's how to set up the recording:

1. Drop the Motion Capture Components script tag into your HTML file (e.g., `<script src="https://unpkg.com/aframe-motion-capture-components@0.1.2/dist/aframe-motion-capture-components.min.js">`)
2. Add `avatar-recorder` component to the scene (i.e., `<a-scene avatar-recorder>`)
3. Enter VR
4. Press `<space>` to start recording
5. Record movements and actions
6. Press `<space>` to stop recording
7. Save the recording JSON file

Now we can replay the recording.

## How to Replay

By default, the recording will also be saved and replayed from localStorage. If
we want to take our recording on the go, here's how to replay a recording
(assuming we already have the script tag above):

1. Put the recording file somewhere accessible to the web page (e.g., in the project directory or on a CDN)
2. Add `avatar-replayer` component to the scene (i.e., `<a-scene avatar-replayer>`)
3. Specify the path to the recording in the `avatar-replayer` component (e.g., `<a-scene avatar-replayer="src: recording.json">`)

Then replay the recording on any device from anywhere without a headset to your
heart's content. Get in the headset, record some clicks, and then from a
laptop, we can build event handlers on top of the controller events we emitted
in the recording.

## Possible Features

To make it even easier, we'll may add some features to the motion capture
component at some point:

1. Specify a recording with query parameter so it doesn't have to be hard-coded into the HTML file
2. Start and stop the recording with the VR controller rather than the keyboard
3. Add in-VR indicators with a countdown to tell us when recording has started and stopped

Go forth. Innovate and experiment with room scale VR interactions!
