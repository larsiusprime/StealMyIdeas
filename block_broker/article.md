# Block Broker

Tetris 99, but you can bid for pieces you need and sell ones you don't. 
"My kingdom for a long piece!"

So a while back I made this little experimental library called [BazaarBot](https://github.com/larsiusprime/bazaarBot)
which I [wrote about on Gamasutra](https://www.gamasutra.com/blogs/LarsDoucet/20130603/193491/BazaarBot_An_OpenSource_Economics_Engine.php).
The basic idea was to create an "open source economics" engine, which is to say
a glorified auction house API. It turned out to be a lot trickier than I 
expected to turn it towards any useful kind of end, and the [research paper](https://www.academia.edu/2600455/Emergent_Economies_for_Role_Playing_Games) I 
based it off of has attracted [some criticism](https://github.com/larsiusprime/bazaarBot/issues/17).
I [refactored](https://github.com/larsiusprime/bazaarBot/tree/refactor) BazaarBot
in response, but have never gotten around to making anything really interesting
with it.

A big problem with making an econ game is what I call "The Vanilla Ice Cream" problem.
The econ sim is a sort of system that requires an underlying sim where various
agents are actively doing something and using and consuming resources before it
makes any kind of sense to drop a market system on top. And then, you wind up
spending so much time making little goblins or whatever wander around a forest
and hunt pigs and chop down trees and build houses that you never get around to
building your econ sim, which is all you wanted to do in the first place! What
you're really interested in is the chocolate syrup and the nuts and sprinkles,
but you spend all your time just trying to churn up the boring Vanilla ice 
cream instead.

"Block Broker" was an attempt to find the simplest and stupidest "Vanilla Ice
Cream" to layer a market system on top of. I was on a walk with my wife one day
and she suggested Tetris.

It could work! Maybe!

So, you get a bunch of people playing Tetris simultaneously. Tetris 99 is a good
example, but this would probably be a little less directly competitive for some
reasons that will become clear. Also, the other players don't *have* to be
human, they could just as easily be computers, or a mix of AI and human. In any
case, you're playing Tetris, and so are a bunch of other people, and you're all
connected in a single game session somehow.

The Tetris company has [standardized modern Tetris](https://tetris.fandom.com/wiki/Tetris_Guideline)
with a few key features -- the two most salient for this article being the "Hold
piece" mechanic that lets you save one piece for later, and the ["7-bag" random
generator] which decides which piece comes next. As the name implies, every 
sequence of seven pieces is guaranteed to contain one of each of the seven 
possible Tetromnioes in the game, shuffled in random order within each "7-bag".
This means that the longest time you will ever go waiting on a long piece is 12
pieces: when it comes first in one bag, and last in the next one.

So in Block Broker, we expand on the "Hold piece" mechanic. Your "Hold piece"
box becomes your "Sell piece" box, and you can adjust the price you want to sell
it for. The default price is "Not for sale", but flicking e.g. the left analog 
stick up and down (you use the DPAD for normal play) will allow you to adjust 
your asking price up or down. In addition to the "Hold piece" box, you have a 
"Want piece" box. You can switch what piece you want by flicking the right 
analog stick left and right, and you can adjust the price you're willing to pay
by flicking it up and down (or maybe use L & R to switch pieces, I dunno -- 
controls will be essential for implementation but I won't settle that issue now).

So you can offer your hold piece for sale, and you can ask for a certain piece
from the market, and you can set a price on each. What's the currency? We could
either go with score or lines. Probably score, because scoring a Tetris should
be worth more than just 4x the currency reward of a single line.

Offers are resolved in real time. When you adjust the price on your ask/sell
boxes, a short timer will time out and then make those prices live. (This way
you can kick a price up or down without it resolving instantly halfway to your
target price). A BazaarBot-like auction house will then resolve orders -- if the
price you're willing to pay for a given piece is equal to or higher than the 
selling price someone is offering, then their sell box is cleared, the money is
transferred, and that piece will be the next one that drops for you. I'm not 
sure how you resolve a buy price that matches to a lower sell price -- I'd start
by just giving the seller the price the buyer offered, even though it's higher
than what they asked for. Other alternatives are to match the seller's lower
price (but give the highest price priority in matching), or to clear at the 
average of the buy & the sell price. At any rate, offering to pay more to buy
should reliably get you your pieces faster than those offering to pay less, and
offering to sell for less should reliably clear their inventory faster than 
those offering to sell for more.

Okay, so we've got multiplayer Tetris with buying and selling of pieces. What is
this going to look like and what else needs to change?

Managing attention is the first thing that has to be handled. Tetris 99 is hard
enough to play when you're just trying to do the Tetris, managing the strategy
of who to target is a whole nother level, and most people just stick to flicking
the analog stick to one of the four AI targetting modes. For this reason I think
this sort of game would work best when you can't directly compete with the other
players by sending garbage and trying to knock eachother out. You'll also 
probalby need to add some "breathing moments" where the player has time to pay
attention to the market and adjust their buy/sell orders. Natural moments might
be when you make a Tetris, or perhaps there's a regular pause every tenth drop
or something for every player. If you do put competitive garbage lines in, 
perhaps that comes with a momentary pause.

The next this is the 7-bag randomizer might need to go. The purpose of that
mechanic is to smooth out the randomization, because with a perfect RNG it's
entirely possible you could *never* get a line piece, and any other number of
pathological cases like a ridiculously long string of nothing but S or Z pieces.
It also ensures that given sufficient dexterity and skill, you can continue
playing forever. With a truly random bag that makes no guarantees you could be
forced into a game over regardless of skill. But that's all because in standard
Tetris, you have literally no recourse to getting pieces from anywhere else. In 
Block Broker, we have the market as a way to get pieces that you need.

And this is where things get interesting.
 
# So What?

We can now create all number of interesting and/or pathological simulations. We
could create a game where 99 players compete with one another, all get a mostly
reasonable mix of pieces, and just see what happens when they can also trade.
Or, we can take that same scenario, but each player only ever gets one kind of
piece -- an economy of narrow specialists -- and they *have* to trade to do much
of anything. And do some lucky jerks get nothing but line pieces all day, which
they can either stack together for cheap Tetrises, or sell on the market for 
massive profits? This is getting kind of darkly educational all of a sudden.

The varieties are endless -- what does it look like when you're sending garbage 
back in forth in standard competitive Tetris fashion, versus when you're just 
competing individually to get the best score and can't hurt each other directly?

What's it like with the 7-bag system, does that reduce the need to trade?
What's it like if we simulate "weather" conditions, and certain people get a 
"drought" or "bumper crop" of line and l pieces? What if someone gets a "plague"
not of locusts or weevils, but of squares and S/Z pieces?

I see "Block Broker" less as a specific variant of Tetris and more as a platform
for economic and psychological experiments with Tetris as a basis.