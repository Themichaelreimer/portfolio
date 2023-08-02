---
title: Terminal Adventure 
publishDate: 2021-12-04 00:00:00
img: /assets/projects/terminaladventure/cover.png
img_alt: Iridescent ripples of a bright blue and pink liquid
description: |
  It's a game about nothing!
  Descend the pointless dungeon, collect magical artifacts and slay the dragon to reclaim your wallet so you can get on with the rest of your day.

tags:
  - Game
  - Lua
  - Love
  - Devlog
  - Retrospective
---

## Retrospective

Video retrospective + gameplay coming soon

### Lessons Learned
The game isn't that fun. But that's ok. All in all, I had a great time making this game and am still proud of it years later. I got some great experience and lessons from it too, including really appreciating the power of architecture. At week 8, I did a major refactor and transitioned a major section of the project from an object oriented architecture to an Entity-Component-System architecture. Doing this, I found three huge benefits:

- The performance increased substantially. It's well known that ECS tends to be the best for performance for real time games due to the much better processor cache efficiency, but now I had real life experience showing how much of a difference it makes. I was able to quadruple the number of rays cast in lighting, and still had better, smoother performance than before.
- Emergent properties, and amazing seperation of concerns: Systems were able to interact together in ways that produce interesting and logical results, without the developer necessarily having to think of every possible interaction, or even necessarily have systems be aware of the existence of other systems.
- The ECS code is simply easier to understand. When you think about what you want things in games to do, you tend to describe very general processes and concepts, which map very nicely onto ECS. It can be unconventional at first for someone used to thinking in typical computer-science ways, but it's conceptually a lot closer to how non-technical humans like to think about things.

> So what is ECS anyway?

ECS stands for Entity Component System. It is a classic 3 tier architecture design where the responsibilities are split thus:
- Components: Components are properties that entities can have. Components in and of themselves have no functionality, and are essentially just C style structs, plain old objects, etc. Examples of components might include: "Sprite", "Name", "Color", "Mass", "RigidBody" and so on.
- Entities: Entities are collections of components. Like components, these are "dumb" and contain no real functionality.
- Systems: This is where the magic is. In a system, we have a set of entities with <em> all the necessary components needed to accomplish a desired behaviour.</em> For example, in a gravity system, we will get the set of all objects that have mass and a position. We then process gravity for all objects all at once.

The result of this architecture is excellent seperation of concerns, excellent cache locality, and getting to develop a game entirely by coding "concepts" instead of "objects that do things".

### What from here? What would I do differently next time?

It's unlikely I'll do much more with this in the current implementation. Rebooting this in another language with better multithreading support and better libraries is certainly possible ;).

Some of the improvements on my mind that would be great to deliver:
- Pixel-based lightmap instead of tile-based lightmap for smoother light.
- Saving and loading games. Save file would probably be implemented via SQLite, with some code to delete your .db file on death :)
- Drastically expanding config options, for example, letting users define their own colour pallete for ASCII mode. Modding support by re-constructing as much of the engine as possible into data instead of code, and making it easy for users to change this data.
- Making the dungeon less linear, with branching paths where one room can lead to many rooms
- Making combat fun. In hindsight, one of the biggest problems on this front is that the sword's hitbox actually moves with the sword, and is <em>too</em> accurate. It probably would have been more fun for the sword to just simply hit whatever is in a fixed region instead of getting too complex about it. The too accurate hitbox also creates a problem, where if the sword moves too fast, it can skip over the enemy's hitbox entirely in a frame, and if it's too slow, the player doesn't feel that it's satisfying.
- More content. More kinds of enemies. A game like this would be fun because it forces the player to improvise differently in every run of the game. There's only 10 collectable items (and only one uses magic) and about 8 enemies all working off the same enemy-controller, so it really doesn't feel like there's much variety there.

## Devlog
This devlog was maintained on the Github repo during active development.

## Post-release Update
![](/assets/projects/terminaladventure/11.gif)
- Toggle between rendering via text-labels, or graphical tiles via `/`
- Smooth-lighting like shader
- Music
- Proper window resizing


## Weekend 13 (Demo v0.1 Updated)
- Fixed several bugs of varying severity
- Added Slime enemies
- Added health recovery items that sometimes drops from defeated enemies
- Several balance changes
- Work towards an item charging system

## Weekend 12 (Demo v0.1 released)
I've lost track of everything that got added, but:
- Added two new biomes
- Added lava and the state of being on fire
- Added start, death and victory screens
- Added 3 new items, including your Wallet
- Added Dragon, health recovery

Check it out!

## Weekend 11
![](/assets/projects/terminaladventure/10.gif)
![](/assets/projects/terminaladventure/9.gif)
  - Added Sound effects
  - Added alternate level generation algorithms, and the first variation: Flooded Caves
  - Added Water and Drowning for player and Enemies
  - Added inventory and inventory menu
  - Added a "Pink Plush" enemy
  - Added Life Jacket and LifeUp collectables


## Weekend 9/10
![](/assets/projects/terminaladventure/8.gif)
  - Introduced Enemies, AI, and a combat system
  - Added 2 new enemies: Snakes and Jackals
  - Re-introduced collectables with the Map, and X-ray glasses collectables
  - Fixed crashes and added screen-shakes on damage


## Weekend 8
  - Introduced an Entity-Component-System architecture and ported player, items, weapons, and lighting to ECS
  - Fixed lots of bugs, and improved performance

## Weekend 7
![](/assets/projects/terminaladventure/7.gif)
- Introduced bombs, destructable terrain, health/damage
- Introduced some new bugs
- Fixed some bugs

## Weekend 5/6
![](/assets/projects/terminaladventure/6.webm)
More variety in world generation; multiple floors, X-Ray glasses collectable


## Weekend 4
![](/assets/projects/terminaladventure/5.gif)
Lighting via raytracing and the beginnings of items and collectables


## Weekend 2/3


### GUI and Started Lighting
![](/assets/projects/terminaladventure/4.gif)
I swear this looks fine in person, I blame the gif encoder

### Sword, Camera, Colours
![](/assets/projects/terminaladventure/3.gif)

## Weekend 1


### Acceptable Physics
![](/assets/projects/terminaladventure/2.gif)

### Working out collision kinks
![](/assets/projects/terminaladventure/1.gif)
Player is allowed to rotate, and has the origin in the top-left corner, yielding wacky results
