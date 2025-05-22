# childTabletGame
A C++ game simulating a tablet interface using SFML for interactive graphics and gameplay.

This project is a **child-friendly drawing and command interpreter game**, built using **C++** and **SFML**. Inspired by turtle graphics (as seen in the Logo programming language), it helps children learn logical thinking and basic programming concepts by allowing them to draw shapes and patterns using simple text commands on a graphical interface.

## Overview

The application provides a colorful and interactive environment where children can:

* Enter commands such as "forward", "circle", or "color red" to draw on the screen.
* Control the movement and orientation of a virtual "pen" or "cursor".
* Experiment with drawing lines, rotating, changing colors, and repeating patterns.
* Save their command sequences to reuse or share.

Designed for **touchscreen tablets or child-safe desktop use**, the game emphasizes:

* Visual learning
* Creativity
* Fundamental logic building

## Features

### Drawing and Movement Commands

* `fd [n]` / `forward [n]`: Moves the cursor forward by *n* units.
* `bk [n]`: Moves the cursor backward.
* `rt [angle]`: Rotates the cursor to the right by a given angle (supports 30° or 45°).
* `lt [angle]`: Rotates the cursor to the left by a given angle.
* `circle [radius]`: Draws a circle at the cursor's current tip position.

### Pen Control

* `pu`: Lifts the pen to move without drawing.
* `pd`: Lowers the pen to resume drawing.

### Style Settings

* `color [name]`: Changes the drawing color. Supported colors include red, blue, green, yellow, purple, orange, pink, brown, white, and gray.
* `width [1-3]`: Changes the line thickness (1 is thin, 3 is thick).

### Repeat and Loops

* `repeat [n] [commands]`: Repeats a block of commands *n* times for drawing patterns or animations.

### History and Persistence

* Automatically maintains a history of the last 100 commands.
* `save [filename]`: Saves the current command history to a file.
* `load [filename]`: Loads and replays commands from a file.

### Visual Feedback

* All drawing is shown in a real-time canvas with a bounding area (500x500 pixels).
* The command history is visible on-screen, helping children learn from past actions.

## Technical Details

* **Language:** C++
* **Graphics Library:** SFML (Simple and Fast Multimedia Library)
* **UI:** Rendered via SFML's shapes, fonts, and events
* **Math:** Uses trigonometric functions for cursor rotation and positioning

## Getting Started

### Prerequisites

* Install [SFML](https://www.sfml-dev.org/download.php) on your machine.

### Compilation

```bash
g++ -std=c++17 code.cpp -o turtle -lsfml-graphics -lsfml-window -lsfml-system
```

Make sure `arial.ttf` (the font used for text rendering) is placed in the same directory as the compiled binary.

### Execution

Run the executable. A window will open. You can start typing commands directly, and results will appear in real time.

## Possible Extensions

* Add support for undo and redo
* Introduce graphical UI buttons for non-text users
* Add voice feedback or animations
* Implement user profiles or drawing challenges
