---
title: "How to model light with computers"
date: 2022-10-31T22:26:25-07:00
draft: false
description: "Understanding the underlying concepts of a basic ray tracer."
tags: [code, graphics]
---

Over the last few weeks, I've been poking around with a basic ray-tracer.
It's been fun to tweak values, but it's my intention to fully understand
everything that's going on under the hood.

[Studies show](https://psycnet.apa.org/doiLanding?doi=10.1037%2Fedu0000071) that
teaching (or preparing for teaching) a subject leads to deeper understanding.
Therefore, I'm going to try to explain the concepts at as simple a level as is
possible here, for the sake of really grokking this stuff myself. 
Consider this a 30,000 foot overview of ray-tracing.

## A Basic Model of Light
In general, here's the idea:
When we experience the sensation of sight with our eyes, what is truly happening
is that rays of light reflect off of objects in our environment, eventually
arriving at our eyes.

![Figure 1](/ray_f1.jpeg)

All insights build from this, so understanding this deeply is vital.
There are minor details to this model that aren't immediately obvious as well.

### Nuances
Objects always appear to have a **color**. This color is a property inherent to
the object, but it appears that way because it **reflects** that color of light,
and **absorbs** all other colors of light.

> An example of this phenomena in action is plant photosynthesis. Plants appear green
> to us, which means that they absorb other types of light (red, blue).
> it is well documented that plants are completely unable to absorb green light.
> Therefore, a plant washed in green light and nothing else receives just as
> much nutrition as one in pitch darkness.

Objects also appear to have a **surface** type.
These surfaces are defined by the particular way in which light reflects off
of an object.

**Specular** surfaces reflect light perfectly.
> A good example of this is a mirror. Given a ray in, you can trace the bounce
> off the surface perfectly.

**Diffuse** surfaces are rough, and therefore reflect light imperfectly.
> An example of diffuse surface is... Pretty much everything around you. Stone,
> wood, fabric, etc.

![Figure 2](/ray_f2.jpeg)

A final note, light often only finds your eye after one or two or ten
**bounces**. A bounce is what happens when a ray hits an object and then hits
another object before hitting your eye. This bouncing property is generally
responsible for the principle of **ambient** light.
> Look under your desk right now. There's not a direct path from your light
> source to that point under your desk, but it's still illuminated due to light
> bouncing off of the rest of your environment and then bouncing from that
> otherwise dark point.

There are a variety of other crazy situations with light, but armed with this
basic axiomatic model of light, one can start to understand them. How does glass
work? What about water? These answers are just a few short minutes of reflection
(or a google search on the word *refraction*) away. It's a very wonderful
system.

Once you've got a good handle on how light functions, we can start talking about
how we can implement this model in our computers!

## Rays
We consider our eyes to be a singular point for the sake of computing light.
We call that point our origin.
Emanating from this point are rays.
> You may be asking: Why are the rays **coming from** our eyes, when light
> actually comes **into** our eyes from light sources in real life?
> A perfectly reasonable question. In fact, this is the first of many completely
> inaccurate approximations we make for the sake of **performance**.
> 
> You see, calculating all of the individual rays of light coming from all over
> the place is a lot of work. Especially when you consider all the rays that
> never even intersect your eye (the vast majority of rays that exist in your
> environment right now). Add to this the difficulty of calculating bouncing
> rays, which can theoretically be calculated to any depth

Those rays intersect with objects, "seeing" a color when they do.

A ray can be defined by the following relation:

> P(t) = A + tb
>
> P is a point on our ray.
>
> A is the origin point.
>
> b is the direction vector.
> 
> t is how far along the ray you are. t = 0 is the origin. Positive t values
  result in a point in the path of the direction vector starting at the origin
  point.
  For our purposes, a ray generally only refers to positive t values.

![Figure 3](/ray_f3.jpeg)

## Collisions
So we have rays. What do they do?

These rays are going to tell us information about a 3D space.
Much in the same way that light bounces off objects into our eyes, which allows
us to tell what objects are where in space, our rays are going to collide with
objects and do the same.

The way we do this is through **collisions**. Collisions are useful in all sorts
of programming, from graphics to gameplay to everything inbetween. This is the
science of determining if some object is in the same place as
another object, and what it means when it is.

> An example can be found in all manner of computer games. Fighting games are
> especially collision-focused. A character's attacks generate a bunch of boxes,
> which check against an opponent's boxes, and each of these must determine if
> they collide. If so, damage is done.

In the interest of simplicity, most basic ray-tracers use spheres. You'll see
them all over the place online.
The reason for this is that sphere collisions are the easiest collisions to
detect. Let's go over this collision.

> Ray-Sphere Intersection
>
> A sphere at the origin can be defined by the following equation:
>
> x^2 + y^2 + z^2 = R^2
>
> Where
>
> x,y,z is the center of the sphere.
>
> R is the sphere's radius.
>
> In other words, if a point and radius satisfies this equation, it is on the
> sphere's surface. If the left side of the equation is larger, it means that
> the point is outside of the circle. If the right side is larger, the point is
> inside the circle.
>
> We can generalize this equation to a sphere at an arbitrary point (a,b,c):
>
> (x-a)^2 + (y-b)^2 + (z-c)^2 = r^2
>
> This can also be written in the following way:
>
> (P-C)^2 = r^2
>
> Where
>
> P is our given point
>
> C is the circle's center.
>
> This equation is the one we will use to represent a sphere in space.
> In order to calculate whether a ray collides with the sphere, we need to
> determine if a point is in the sphere or not. Thankfully, we have a
> relationship which defines a ray at a point already:
>
> P(t) = A + tb
>
> We can therefore substitute this in for the point value in the circle
> equation:
>
> (A+tb - C)^2 = r^2
>
> And to move all of this to the left side and simplify, we get:
>
> t^2 * b + 2tb * (A-C)+ (A-C)^2 - r^2 = 0
>
> Now we only have one unknown value – t, and we have a quadratic equation. 
> 
> We can solve this equation and find our roots. There are three possibilities:
> 
>   0 Roots means that we don't have a collision.
>
>   1 Root means we collide with the edge of the sphere.
>
>   2 Roots means we collide with the sphere and punch through the other side.
>

So we have our collision detection in place.
In this case, we want to determine whether our ray collides with an object in
space. If it does, we know there's an object there. Once we have determined
there is a collision, then we engage in **collision handling**. This process
varies greatly from program to program.

> Mario colliding with the ground and colliding with a goomba use the same
> collision detection algorithm, but result in different collision handling.

In our case, when a ray collides with an object, we will tell it to illuminate a
pixel based on what that object's color should be. This is a huge step, so let's
break it down.

## Filling a canvas
Firstly, our screen is a large canvas of pixels. At first, they're blank.
Our foundation implies that we can color pixels whatever we want them to be,
with something like blitToScreen(120, 335, RED), which makes a pixel at x=120, y=335
change to red. We can set these pixels to be whatever we like, but we know we
only have so many of them, determined by our **resolution**. Resolution is based
on your monitor's pixel density and size.

So we have a good number of pixels, maybe 1920 by 1080. The ratio between these
numbers is also important to think about. It's basically the type of rectangle
we want to render to. When you hear people talk about an **aspect ratio**, or
mention that a movie is in *widescreen* or *4:3* or *16:9*, they're talking
about aspect ratios. We can choose our aspect ratio as programmers, meaning that
we can make square shots or super wide, epic shots. Pretty cool to play around
with.

Secondly, those pixels are our end result, so we need to capture data for each
of them. Imagine casting rays at a sheet with a pinhole with just one pixel
open. If we shoot a ray through there, we will get collision information through
that one point.

In order to populate our screen, we need to consider a pinhole at each of the
pixels of that sheet. We call this a **viewport**.

> For our simple example, the image and viewport should have the same aspect
> ratio. However, they need not have the same number of pixels. If this is the
> case, consider the consequences. One could get a ton of rays in different
> points and then average them to get a pixel's color, creating the illusion of
> precision even though we don't have enough pixels to truly create the precise
> lines the source has. This technique is known as **anti-aliasing**, and it's
> happening all over your computer right now to render smooth looking fonts,
> graphics, and more.

If we send a ray through each of these points on our viewport, from the origin,
we get a good sample of where objects are in the world, and we end up with a
result like this!

![Figure 5](/ray_f5.jpeg)

Stay tuned for next time where I will discuss how we make this look like a real
3D shape.
