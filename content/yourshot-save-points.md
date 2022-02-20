+++
title = "How I Added Save Points to YourShot"

description = "A quick brief on how I added save points to YourShot"
date = 2021-01-17

[taxonomies]
tags = ["yourshot", "tutorial"]
categories = ["Ramble"]
[extra]
+++

The time has come to add a proper method of saving to _YourShot_. <!-- more -->

Previously i had been using the Pause Menu to allow for saving, but I feel like it just doesnt fit the game, and also breaks immersion for a while when you're opening a menu, completely freezing the game, and then pressing save. I looked into a bunch of approaches. [This video in particular](https://www.youtube.com/watch?v=PJZByWHtzb8&ab_channel=NakeyJakey) was especially helpful. I wrote down most approaches that I saw, and heres a list:

- Autosaving
- Manual Saving Anytime, Anywhere
- Autosaving + Manual Saving
- Auto Manual Saving Prompts
- Quicksaves
- Save Rooms
- Save Points

And the one that really caught my eye were save points. Something about the feeling when you have to face off multiple encounters without saving when the next save point is to the end of the level/room is just something that I felt like would make for an enjoyable experience. But like most other manual saving options, this one can be very annoying if not done right. I stumbled upon [this thread](https://www.resetera.com/threads/save-points-in-games-examples-of-great-and-poor-execution.17575/) that had a variety of examples of save points executed well, and uh... not so well.

**My key takeaway from this thread** was that while big flashing odd-looking out of place saves may make themselves easier to find, most people don't seem to like them very much. I recalled that I had recently implemented a choice system for YourShot already, so why not use that, and enable you to interact with a Save Point that shows information on your current whereabouts and whatnot, and ofcourse allows you to save the game. So, lets get right to it!

First, I needed a Sprite for the save point, so I made this weirdish spr-ite that gets darker each frame, before looping back. It actually turned out alright in game though.![Save Point Image](https://i.ibb.co/QN95WtX/savepoint.png)

Next, I used the choice system that i had recently made for setting up a dialogue for the save point interaction. Heres how it looks in game:
![Dialogue Interaction](https://i.ibb.co/nQBX0mC/Epic.gif)

Then I just needed to do some backend stuff like hooking the savepoints `OnDialogueEnd` event to a `GameManager.Save()` function.

And yeah that was about it! I turned this save point into a [Unity Prefab](https://docs.unity3d.com/Manual/Prefabs.html) and now I can populate my levels with save points.

I want to keep a healthy balance of save points for YourShot. I dont want them to be too scarce, but I also want to make it a challenge to reach them. For frequency its gonna be somewhere from an _Undertale Savepoint_ to a _Dark Souls Bonfire_.

That was about it for now, I really want to get to work now on implementing a unique health system as well as some fun combat, and thats probably what im gonna work on next.

I currently have exams that'll probably last around like 2 weeks, so I wont really get much time to work on the game at all, but I try to jot down any ideas i have, and they're pretty pog not gonna lie.
![PeepoSmug](https://i.ibb.co/PTjt73R/789549358080720916.png)
