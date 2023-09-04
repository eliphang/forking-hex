# Forking Hex 🔱⬢⬡
Find a move that connects two sides of the board and win crypto.

## Background
Forking Hex is based on the game Hex. The moves are the same. The innovation of Forking Hex is the addition of *forking*.

## Forking
Anyone (including new players who haven't previously made moves) can make a move on any *open* position. More than one move can be made on a position, creating forks.

Thus, Forking Hex is loosely a team game, with players continuing positions that seem to be winning or discontinuing positions that seem to be losing. Players can even play on both sides of the same game.

## Winning
There are no draws in Hex. This is also true for Forking Hex. A player who makes a losing move will forfeit the crypto deposit they made for that move to players on the other team who made moves before them. Winning and losing depends on the quality of the moves a player makes, not the team they belong to. Because Forking Hex is heavy on strategy (think "Go") and light on tactics (think "Chess"), making a losing move is rare, but every game will have at least one losing move. It's possible for teams to win some forks and lose others. There is no losing or winning team. Players are rewarded for being on the opposite team upstream from a player who makes a losing move.

## Rules
### Creating a game
Anyone can create a game, specifying

* the size of the board. John Nash said 14x14 is the optimal board size, but any square size is possible. The length and complexity of the game depends on the size.
* time per move for White (in blockchain blocks). This is how long a position stays *open* when it's White's turn, meaning how long players can make moves on that position, including forks.
* time per move for Black. This must be more than the time for the first team. Hex is ultra-weakly solved. This means we know that the first mover will always win with perfect play, but we don't what the perfect moves are. To balance this, we give the second mover (Black) more time per move.
* cost per move. Each move requires a deposit of crypto. Almost all deposits will be returned. Only a losing move loses its deposit, to be distributed to players on the other team.

### Beginning a game
The game begins after White makes a move and Black responds. The position after White's first move can't be forked, meaning Black's first move will be the only response. The first timer starts after Black's first move. The second position stays *open* for the number of blocks specified in "time per move for White". Anyone can make a move for white for this position.

### Moving
Anyone can submit a move to any open position. The move must place a piece of the color whose turn it is adjacent to an existing piece of the same color.

###


## Architectural considerations
### Submitting a proof of win
The smart contract doesn't check for the winning condition after each move, and in most games, a winning condition will never actually be played.

In the rare case a player plays a losing move that results in a win on the next turn by the other team, the winning player should make a winning move by submitting an array of all the hexes connecting one side of the board to the other. The smart contract will check that these hexes connect to each other in order, span the board and contain the correct color. If the check passes, the previous move will be considered a losing move.
