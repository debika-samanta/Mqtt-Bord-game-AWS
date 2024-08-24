# MQTT Board Game using AWS IoT

This project is a multiplayer board game implemented using MQTT and AWS IoT Core. The game features a 500x500 grid where players can move, teleport, and activate powers to eliminate opponents. The AWS IoT Core will act as the game server.

## Game Rules

1. The game consists of a 500x500 grid (numbered 0 to 499).
2. N players will join the game.
3. Each player can occupy any cell at a time. (No two players occupy the same cell at a given time)
4. The player can teleport to any location on the grid.
5. The player has a power, which when activated, will kill any player in adjacent/neighbouring cells.
6. If both players have their power activated, nothing happens.
7. The game is played until only 1 player is left.

## Input

1. You will be provided with N input files - one for each player.
2. Files will be named as `<player-x.txt>`, e.g., `player-1.txt`.
3. The first line contains the number of players that will play the game. (Same in each file)
4. After that, each line contains 3 numbers `<x_coordinate, y_coordinate, power_status>` of the player (0 - power not activated, 1 - power activated). E.g., `<102, 314, 0>`, `<220, 76, 1>`.
5. You can assume that there will always be sufficient input lines for the game to finish.

### Sample Input
With only 2 players - Player 1 wins the following game:

**player-1.txt**
2 2 1
2 0 0
3 7 0 
10 5 1 
4 7 0 
6 8 1

**player-2.txt**
2 5 0
3 1 1
7 2 0 
11 5 1 
10 3 1 
6 7 0

## Output and Player Flow

1. After connecting to the server, the player will wait until all other players have joined.
2. The game starts once all players have joined.
3. Each player updates its location and power status to the server.
4. Each player subscribes to the location and power status (or any other necessary data) of all other players.
5. Player checks if any other player is adjacent to it with activated power and its own power is not activated; If yes, the player dies and disconnects from the server after updating necessary information.
6. All other players should know that a player died, who killed it, and reduce the number of alive players. E.g., `player-7 was killed by player-3`.
7. Once N-1 players have died, the winner should know it’s the only one left and print the same.

## Prerequisites

To run this project, you need to set up the following prerequisites:

### 1. Set Up AWS IoT Core

1. Sign in to your [AWS Management Console](https://aws.amazon.com/console/).
2. Navigate to **AWS IoT Core** and create a new thing.
3. Create and download the required certificates and keys for your IoT devices.
4. Set up an MQTT topic for communication and configure your AWS IoT rules as needed.

### 2. Install Python3 and Pip3

```bash
sudo apt update
sudo apt install python3 python3-pip
pip3 install paho-mqtt

git clone https://github.com/debika-samanta/mqtt-board-game-hivemq.git
cd mqtt-board-game-hivemq

