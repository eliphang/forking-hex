# Forking Hex 🔱⬢⬡
Find a move that connects two sides of the hex board and win crypto.

## Background
Forking Hex is based on the game Hex. The moves are the same. The innovation of Forking Hex is the addition of *forking*.

## Forking
Anyone (including new players who haven't previously made moves) can make a move on any *open* position. Additional moves can be made in response to any open position, creating forks.

Thus, Forking Hex is loosely a team game, with players able to join a team that seems to be winning or leave a team when the situation seem hopeless. Players can even play on both sides of the same game.

## Winning
There are no draws in Hex. This is also true for Forking Hex. Every game will have at least one loser, although it's possible for a team to have both losers and winners. Winning and losing depends on the quality of the moves a player makes, not the team they belong to. A player who makes a losing move will forfeit the crypto deposit they made for that move to players on the other team who made moves before them. Because Forking Hex is heavy on strategy (think "Go") and light on tactics (think "Chess"), making a losing move is rare, but in every game at least one losing move will be made.

It's possible for teams to win some forks and lose others. There is no losing or winning team. Players are rewarded for being on the opposite team upstream from a player who makes a losing move.

## Rules
### Game creation
Anyone can create a new game, specifying

* the size of the board. John Nash said 14x14 is the optimal board size, but any square size is possible. The length and complexity of the game depends on the size.
* time per move for the first team (in blockchain blocks). This is how long a move stays *open*, meaning how long players can create responses to it, including forks.
* time per move for the second team. This must be less than the time for the first team. Hex is ultra-weakly solved. This means we know that the first mover will always win with perfect play, but we don't what the perfect moves are. To balance this, we give the second mover more time per move.
* cost per move. Each move requires a deposit of crypto. Almost all deposits will be returned. Only a losing move loses its deposit, to be distributed to players on the other team.


