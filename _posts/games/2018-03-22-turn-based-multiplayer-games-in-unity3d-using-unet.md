---
layout: post
logo: "🎒"
title:  "Turn-based Multiplayer Games in Unity3D using UNet"
date:   2018-03-22
categories: Games
permalink: /games/turn-based-multiplayer-games-in-unity3d-using-unet
description: Multiplayer Networking | Unity3D | UNet | Turn Based Games
---

![](https://miro.medium.com/max/5383/0*iY1iAPp5hBt6Rc7c.)

> Note: This article uses unity3d multiplayer networking concepts, learn more here “[Unity-Multiplayer Networking](https://unity3d.com/learn/tutorials/topics/multiplayer-networking/introduction-simple-multiplayer-example?playlist=29690)”.

After going through the internet like crazy in search of tutorials for creating turn-based multiplayer games in Unity3D, I have arrived at a decision to do it on my own and help my fellow creators to end this struggle.

This is what you will need:

1. Network Manager
2. Network Player
3. Player Controller

---

# NetworkManager

For playing multiplayer games, you need a server to host the games which will also watch over the connected players to maintain their states as the game progresses. First of all, the server will create a match and broadcast the match ID to all the players in the network. The players then are connected to the game by joining the match using the match ID.

A *Network Manager* game object is responsible for these tasks. All the connected players in the match are stored in a list. `AlterTurns()` method ends the current player’s turn and starts the next player’s turn by changing the active player index `iActivePlayer`. Similarly, it updates the active player score, when a player score update is requested by the client.

<script src="https://gist.github.com/div5yesh/fa4ffcfff6f7720d32b77560e2b41b10.js"></script>

# NetworkPlayer

A *Network Player* game object is spawned by unity when a player joins the match. The player hosting or creating a match acts as a server. While the player joining the match is a client. All the player in the network are kept in sync with the server.

> The synchronization between the clients and the server validates the states of game objects across the network for each player in the match.

The idea is to keep the current turn timer, active player index and scores in sync between the players and use network manager to alternate turns and update scores. The objects on client players are a copy of objects on the server. So, to make any changes in the game state, a client must let the server know about the changes and any changes in the game state at server must be notified to the other clients.

> The way this is done by making “**RPC**” calls and sending network “**commands**”.

<script src="https://gist.github.com/div5yesh/e8cc6e06c83307d1204ca81eacb57854.js"></script>

# PlayerController

A *Player Controller* game object is responsible to send player actions like shooting or jumping to the server. You can use this to spawn and unspawn player/objects on the network using `TurnStart()` and `TurnEnd()` methods.

<script src="https://gist.github.com/div5yesh/cc1fb36a140134dbd34d1b2d5f8330f5.js"></script>

Git Repo **coming soon**!

Originally posted: [medium.com/@div5yesh](https://medium.com/@div5yesh/turn-based-multiplayer-games-in-unity3d-using-unet-abcd8360ddd5)