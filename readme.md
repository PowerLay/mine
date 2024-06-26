# An advanced mining program for ComputerCraft Turtles

This program is capable of mining an arbitrary area while removing lava, automatically refueling itself, bringing the mined items into one place, and more (no auto torches though sadly).

## Basic usage

1. Run `pastebin get 7uHd9pPx mine`. Run `mine`.
1. On startup, the program shows a bunch of info, such as fuel level, slots used for various items, etc.
1. By default, three slots are assigned: Chests, Fuel and Cobblestone.
Chests are required since they are used to drop off mined items, but the cobblestone and fuel slots can be left empty.
The turtle will store collected fuel and cobblestone in those slots and use them when necessary.
1. Below that, you will see a list of programs.
You can run `help <program>` to get a description of any specific program.
1. Let's assume you want the turtle to branch mine.
Type `branch 5 20`.
The turtle should start mining a 20-block long tunnel in the direction it is facing.
The tunnel will have 5-block branches going to the left and right.
Note that the order it mines the blocks in might seem a bit strange
1. While mining, the turtle will go through ore veins without going further than 5 blocks from the area it's mining.
1. The turtle will place chests near the place where it has started mining.

**Currently existing programs:**

- `help <program>` -
display info about the chosen program
- `sphere <diameter>` -
Mine out a sphere of diameter `<diameter>`, starting from it's bottom center
- `cube <left> <up> <forward>` -
Mine out a cuboid of a specified size. Use negative values to dig in an opposite direction
- `rcube <leftR> <upR> <forwardR>` -
Mine out a cuboid centered on the turtle. Each dimension is a "radius", so typing `rcube 1 1 1` will yield a 3x3x3 cube
- `branch <branchLen> <shaftLen>` -
Branch-mining. `<branchLen>` is the length of each branch, `<shaftLen>` is the length of the main shaft
- `custom <absolute/file/path.lua>` -
Mine out a custom volume generated by running code from file `<absolute/file/path.lua>`. See the _Mining out any volume you want_ section.

## Configuration

The [mine.lua](https://github.com/Equbuxu/mine/blob/master/mine.lua) file contains a config section at the top.
You may edit this section to change the turtle's behaviour.
Each setting is explained by a comment above it.

## Mining out any volume you want

The `custom <absolute/file/path.lua>` accepts a lua file, and runs a function named `generate` from it.
The function should return a list of vectors, each specifying a position to be mined.
You can see an example in [`cylinder.lua`](https://github.com/Equbuxu/mine/blob/master/cylinder.lua).

Tips for generating good volumes:

- Make sure that the function outputs a single volume (instead of multiple separate ones).
- The turtle always attempts to place chests at the very bottom part of your volume. The turtle tries to navigate to the place above the chest, which means that the very bottom part of your volume must be at least two blocks high, and there should be enough two-high spaces for all chests. The program will crash otherwise.
