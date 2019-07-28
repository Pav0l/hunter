# hunter

treasure hunt algorithm

# persist these in DB

- map of the world

```python
map = {
    0: {n: 1, w: 2, e: 3, s: 4},
    1: {n: 5, w: 7, e: 9, s: 0}
}
```

- global que to keep track of unvisited rooms

```python
global_que = [(1, 's'), (1, 'n')] # tuple of ID and direction to explore
```

- list/set of visited rooms

```python
visited = [1, 2, 4, 6]  # room IDs
```

- every room dict

```python
{
  "room_id": 0,
  "title": "A Dark Room",
  "description": "You cannot see anything.",
  "coordinates": "(60,60)",
  "players": [],
  "items": [],
  "exits": ["n", "s", "e", "w"],
  "cooldown": 30.0,
  "errors": [],
  "messages": ["You have walked south.", "Wise Explorer: -50% CD"]
}
```

- list of shops so it's available for every player

# create classes and methods

## world

- add different world powers, etc in

## player (server)

- keep track of cooldowns/stats/powers/etc

# explore map algo

The goal is to utilize all 4 players in exploring the map and updating it instead of just one player doing it.

To explore the map, utilize DFT with BFS when you hit a dead end.

First player initialzies the game server from starting room, adding all exit directions to global que and his local stack.

P1 starts DFT poping a room from his stack, making a request to game server, adding response room to visited, saving response room to DB and adding all its exits to global que and local P1 stack.

P2 starts the DFT by poping a room from GLOBAL que and then continues with request, save response to DB/visited, add exits to global que and P2 stack.

P3, P4 ditto

When player hits dead end, he does BFS to next item in stack and continues DFT from there saving rooms to map.

Every request to the game serve must be checked against the cooldown timer.

Once all rooms from global que and local stacks are explored (present in visited list), the map should be complete.
This should shorten the time for the team to explore the whole map.
