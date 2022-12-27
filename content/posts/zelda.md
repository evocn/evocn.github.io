---
title: "Movement in 'The Legend of Zelda'"
date: 2022-11-11T10:09:56-08:00
draft: false
description: "A cool trick from 1986."
tags: [games]
---

In *The Legend of Zelda* for the NES, I noticed a cool trick used to keep people
from getting stuck on the terrain. It looks like this:

![movement](/z_mov.gif)

There's something weird going on here that is hard to put your finger on, but
impossible to miss as you're playing the game. There's an effect, some nuance of
the movement, that keeps you from getting stuck on the terrain and keeps your
sword in line with the enemies.

To show what the game avoids with this effect, here's an example from a little
mock-up I made of this movement without the effect applied.

![mockup](/z_mock.gif)

You can see that the player gets stuck on objects. We don't want that. The
player's intention was clearly to move between the trees, but that intention
doesn't translate very well in my mockup. In Zelda, this rarely happens. Most of
the time you squeeze right through gaps like these. So how do they do it?

In the game, the player is allowed to move pixel-by-pixel. This gives the player
a high degree of control over their movements. However, in other games, this can
lead to some frustrating player experiences. You get stuck often. In some games,
you'd rather just move on a grid to avoid this problem entirely.

That's what Zelda does.

You can move pixel-by-pixel, as shown.
However, when you try and move on the other axis, it snaps you into place.
There's a hidden grid keeping you from bonking on objects!

![movement](/z_mov.gif)

As a note, Zelda's grid occurs on an 8-by-8 pattern, so Link takes up four
tiles. This also serves to continue the illusion of precise movement.

It's a great solution to the problem, one that gives this game a distinctive
feel. You can really get used to this kind of movement, and it becomes a pretty
deep and compelling system in its more demanding moments.

![combat](/z_com.gif)

The game is obviously well-known for being a sprawling adventure, magical in
ways other games aren't. However, its core mechanic often goes
underappreciated, and upon replaying it recently, I realized that what really
compelled me about the game was its dynamic combats. These combats are made
possible by this technique.

## Other options
How have other games solved this problem?

Look no further than *Link to the Past*, released five years later.

![link to the past](/z_lttp.gif)

This game opts to fudge things a little, with rounded hitboxes you roll off of.

It's hard to say which method is preferable. *Zelda 1* creates a system that
I've never seen repeated in a game – it makes combat which is compelling with
only a four-frame sword whose hitbox is the size of a pencil. LTTP, on the other
hand, is a lot bigger, a lot flashier, and, it can't be argued, a lot smoother.

There's something in the design of that original Zelda that really speaks to me.
A system without perfect control. It strikes a balance without feeling "smooth",
and that's what keeps Zelda in the realm of hard games. Every screen is a
life-or-death struggle. I find the combat and the movement in *Zelda 1* to be more
compelling than that of its successor. While the developers worked to remove
obviously annoying things from the game, it's still true to itself and its
system.
