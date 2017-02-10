---
title: A-Frame v0.5.0 - Features & Tools
date: 2017-02-09 10:00:00
layout: blog
image:
  src: v0.5.0.gif
---

Give A-Frame a high five for the release of **v0.5.0**!

## What's New?

[mattdesl]: https://twitter.com/mattdesl
[three-bmfont-text]: https://github.com/Jam3/three-bmfont-text
[text]: https://aframe.io/docs/0.5.0/components/text.html

A **text** component, using SDF and MSDF, has landed into A-Frame core! Based
on [mattdesl's][mattdesl] [three-bmfont-text], the text component has gone
through a long lineage starting with bryik's initial
`aframe-bmfont-text-component` to fernandojsg's improvements to mchen's fork to
mchen shepherding the component into A-Frame. The text component comes with
several stock fonts and supports custom fonts, alignment, anchors, baselines,
spacing, and wrapping. [Read more about the text component][text].

![Text](https://cloud.githubusercontent.com/assets/674727/22808347/4daf3bc4-eee0-11e6-9af7-048faf188b0f.png)

[aboutgltf]: https://www.khronos.org/gltf
[gltf]: https://aframe.io/docs/0.5.0/components/gltf.html

The **glTF model** component has also landed into A-Frame core! glTF (GL
Transmission Format) is an open project by Kronos providing a standard
efficient 3D file format that is tailored for transmitting models over the Web.
The `gltf-model` component loads a 3D glTF model with a line of HTML. Note that
glTF is a fairly new specification and adoption is still growing, but a large
portion of the WebVR community are optimistic that glTF will become the `.jpg`
of 3D assets. [Read more about the `gltf-model` component][gltf].

[releasenotes]: https://github.com/aframevr/aframe/releases/tag/v0.5.0

Notable bug fixes include:

- Fixing mobile iOS resolution and bluriness. Thanks to
  [nullcode](https://github.com/nullcode) for the fix!
- Fixing Cardboard support for many mobile devices, especially those with large
  screens. Thanks to [@thoragio](https://twitter.com/thoragio) for forking
  WebVR polyfill to update its device database.
- Fixing and forking WebVR polyfill for better WebView support. Thanks to
  [grigorkh](https://github.com/grigorkh) for the fix and
  [andymartinwork](https://github.com/andymartinwork) for QAing.

Check out the [release notes][releasenotes] for the complete changelog,
includes a list of all new features, optimizations, and bug fixes.

### Record and Replay Tools

<!-- more -->

## What Have People Built?

<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

<div class="tweets">
https://twitter.com/fernandojsg/status/821471460871041024
https://twitter.com/kfarr/status/825643364519251968
https://twitter.com/aframevr/status/824458764354940928
https://twitter.com/whoyee/status/821271916451229697
https://twitter.com/micahstubbs/status/814622454597328896
https://twitter.com/JonathanZWhite/status/816755095371137024
https://twitter.com/maros_pekarik/status/815912259704750080
https://twitter.com/andgokevin/status/819899447169560577
</div>

## What's Next?
