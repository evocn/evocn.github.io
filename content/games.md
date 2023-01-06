---
title: "Games"
date: 2022-12-26T23:11:03-08:00
draft: false
---

These are the games I've worked on.

### Emblem ([github](https://github.com/evocn/emblem))

{{< figure caption="a scene from an early prototype." src="/emblem.png"
title="prototype">}}

A work-in-progress.


A small-scale tactics game in the vein of *Fire Emblem* and *Into the Breach*.

Developed from scratch (minus SDL) in C++.

### Experience
A walking simulator inspired by *Myst* and *The Witness*.

School project with a group of three, 
developed over the course of 10 weeks from scratch in C++ and OpenGL.

We used libraries to open windows, load meshes, do some math, and run audio, but
everything else was us.

{{< figure caption="We built three levels expressing different parts of the creative experience." src="/experience_2.png"
title="GUI for the level editor">}}

{{< figure caption="the starting area. Shadow-mapping is expensive, so we implemented view-frustum culling to keep the games running smooth on our dinky little macs."
    src="/experience_3.png"
    title="forest">}}

{{< figure src="/experience_1.png"
title="desert">}}

{{< figure src="/experience_4.png"
title="street">}}

{{< youtube 9Me2BgbvU00 >}}

Don't look at the code – lots of ***lessons*** learned in there.
If you must, here's the [github](https://github.com/CPE-476/Experience).
