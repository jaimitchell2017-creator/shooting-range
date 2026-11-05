# Storm Drop

A 3D battle royale that runs in your browser from a single HTML file. Ride the battle bus, jump when you choose, glide down on a hoverboard, loot chests, outlast the shrinking storm, and unlock new guns by playing.

## Quick start

1. Open the game in your browser and press **Play**.
2. The lobby searches for players for 30 seconds. If fewer than 5 players join, bots fill the match up to 10 fighters. You can press **Start now with bots** to skip the wait.
3. You start on the battle bus. Press **Space** to jump.
4. Your hoverboard equips automatically. Land near a glowing chest, grab a gun, and be the last one standing.

Click the game to capture the mouse. If mouse look does not work in your browser, use the arrow keys to aim.

## Controls

| Key | Action |
| --- | --- |
| W A S D | Move |
| Mouse | Aim |
| Left click | Fire (hold for automatic guns) |
| Shift | Sprint on foot, boost on the hoverboard |
| Space | Jump from the bus, jump on foot, fly up on the hoverboard |
| C | Dive down on the hoverboard |
| F | Hop off or back on the hoverboard |
| E | Open a nearby chest |
| R | Reload |
| 1, 2, 3 | Switch weapon slot |
| Arrow keys | Aim without a mouse |

## How a match works

- **Lobby:** 30-second countdown. Fewer than 5 players means bots fill the match to 10 fighters. With no other players, you are the only human and the rest are bots.
- **Battle bus:** Flies across the map at 190m for about 30 seconds. Bots jump at random times. If you have not jumped by the end of the route, you are dropped automatically.
- **Hoverboard:** Equips when you leave the bus. It hovers at least 2.5m above the ground, so you can fly over the map, shoot, and open chests. Press **F** to step off.
- **Storm:** The safe zone starts 450m wide and shrinks in five stages. Standing outside it costs HP every second, and the damage grows each stage.
- **Win:** Be the last fighter alive for a Victory Royale.

| Stage | Safe zone radius | Storm damage per second |
| --- | --- | --- |
| 1 | 450m (holds 75s) | 1 |
| 2 | 300m | 2 |
| 3 | 180m | 3 |
| 4 | 90m | 5 |
| 5 | 30m | 7 |
| 6 (final) | 8m | 10 |

## Chests and loot

Golden beams mark chests. Walk up and press **E**. Each chest gives a random gun from the ones you have unlocked plus 25 HP (up to 100). You carry up to three weapons. Finding a gun you already hold refills its magazine, and when all three slots are full the new gun replaces the one in your hand. Chests only give the Pistol if it is the only gun you have unlocked.

## Weapons and unlocks

You earn XP at the end of every match, and your total is saved in your browser. Each XP threshold unlocks a new gun that can then appear in chests. Headshots deal double damage.

| Gun | Unlocks at | Damage | Mag | Fire mode | Range |
| --- | --- | --- | --- | --- | --- |
| Pistol | 0 XP | 18 | 12 | Semi-auto | 150m |
| SMG | 200 XP | 10 | 30 | Automatic | 110m |
| Assault Rifle | 600 XP | 19 | 30 | Automatic | 220m |
| Shotgun | 1,200 XP | 12 x 8 pellets | 6 | Semi-auto | 50m |
| Sniper | 2,000 XP | 95 | 5 | Semi-auto | 400m |
| Plasma Cannon | 3,200 XP | 40 | 18 | Automatic | 260m |

**XP per match:** 100 per elimination, plus 25 for each placement above 10th (for example, 2nd place earns 225), plus 20 per full minute survived, plus a 300 bonus for winning.

## The world

- Endless terrain is generated in chunks around you as you move: hills, lakes, beaches, rocky slopes and snow peaks, with pines, oaks, bushes and rocks.
- The sky has a sun, drifting clouds and fog, with soft shadows and filmic tone mapping.
- The playable area is the shrinking storm circle. The terrain itself keeps going past it.

## Bots

Bots ride the bus, drop in on hoverboards, wander toward the safe zone, and fight whoever they spot within about 85m, including each other. They find better guns over time. They take hits only once they land, and they deal reduced damage compared with a human player.

## Tech notes

- One self-contained HTML file using [three.js](https://threejs.org) r128 (loaded from cdnjs) over WebGL. No WebGPU is required.
- Progress is stored in `localStorage` under the key `sd_xp`. Clearing site data resets your unlocks.
- Pointer lock is used for mouse look, with arrow keys as a fallback.

## Tweaking the game

Constants live near the top of the script, so they are easy to change:

- `MATCH`: total fighters per match (default 10).
- `PH`: the storm stages as `[radius, shrink seconds, hold seconds]`, and `SD` for the damage per stage.
- `BUS_Y`, `BUS_V`, `BUS_T`: bus height, speed and route duration.
- `W`: the weapon table (damage, fire rate, spread, magazine size, reload time, range, unlock XP).
- `CS` and the chunk radius in `updChunks`: how much world is drawn around you.

## Known limitations

- Only you are a human player. A web page like this cannot find other people on its own, so real online matches would need a game server. The lobby rules (5 players in 30 seconds, otherwise bots) are already in place for that.
- Trees, rocks and bushes are decoration. They do not block movement or bullets.
- There is no fall damage, and there are no shields or building.
- Many trees and shadows can be heavy on low-end laptops. If the game stutters, a quality toggle would be the next thing to add.
