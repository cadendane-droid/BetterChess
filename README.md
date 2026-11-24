# BetterChess

Chess with new pieces, portals and supply crates. Two players, online
(peer-to-peer) or on one device, from a single static page — host it on
GitHub Pages like the other GameForAll games.

## Rules

**No check, no checkmate: capture the enemy king to win.** You are allowed to
leave your king in danger; the status line warns you when it can be hit.
There is no castling and no en passant.

### Starting position

```
8  R N B Q K W N C      (Black, same layout)
7  P P A P P A P P
2  P P A P P A P P
1  R N B Q K W N C      (White)
   a b c d e f g h
```

### Pieces

| Piece | How it moves |
|---|---|
| King | One square any way. **Royal Dash**: once per game, two squares in a straight line if the square in between is empty. |
| Queen, Rook, Knight | As in chess. |
| Bishop | Diagonal slides, plus a **sidestep** of one square straight onto an empty square, so it can change colour. |
| Pawn | As in chess, but promotes to any piece including Cannon, Archer and Wizard. |
| **Cannon** (new) | Slides like a rook but can't capture that way. Captures by leaping over exactly one piece (either colour) onto the first enemy beyond. |
| **Archer** (new) | Steps one square any way, never captures by moving. **Shoots** any enemy exactly two squares away in a straight line or diagonal, over anything, without moving. |
| **Wizard** (new) | Steps one square any way (can capture), or **swaps** places with a friendly non-king piece up to 3 squares away. |

### The board

- **Portals** — two linked pairs: c4 ↔ f5 and f4 ↔ c5. End a move on a portal
  and you come out of its twin. An enemy standing on the twin is destroyed; a
  friend there blocks the warp.
- **Supply crates** — every 5 moves a crate drops on a random empty square in
  ranks 3–6 (at most 3 at once). Move onto it to pick it up:
  - **Shield** — the next hit breaks the shield instead of the piece; the
    attacker stays where it was.
  - **Haste** — move again immediately.
  - **Frost** — every adjacent enemy piece is frozen for its next turn.
  - **Powder keg** — whatever captures this piece is destroyed too, along with
    everything next to it (kings are immune to the blast; shields absorb it).
    Kegs chain. Archer shots set kegs off from a safe distance.
- A side with no legal move passes. If neither side can move, it's a draw.

Both browsers run the same rules engine from a shared random seed, so only the
moves themselves cross the network.

## How it works

Same networking as the other GameForAll games: pick room 1, 2 or 3 and press
**Play**; the first player hosts via the free PeerJS broker and the second
joins. After the handshake the two browsers talk directly. The host plays White
in the first game and colours alternate on rematches. **Play on this device**
starts a pass-and-play game with no network at all.

Names come from `localStorage` key `gameforall.playerName`, shared with the menu.

## Hosting

1. Push this folder to a GitHub repo named `BetterChess`.
2. Settings → Pages → deploy from the `main` branch, root folder.
3. The game lives at `https://<your-username>.github.io/BetterChess/` and the
   menu links to it as `../BetterChess/`.

If players can't connect across networks, add a TURN relay exactly as described
in the UltimateTTT README (`TURN_CREDENTIALS_URL` near the top of the script).
