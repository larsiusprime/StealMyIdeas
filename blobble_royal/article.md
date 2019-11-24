# Hook

Battle Royale: Humans vs The Blob.
If the blob eats you, you join it.

# Pitch

Battle Royale, but it's a 2D platformer where it's 99 humans against a giant amorphous blob, 
and any humans that get eaten by the blob JOIN THE BLOB, which is a bunch of players all controlling one entity collectively.

# Explanation

So you've got this map. 2D running around and jumping, and presumably being able to fight somehow (let's say swords and short-ranged guns).
There's one amorphous monster blob under computer control that starts in the center of the map, and starts out fairly small.
Everyone else is a human. Humans are all on the same "team" in the sense that they can't hurt one another directly. The only way
a human can be hurt is to be caught and digested by the blob.

The blob moves like an amoeba, via pseudopod projection. The blob is a certain amount of stretchable membrane stretched over 
a certain volume of cytoplasm. It can project a pseudopod out in one direction to stretch the membrane, and the terminal point
of this pseudopod moves sort of like a player -- it can run and jump, albeit slowly, and it's attached to the host blob, so it
has limited range. But by moving consistently in one direction it can drag the rest of the mass of the blob in that direction. The
pseudopod can also choose to "stick" itself so that it will cling to the current surface, allowing it to drag the whole blob up 
walls and platforms.

Whenever a human touches the blob, it risks being engulfed. After more than a second of prolonged contact with any part of the blob's
surface, a human will be stuck, and will have to jump vigorously to free themselves. After a few more seconds they will start to 
sink into the cytoplasm. Once completely inside the blob, they'll have a few final seconds before they are digested and converted
from a human player into a blob player. A human with enough luck and determination can sometimes free themselves from the blob, but
your chief hope of rescue is other human players. As long as a player is not yet fully digested, other players can free them by simply 
destroying the part of the blob that holds them. The blob has one additional tactics -- engulfing. By taking a pseudopod node and
wrapping it completely around a player (by jumping it over the player's head and making contact with the blob surface on the other side),
the player will be instantly deposited into the blob's interior cytoplasm, skipping straight to the final digestion phase.

Once a human has been fully digested, they're not out of the game -- now they're playing for the ever-growing team blob. Blob players
directly control pseudopod nodes, heck they *are* pseudopod nodes. There'll be some visual indicator (a colored circle or something 
with their initials?) that ties them to their previous identity as a player, which is what they control on screen. Whereas human
players are all playing individually, team blob is a team effort. If a bunch of pseudopods all pull in the same direction, they can
move the blob *fast*. But if they pull in opposite directions, they'll slow the blob down. If there's enough tension (literally) within
the blob, pulling in different directions, the pseudopod nodes can literally pull the blob monster apart. This might have some
strategic advantages in certain situations, but usually puts the divided blob players at a disadvantage because a smaller blob
is easier to kill. This is because blob players can actually move quite quickly *within* the cytoplasm of the blob, and are only 
slow when they are tugging against the stretchy blob membrane at the edges. Also, blob nodes are well protected inside the blob's
cytoplasm. Players can attack and even kill blob nodes. 

Attacking the blob causes its cytoplasm to deplete at the target location. If a player attacks an extruded pseudopod, they can 
divide the blob into pieces and isolate blob players within it. Then, by destroying all the remaining cytoplasm around that blob
player, they eliminate them from play.

The blob cannot be defeated, however, its victory is inevitable. Any damage to its cytoplasmic volume is temporary, and it will
soon catch up. Besides that, it is constantly growing, and blob players can accelerate that growth with every player they consume 
and various food power ups they digest along the way.

# Scoring

The scoring system intends to encourage the following kind of play:

- Human players should want to survive as long as possible while remaining human
- Human players should be torn between competing against each other (be the last one standing) but also form small group alliances to 
cooperate against the blob
- Human players should fear death and seek safety
- Blob players should want to cooperate entirely with other blob players as efficiently and totally as possible
- Blob players should fear cowardice
- All players should have something rewarding and fun to do regardless of whether they're currently a human or a blob or how much time
they've spent on either side in the current match

So here's a stab at achieving that:

- Long term progression has both Human and Blob statistics/scoring
- When you become a blob, you're not "done," now you work on your blob statistics
- The longer you last as a human, the stronger you are as a blob when you spawn in
- If you stick out a blob match from start to finish and cooperate well (rather than raqeguitting as soon as you get blobbed), 
in your next match your human will spawn with some better starting equipment or something
- Blob nodes share any scoring point just by being near eachother. Do we reward kills? All blob players who were close to the kill site 
get equal credit, each getting a full share (not diluted amongst them). 
- Blob nodes get a constant score bonus for spending time close to the membrane surface, where they are most vulnerable.
- Blob nodes get a constant score bonus just for spending time close to other blobs, with the exception of no bonus points gained
while hovering around the safe center of the cytoplasm.

- Three different flavors of ranking per match
  - Human: last human standing rank. #1, #2, #3, etc.
  - Blob: most valuable pseudopod rank. #1, #2, #3, based on how much you contributed (kills, power-ups, and pulling together)
  - Overall: some combination of how long you lasted as a human + how much you contributed as a blob per unit of time spent as a blob.
