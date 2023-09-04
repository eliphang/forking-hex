# Forking Hex 🔱⬢⬡
Find a move that connects two sides of the board and win crypto.

## Background
Forking Hex is based on the game [Hex](https://en.wikipedia.org/wiki/Hex_(board_game)). The innovation of Forking Hex is the addition of *forking*.

## Forking
Anyone (including new players who haven't previously made moves) can make a move on any *open* position. More than one move can be made on a position, creating forks.

Thus, Forking Hex is loosely a team game, with players continuing positions that seem to be winning or discontinuing positions that seem to be losing. Players can even play on both sides of the same game.

## Winning
There are no draws in Hex. This is also true for Forking Hex. A player who makes a losing move will forfeit the crypto deposit they made for that move to players on the other team who made moves before them. Winning and losing therefore depends on the quality of the moves a player makes, not the team they belong to. Because Forking Hex is heavy on strategy (think "Go") and light on tactics (think "Chess"), making a losing move is rare, but every game will have at least one losing move.

## Rules
### Creating a game
Anyone can create a game, specifying

* the size of the board. John Nash said 14x14 is the optimal board size, but any square size is possible. The length and complexity of the game depends on the size.
* time per move for White (in blockchain blocks). This is how long a position stays *open* when it's White's turn, meaning how long players can make moves on that position, including forks.
* time per move for Black. This must be more than the time for White. Hex is ultra-weakly solved. This means we know that the first mover will always win with perfect play, but we don't know what the perfect moves are. To balance this, we give the second mover more time per move.
* cost per move. Each move requires a deposit of crypto. Almost all deposits will be returned. Only a losing move loses its deposit, to be distributed to players on the other team.

### Beginning a game
The game begins after White makes a move and Black responds. The position after White's first move can't be forked, meaning Black's first move will be the only response. The timer starts after Black's first move. The second position stays *open* for the number of blocks specified in "time per move for White." Anyone can make a move for white for this position.

### Moving
Anyone can submit a move to any open position. The move must place a piece of the color whose turn it is on an empty hex. Moving requires a deposit equal to the "cost per move" setting. Move deposits are returned unless the move is a losing move.

### End
The game ends when the timers have expired for all positions.

### Losing positions and moves
A losing position is one in which all positions directly after it are winning positions. A winning position has no positions after it. A winning position might satisfy the winning condition of Hex, connecting two sides of the board, or it might have closed without any moves played on it (because every player considers it to be winning).

A losing move is a move that creates a losing position.

### Rewards and penalties
After a game has ended, players can reclaim their move deposits minus penalties and plus rewards.
#### Penalties
Each losing move forfeits its deposit as a penalty. A small percentage of each penalty goes to the developer fund and the rest is distributed as a reward.
#### Rewards
Each losing move is traced back from the losing position to the starting two moves, only considering moves from the opposite color to the losing move. A player receives a portion of the reward equal to the number of moves they made in this trace divided by the total number of moves in the trace. For example, if the losing move was a Black move, and there were 40 White moves before it, and a player made 5 of those moves, they would receive 1/8 of the reward.

## Architectural considerations
### Submitting a proof of a winning position
The smart contract doesn't need to check for the winning condition after each move, and in most games, a winning position will never actually be reached, because players will see in advance when positions are losing.

If a player plays a losing move that results in a win on the next turn by the other team, a player from that team should make a winning move by submitting an array of all the hexes connecting one side of the board to the other. The smart contract will check that these hexes connect to each other in order, span the board, and contain the correct color. If the checks pass, the position will be marked as winning, and no moves will be allowed to be played on it.
### Checking for rewards
If the gas cost of checking for rewards is high, then there should be a read-only function that calculates the rewards for a player for free. There should also be a function that returns a player's move deposits without a check for rewards. This way a player can choose whether to pay the added gas of claiming their rewards or just claim the deposits. After all players in a game have claimed their deposits, any unclaimed rewards go to the developer fund .
