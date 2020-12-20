# Dungeon generator

This is a procedural dungeon generator written in javascript.  

[Live demo](http://domasx2.github.io/dungeon-generator/)

## Features

1. Pre-defined, tagged rooms
2. Highly configurable
3. Seeded rng
5. Feedback about exits, perimeter, etc
4. (Optional) corridors
5. (Optional) circular paths


## Output examples

![Sample 1](http://domasx2.github.io/dungeon-generator/samples/sample1.png)
![Sample 2](http://domasx2.github.io/dungeon-generator/samples/sample2.png)
![Sample 3](http://domasx2.github.io/dungeon-generator/samples/sample3.png)
![Sample 4](http://domasx2.github.io/dungeon-generator/samples/sample4.png)

## Usage

@TODO

```javascript
import Dungeon from 'dungeon-generator';

let dungeon = new Dungeon({
    "size": [64, 64],
    "rooms": {
        "initial": {
            "min_size": [4, 4],
            "max_size": [4, 4],
            "max_exits": 1
        },
        "any": {
            "min_size": [4, 4],
            "max_size": [4, 4],
            "max_exits": 4
        }
    },
    "max_corridor_length": 1,
    "min_corridor_length": 1,
    "corridor_density": 0,
    "symmetric_rooms": true,
    "interconnects": 0,
    "max_interconnect_length": 0,
    "room_count": 8
});

dungeon.generate();
dungeon.print(); //outputs wall map to console.log

dungeon.size; // [width, heihgt]
dungeon.walls.get([x, y]); //return true if position is wall, false if empty

for(let piece of dungeon.children) {
    piece.position; //[x, y] position of top left corner of the piece within dungeon
    piece.tag; // 'any', 'initial' or any other key of 'rooms' options property
    piece.size; //[width, height]
    piece.walls.get([x, y]); //x, y- local position of piece, returns true if wall, false if empty
    for (let exit of piece.exits) {
        let {x, y, dest_piece} = exit; // local position of exit and piece it exits to
        piece.global_pos([x, y]); // [x, y] global pos of the exit
    }

    piece.local_pos(dungeon.start_pos); //get local position within the piece of dungeon's global position
}

dungeon.initial_room; //piece tagged as 'initial'
dungeon.start_pos; //[x, y] center of 'initial' piece 
```
