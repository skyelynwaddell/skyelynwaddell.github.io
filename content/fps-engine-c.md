+++
title = "3D Game Development in C"
date = 2025-07-12T17:17:06-06:00
draft = false
description = "Journey through the creation of 3D game development, tackling a first person shooter engine built entirely in C. Covers topics such as rendering, map & geometry projection, textures, collision detection, lighting & shaders, occlusion culling and more."
image = "/images/c.png"
categories = ["c", "fps", "3d", "raylib", "gamedev"]
authors = ["Skye Waddell"]
avatar = "/images/c.png"
+++
# 3D Game Development in C 🎮

*THIS PAGE IS A WORK IN PROGRESS*

{{< figure src="/images/image.png" width="100%" alt="FPS engine preview" >}}

## Table of Contents
- [Introduction](#introduction)
- [Getting Started](#getting-started)
- [Main Game Loop](#main-game-loop)
- [Create an FGD for our mapping software](#create-an-fgd-for-our-mapping-software)
- [What is a brush?](#what-is-a-brush)
- [Setting up Map & Geometry Types](#setting-up-map--geometry-types)
- [Parse brushes from a .map file](#parse-brushes-from-a-map-file)
- [Generate Map Geometry](#generate-map-geometry)
- Create a Texture Manager & Cache
- Project UV Textures onto map geometry
- 3D Player Object
- First Person Camera
- 3D collisions
- Parse entities from .map
- Lighting & Shaders
- Occlusion Culling & Optimizations

## Introduction
What this book does `NOT` cover:
- How to use C or a compiler (watch a youtube video)
- Tutorial for raylib graphics library (its pretty easy to setup)
- How to make maps with Trenchbroom
- How to build a graphics library from scratch (we arent reinventing the wheel here)

```c
NOTE
// If I say create .c file, it means ALSO create a matching .h file
// If I say create a .h file only, it means it DOESNT need a matching .c file
```

Since this book is written in C (which many languages have similar syntax to), it should be pretty straight forward to port this code to any programming langauge --- Especially since Raylib has bindings for many languages as well.

I am going to tell a story of my journey of developing, and learning 3D games.... It will tie in and all make sense to what I am going to explain and cover in this manual/book.

I've always loved games since I was a kid, and it has been my main passion and driving force for learning how to code initially. Games have always brought me joy and I have always been fascinated and completely astonished by the fact people got to create these things for a job.
Video games have always been a safe get away and escape from reality, but for me the development of these was always so interesting. An unattainable goal of complex wizardy and math I once thought they were --

One such achievement I had always set for myself was one day, I wanted to create my own 3d game without the use of an engine.
After many years of practicing 2D and 3D game development across many engines, and frameworks I felt around a few months ago I might actually have a deep enough understanding of how the 3D game engines worked. A lot of this I can thank to Quake.

Quake was a game released in 1996 which was a technical masterpiece at the time, with features and graphics that was unseen or heard of at that time.
During my adventure of 3D game development I was using Godot. It is a fantastic engine, and if you are looking for a more high-level approach to building games I highly recommend it.
However, during the development I was working on a FPS game since I have always played a lot of these and felt like I would have the most knowledge about this kind of game.
Building maps out of the Godot nodes and geometry soon grew to be tiring and I felt there had to be a better way... 
This is when I found FuncGodot and Trenchbroom.

Funcgodot is a map parsing tool that allows for you to make 3d maps in trenchbroom and then builds them in Godot for you, allowing for a much more easy and fun approach to developing levels.
Trenchbroom is completely free and opensource and was originally developed for Quake maps, but since Quake is open source you can technically use the map files for any game or engine that can parse them.

After using these tools for a while, and the learning the ins and outs of how Quake and its maps were built I really started to understand 3D games on a more fundamental level, and finally felt like I was ready to try and tackle creating a 3D game.

Picking the language...
Since Doom and Quake, some of my favorite FPS games ever were written in C, I figured that C would be the perfect language since it has created some amazing FPS games before that are very well optimized even by todays standard.

The next thing of choice was to be how was I going to render the game, and I had created a few test projects.
I knew that for rendering I wanted to go with OpenGL since it is my favorite, and will run on a potato even. This is important because I want my games to be able to be played on anything.

I initially had a C project setup with SDL 2 and OpenGL with a completely bare project...
At this time I started trying to draw and render some simple lines and triangles, I think I spent way too much time during this step.
Having a lot of experience in web development, and javascript I knew that there had to be a solution or giant library/package with all the 3D functions and abstractions to call SDL and OpenGL from so I didn't have to write an entire graphics library as well.

This is when I found Raylib ~ this is basically just a c header file that contains almost every type, function, and any other useful things you may ever use when it comes to rendering graphics with SDL, GLFW, and OpenGL which was perfect and exactly what I was looking for.

Here is where we start off and we will start building our 3D First Person Game with C, and raylib (which uses SDL or GLFW with OpenGL).

## Getting started
Check out my 3D game/engine built in C on github: [skyesrc-engine](https://github.com/skyelynwaddell/skyesrc)

For this project we will be using C and raylib.
Raylib is a C graphics library that contains useful high-level abstractions and functions to interact with SDL or GLFW alongside OpenGL to make our lives easier. No, it doesnt work with Vulkan.

Get all this stuff...
- [C & GCC Compiler](https://gcc.gnu.org/install/download.html)
- [Raylib](https://www.raylib.com/)
- [Raymath](https://github.com/raysan5/raylib/blob/master/src/raymath.h)
- [RayGUI](https://github.com/raysan5/raygui)
- [rcamera](https://github.com/raysan5/raylib/blob/master/src/rcamera.h)
- [rlights](https://github.com/raysan5/raylib/blob/master/examples/shaders/rlights.h)
- [Trenchbroom](https://trenchbroom.github.io/)

For this engine we will be using trenchbroom .map files for our levels and editor as it gives us a nice baseline and 3D editor to work in for our game.
You will want to learn trenchbroom, as this is how you will build your levels.

**The map parser we will build will only be parsing Valve 220 map format, since it is has better UV texture alignment in comparison to the the Standard quake map format.**

At this point you will want to setup a C project.
You will want to make sure that all the listed libraries are included and linked in your project and working, see a tutorial or the raylib discord for help setting up a project. 

raylib discord: https://discord.com/invite/raylib

## Main Game Loop
I always create some header files initially.
These 2 files can contain any #define variables, or global variables/functions. These will be very useful.
  - global.h & global.c
  - utils.h & utils.c
  - defs.h

I define BOOLEAN in my defs incase you see true/false in the code.
#### defs.h
```c
// defs.h
#define false 0
#define true 1
```

Next I'm going to create the "gameloop" header and definition files.
  - init.c
  - update.c
  - draw.c
  - draw_gui.c
  - draw_viewmodel.c
  - input.c
  - cleanup.c

Each should have a simple function defined for now, matching their filename.

The next step is to create the gameloop in `main.c`.
Here is a pretty bare-bones setup including the above files and functions I had mentioned to create.
#### main.c
```c
// main.c
#include <stdio.h>
#include "raylib.h"
#include "raygui.h"
#include "raymath.h"

#include "defs.h"
#include "global.h"

#include "init.h"
#include "input.h"
#include "update.h"
#include "draw.h"
#include "draw_viewmodel.h"
#include "draw_gui.h"
#include "cleanup.h"

// Program Entry Point
// -----------------------------
int main()
{
  // Initialization
  // -----------------------------
  init();

  // Main Game Loop
  // -----------------------------
  while(!WindowShouldClose())
  {
    SetConfigFlags(FLAG_MSAA_4X_HINT); // Multi Sampling Anti Aliasing 4X
    SetExitKey(0); // Disable exit key (ESC)

    input();
    update();

    // Draw
    // -----------------------------
    BeginDrawing();
      ClearBackground(WHITE);
      
      draw();
      draw_viewmodel();
      draw_gui();

    EndDrawing();
  } // draw -------------------------

  // De-Initialization
  // -----------------------------
  clean_up();
  CloseWindow();
  return 0;
}
```

## Create an FGD for our mapping software
What the hell is an FGD?
Its a Forge Game Data file with all of our game objects, and such... Basically our map and game are completely seperate, therefore we can define any objects, wall types (like water, or glass), pickups, npc's etc in here.
You can design your maps in Trenchbroom, then whatever is defined in the FGD will be allowed to be placed in the room which will be exported in the .map file.
We can then parse which objects, pickups, etc have been placed in a room and then actually spawn them in our game.

You can see how a FGD file will be useful.
For example, the FGD will define that I can have pickup_apple, and pickup_orange items, and then they will be added to the Entity Browser for any Map using that FGD.

This is why Trenchbroom works for us, Since Quake was so moddable -- Every Map could technically be an entirely different game based on what objects and other entities or brushes were defined in the FGD. Allowing for us to utilize this as a mapping tool for any game.

For starters you will want to create a custom game for Trenchbroom.
Its different for all platforms, Ill quickly go over the windows version.

You goto where Trenchbroom installed, ie. Documents.
Then you will want to find the `/games` folder and create a new folder with your game/engine name, and add your own custom GameConfig.cfg file in here.

Here is a template you can use for the GameConfig.cfg file, modify it to match your game/engine details, change the name.
#### GameConfig.cfg
```c
// GameConfig.cfg
// place in -> /Trenchbroom/games/my_cool_game/
{
	"version": 8,
	"name": "GAME_ENGINE_NAME",
	"icon": "icon.png",
	"fileformats": [
        { "format": "Valve" },
        { "format": "Standard" }
    ],
    "filesystem": {
        "searchpath": ".",
        "packageformat": { "extension": ".pak", "format": "idpak" }
    },
	"textures": {
		"root": "textures",
		"extensions": [".bmp", ".exr", ".hdr", ".jpeg", ".jpg", ".png", ".tga", ".webp"],
		"excludes": [ "*_albedo", "*_ao", "*_emission", "*_height", "*_metallic", "*_normal", "*_orm", "*_roughness", "*_sss" ]
	},
	"entities": {
        "definitions": [ "gamedata.fgd" ],
        "defaultcolor": "0.6 0.6 0.6 1.0"
    },
    "tags": {
        "brush": [
            {
                "name": "Detail",
                "attribs": [],
                "match": "classname",
                "pattern": "func_detail*"
            },
            {
                "name": "Trigger",
                "attribs": [ "transparent" ],
                "match": "classname",
                "pattern": "trigger*",
                "texture": "trigger" // set this texture when tag is enabled
            },
            {
                "name": "Func",
                "attribs": [],
                "match": "classname",
                "pattern": "func*"
            }
        ],
        "brushface": [
            {
                "name": "Clip",
                "attribs": [ "transparent" ],
                "match": "texture",
                "pattern": "clip"
            },
            {
                "name": "Skip",
                "match": "texture",
                "pattern": "skip"
            },
            {
                "name": "Hint",
                "attribs": [ "transparent" ],
                "match": "texture",
                "pattern": "hint*"
            },
            {
                "name": "Liquid",
                "attribs": [ "transparent" ],
                "match": "texture",
                "pattern": "\**"
            }
        ]
    },
    "softMapBounds":"-4096 -4096 -4096 4096 4096 4096",
    "compilationTools": [
        { "name": "qbsp"},
        { "name": "vis"},
        { "name": "light"}
    ]
}
```
&& Here is a barebones .fgd file you can use to get started:
You can keep this in your Game Engine directory, and doesnt have to be stored in the trenchbroom games folder.
#### gamedata.fgd
```c
// gamedata.fgd

// ############################## //
// MAP DATA FGD (FORGE GAME DATA) //
// ############################## //

//
// worldspawn
//
@SolidClass = worldspawn : "World entity"
[
	message(string) : "Text on entering the world"
	worldtype(choices) : "Ambience" : 0 =
	[
		0 : "Medieval"
		1 : "Metal (runic)"
		2 : "Base"
	]
	sounds(integer) : "CD track to play" : 0
	light(integer) : "Ambient light"
	_sunlight(integer) : "Sunlight"
	_sun_mangle(string) : "Sun mangle (Yaw pitch roll)"
]

@baseclass = brush : "Any kind of brush in the world"
[
	sector(integer) : "Sector Group Tag [int]"
]

@SolidClass base(brush) = brush_default : "All brushes must inherit from this if to be culled" []

//
// base marker definitions
//
@baseclass = Angle [ angle(integer) : "Direction" ]

@baseclass = Appearflags [
	spawnflags(Flags) =
	[
		256 : "Not on Easy" : 0
		512 : "Not on Normal" : 0
		1024 : "Not on Hard" : 0
		2048 : "Not in Deathmatch" : 0
	]
]

@baseclass = Targetname [ targetname(target_source) : "Name" ]
@baseclass = Target [
	target(target_destination) : "Target"
	killtarget(target_destination) : "Killtarget"
]

//
// player starts, deathmatch, coop, teleport
//
@baseclass base(Appearflags) size(-16 -16 -24, 16 16 32)
	color(0 255 0) model({ "path": "models/9mm.glb" }) = PlayerClass []

@PointClass base(PlayerClass) = info_player_start : "Player 1 start" []
@PointClass base(PlayerClass) = info_player_coop : "Player cooperative start" []
@PointClass base(PlayerClass) = info_player_start2 : "Player episode return point" []
@PointClass base(PlayerClass) = info_player_deathmatch : "Deathmatch start" []
@PointClass base(PlayerClass) = testplayerstart : "Testing player start" []
@PointClass size(-32 -32 0, 32 32 64) base(PlayerClass, Targetname) = info_teleport_destination : "Teleporter destination" []
@PointClass color(200 150 150) = info_null : "info_null (spotlight target)"
[
	targetname(target_source) : "Name"
]

@PointClass base(Appearflags) = light : "Light" 
[
	color(color255) : "Color" : "255 255 255"
	alpha(float) : "Alpha" : 255.0 : "The transparency of the light color"
	brightness(float) : "Brightness" : 0.6 : "How bright the light is." 
	radius(float) : "Radius" : 40.0 : "How big the light is."
	
]
```

Here you can see where you can load your custom FGD into Trenchbroom, again this is not a trenchbroom tutorial but you can see where it would be loaded.
{{< figure src="/images/fgd.png" width="50%" alt="FPS engine preview" >}}

From here you will have to goto Trenchbroom Settings, and Game Configurations and add the Project directory of your game/engine to the correct game in the list (it will be the newly added one recognized by the new GameConfig.cfg file!!!)

Make sure your textures folder trenchbroom is referencing/using is located in your game/engine project directory...

Mess around until you can build a simple room with some textures on the brushes/walls, and export it as a .map file.
You will need this so we can have a room to walk around in!

Contact the trenchbroom/quake mapping discord if you need any help with making maps.

Trenchbroom Tutorials: 
https://www.youtube.com/watch?v=gONePWocbqA&list=PLgDKRPte5Y0AZ_K_PZbWbgBAEt5xf74aE

## What is a Brush?
Once you have built a simple map and exported it as a .map file its time to actually read that data in our C program.

First we need to understand what a brush is, how we make geometry from them, and we need to define some types/classes for what the map & geometry will need.

What exactly is a brush you may ask?
As you were building your geometry in Trenchbroom you may have noticed it was similar to painting as you would click and drag the polygonal geometry out and shape it ~ thus they named them a brush.

A simple brush in a .map file looks like this:
```c
// brush 0
{
( -306 -128 -48 ) ( -306 -127 -48 ) ( -306 -128 -47 ) checkers [ 0 -1 0 0 ] [ 0 0 -1 -32 ] 0 1 1
( 48 -128 -48 ) ( 48 -128 -47 ) ( 49 -128 -48 ) checkers [ 1 0 0 -48 ] [ 0 0 -1 -32 ] 0 1 1
( 48 -128 -32 ) ( 49 -128 -32 ) ( 48 -127 -32 ) checkers [ -1 0 0 48 ] [ 0 -1 0 0 ] 0 1 1
( 176 0 32 ) ( 176 1 32 ) ( 177 0 32 ) checkers [ 1 0 0 -48 ] [ 0 -1 0 0 ] 0 1 1
( 176 704 -16 ) ( 177 704 -16 ) ( 176 704 -15 ) checkers [ -1 0 0 48 ] [ 0 0 -1 -32 ] 0 1 1
( 368 0 -16 ) ( 368 0 -15 ) ( 368 1 -16 ) checkers [ 0 1 0 0 ] [ 0 0 -1 -32 ] 0 1 1
}
```
Each line here represents a face or side of the brush, aka a BrushFace. Since this brush is 6 lines (meaning it has 6 faces), we can safely assume that it is cube shaped. 

So a Brush, is just a collection of BrushFace's.

You may be wondering what each of these values does in a BrushFace, I'll explain.
Each `brushface` is an Infinite Plane that has 2 directions and a texture.

Imagine we draw a cube with infinite planes, it would looks something like this.
I couldn't draw it exactly as it would just look like a giant box still, so the front and back faces dont have their infinite plane being drawn... just so you can visualize a cube created of planes, where each plane has 2 infinite directions.

{{< figure src="/images/infinitecube.png" width="100%" alt="FPS engine preview" >}}

The infinite planes, turn ORANGE once they intersect here in this image for visual purposes, the idea is to remove any intersecting orange parts of the infinite planes, and we are left with a Convex Polygon, in this case a simple cube shape.
It sounds easier than it is.

Let's look at one line (BrushFace) of the Brush and break it down

```c
( -306 -128 -48 ) ( -306 -127 -48 ) ( -306 -128 -47 ) checkers [ 0 -1 0 0 ] [ 0 0 -1 -32 ] 0 1 1

// lets put each one of these on a new line
pos1: ( -306 -128 -48 )   // [ x y z ] Origin Point of the plane --- The anchor point / position of the plane
pos2: ( -306 -127 -48 )   // [ x y z ] with pos_1 defines the first infinite direction of the plane
pos3: ( -306 -128 -47 )   // [ x y z ] with pos_1 defines the second infinite direction of the plane
texture name: checkers
U Coords: [ 0 -1 0 0 ]    // [ Ux Uy Uz Uoffset ]
V Coords: [ 0 0 -1 -32 ]  // [ Vx Vy Vz Voffset ]
UV Rotation: 0
UV XScale: 1
UV Yscale: 1
```

- pos1 represents the Origin or Position of the Plane in 3d space.
- pos2 is used with pos1 to calculate the first direction of the infinite plane.
- pos3 is used with pos1 to calculate the second direction of the infinite plane.
- The Fourth value, here it is `checkers`, represents the name of the texture used on that BrushFace, since each face of a brush can have a different texture. The C program would then look for something like: `/textures/checkers.png`
- The fifth and sixth values that look like arrays, are just the UV texture coords. 
- The last three values are: UV Rotation, XScale, and YScale of the Texture.

## Setting up Map & Geometry Types
Let's define `plane.h` and `brushface.h`

We will eventually need to convert each BrushFace into a Plane for calculations so we can create the class/type.
#### plane.h
```c
#ifndef PLANE_H
#define PLANE_H

#include "raylib.h"
#include "utils.h"

typedef struct {
    Vector3 normal; // plane normal (a,b,c)
    float distance; // plane distance from origin
} Plane;


#endif // PLANE_H
```

Here is the brushface class, it will have some functions we will use later and the type definition for what a BrushFace contains. As you can see it holds every value on one of those brushface lines we previously went over.
#### brushface.h
```c
// brushface.h
#ifndef BRUSHFACE_H
#define BRUSHFACE_H

#include <stdio.h>
#include "raylib.h"
#include "raymath.h"
#include "string.h"
#include "plane.h"

typedef struct {

    // Defines the position, size, and directions of the infinite plane
    Vector3 pos_1;    // [ x y z ] Origin Point of the plane --- The anchor point / position of the plane
    Vector3 pos_2;    // [ x y z ] with pos_1 defines the first infinite direction of the plane
    Vector3 pos_3;    // [ x y z ] with pos_1 defines the second infinite direction of the plane

    // with all the infinite planes in a brush we can clip all the geometry wherever 
    // any of the infinite planes intersect with eachother to form the convex polygon.
    
    // texture data for a brush face
    char texture[64]; // texture string name (not including filetype)

    Vector4 uv_s; // [ Ux Uy Uz Uoffset ]
    Vector4 uv_t; // [ Vx Vy Vz Voffset ]

    int uv_rotation; // texture rotation degrees
    int u_scale;     // horizontal texture scale
    int v_scale;     // vertical texture scale

} BrushFace;

void brushface_print(BrushFace b, int face_index);
Plane brushface_to_plane(BrushFace face);

#endif // BRUSHFACE_H
```

From here I recommend creating a new folder to store all the map/geometry c files. These ones ill tell you how to fill them out as we go.
### New C Files to be made 
- map.c
- brushtopolygon.c

### New H files to be made (dont need a c file duh)
- brush.h
- polygon.h
- triangle.h
- geometry.h

We are going to start off in map.c, we need to first load the .map file, so make sure this is accessible in the project folder, have a /maps folder all your maps are in.

In map.h I define a Map type.
This map type will contain all the different values and properties a map could have, as well as all the brushes and entities a map has.

For now a Map will contain a Map Version, an array of Geometry (we will define this after), and the functions that will be used be map.c
We will add more to this later.
Define all functions in this map.h in your map.c as well, we will fill them out and need them later.
#### map.h
```c
// map.h
#ifndef MAP_H
#define MAP_H

#include <stdio.h>
#include "brushface.h"
#include "brush.h"
#include "geometry.h"

// struct to hold the data stored in .map file
typedef struct {
    int mapversion;

    Brush brushes[MAX_BRUSHES];
    int brush_count;

    Geometry models[MAX_BRUSHES];
    int model_count;
} Map; 

extern Map map;

int map_parse(const char* filename);
void map_create_models();
void map_clear_models();
void map_draw();
void map_draw_models();

#endif // MAP_H
```

We can add these 2 new defintions to our `defs.h` files for map
#### defs.h
```c
#define MAX_LINE 1024
#define MAX_BRUSHES 10000
```


Let's define the Geometry file and all the other header files that will need to be included. These header files mentioned above are all mostly 2d and 3d shape defintions we can use in calculations.

First lets make Geometry.h
This type defines the map geometry model, and its collision box.
Each brush shape we calculate will be turned into Raylib model.
Later in the book we will implement a more advanced collision box to the map geometry for collisions.
#### geometry.h
```c
// geometry.h
#ifndef GEOMETRY_H
#define GEOMETRY_H

#include "raylib.h"

typedef struct {
    Model model;
    BoundingBox bounds;
} Geometry;

#endif // GEOMETRY_H
```

#### triangle.h
Next we can create the triangle header file.
This is a simple type with a Vector3 we can use
for triangle calculations later.
```c
// triangle.h
#ifndef TRIANGLE_H
#define TRIANGLE_H

#include "raylib.h"

typedef struct {
    Vector3 a,b,c;
} Triangle;

#endif // TRIANGLE_H
```

Next let's create the brush and polygon files, and some defines.

#### defs.h
```c
// defs.h
#define MAX_VERTICES_PER_FACE 128
#define BRUSH_FACE_COUNT 64 // a brush can have up to 64 faces - must be convex

```

Polygon class will basically be here to store all the vertices a brush face could have, we will need these to be able to calculate, and resort the vertices in a proper order.
#### polygon.h
```c
// polygon.h
#ifndef POLYGON_H
#define POLYGON_H

#include "raylib.h"

typedef struct {
    Vector3 vertices[MAX_VERTICES_PER_FACE];
    int vertex_count;
} Polygon;

#endif // POLYGON_H
```

And next the brush class will contain the count of brushfaces, the array of brushfaces, and the brushfaces vertices / polygons.
#### brush.h
```c
// brush.h
#ifndef BRUSH_H
#define BRUSH_H

#include "defs.h"
#include "brushface.h"
#include "polygon.h"

typedef struct {
    int brush_face_count;
    BrushFace brush_faces[BRUSH_FACE_COUNT];
    Polygon polys[BRUSH_FACE_COUNT];
} Brush;


#endif // BRUSH_H
```

One more class we will need for our map parser will be the Entity class.
Since Brushes, can be entities, we will need to define this as well.
The entity class will have ANY property EVER that a entity COULD have, then depending on the classname of the entity, we will create the correct Object of the right type, and set its properties accordingly.

Here is a simple Entity class defined with some common properties, every Entity will have a Classname, and Origin property!
Then you can define the other properties an entity MAY have.

#### entity.h
```c
// entity.h
#ifndef ENTITY_H
#define ENTITY_H
#include "raylib.h"
#include "raymath.h"

typedef struct {
    char classname[64];
    Vector3 origin;

    // light properties
    Color color;
    float brightness;
    float radius;

} Entity;

#endif // ENTITY_H
```

## Parse brushes from a .map file
So now we have some of our types/classes and an understanding of brushes.
Now we need to code a parser that can read .map files, and extract each brush into an object/struct we can use.

In your map.c file you will want to create a Map map object, and create a `parse_map` function.
This function will need a few other functions to work, we will cover those after.
This will parse the map file, and figures out if it is parsing a Brush, Entity, or Property.

If it is in a brush it will store all the brushfaces in the Current Brush,
then once all of them have been found, we will need to resort the vertices of the brush so that it looks how we expect
we will convert the brushes into polygons first, then we have to convert each brush face into a plane, then we can resort the vertices finally.
Once all of this has been done we will have a Brush object/struct that will contain all the neccesary properties/values to be able to convert them into game models with raylib.

If it is an entity we will add all the properties to the Current Entity, then depending on the classname of the Entity, we can do specific things. For example if it were "info_player_start" - we know thats the player object and we can set the properties of the spawn location for the player etc.

Add to your utils c file a new helper function for map parser
#### utils.c
```c
// utils.c
/*
string_equals
string[char* string] - The first string to be compared
string[char* string_to_compare_to] - the second string that is compared to the first string
-- compares two strings to see if they match
*/
int string_equals(char* string, char* string_to_compare_to)
{
    if (strcmp(string, string_to_compare_to) == 0) return 1;
    return 0;
}
```
#### map.c
```c
// map.c

Map map;

/*
parse_map
filename[const char*] -- the filename of the map to be loaded ie. "myamazingmap.map"
-- Stores the data about the currently loaded map.
*/
int map_parse(const char* filename)
{
    map.model_count = 0;

    printf("\n");
    printf("### LOADING MAP FILE ### \n");
    char fullpath[256];

    // add maps/ filepath to the filename
    snprintf(fullpath, sizeof(fullpath), "maps/%s", filename);

    FILE* file = fopen(fullpath, "r");
    if (!file)
    {
        perror("Failed to open .map file! \n");
        printf("Tried searching in: %s \n", fullpath);
        return false;
    }

    printf("    Successfully opened map: %s \n \n", fullpath);

    printf("-----------------------------\n");
    printf("### MAP PROPERTIES ### \n");

    char line[MAX_LINE];
    int in_entity = false;
    int in_brush = false;
    int current_entity_has_brush = false;

    Brush current_brush = {0};
    int current_brushface_index = 0;

    Entity current_entity = {0};
    int current_entity_index = 0;

    // Loop through all text in the .map file
    while (fgets(line, sizeof(line), file))
    {
        char* trimmed = line;

        // trim leading whitespaces
        while(*trimmed == ' ' || *trimmed == '\t') trimmed++;

        //skip comments and empty lines
        if (trimmed[0] == '/' && trimmed[1] == '/') continue;
        if (trimmed[0] == '\n' || trimmed[0] == '\0') continue;

        /*
        Object Start {
        ----------------------------------
        */
        if (string_equals(trimmed, "{\n"))
        {
            if (in_entity && !in_brush)
            {
                // Brush Start
                in_brush = true;
                current_brushface_index = 0; // restart brush 
                memset(&current_brush, 0, sizeof(Brush)); //clear brush struct
            }
            else if (!in_entity)
            {
                // Entity Start
                in_entity = true;
                current_entity_index = 0; // restart entity
                memset(&current_entity, 0, sizeof(Entity));
            }
            continue;
        }
        /*
        ----------------------------------
        */


        /*
        Object End }
        ----------------------------------
        */
        if (string_equals(trimmed, "}\n"))
        {
            if (in_brush)
            {
                if (map.brush_count < MAX_BRUSHES) 
                    map.brushes[map.brush_count++] = current_brush;
                in_brush = false;
            }
            
            else if (in_entity)
            {
                // TODO : We will come back here
                in_entity = false;
            }
            continue;
        }
        /*
        ----------------------------------
        */


        /*
        Parse Entity
        ----------------------------------
        */
        if (in_entity && !in_brush)
        {
            char key[128], value[128];

            if (sscanf(trimmed, "\"%127[^\"]\" \"%127[^\"]\"", key, value) == 2) 
            {
                if (strstr(key, "classname") == 0)
                    printf("  Property: %s = %s\n", key, value);
                else
                {
                    printf("-----------------------------\n\n");
                    printf("-----------------------------\n");
                    printf("### Entity: %s = %s ###\n", key, value);
                }
                    

                /*
                Map Version
                ----------------------------------
                */
                if (string_equals(key, "mapversion"))
                {
                    map.mapversion = atoi(value);
                    if (map.mapversion != 220)
                    {
                        printf("Only support for valve 220 .map files currently...");
                        CloseWindow();
                    }
                }
                /*
                ----------------------------------
                */


                /*
                Set Current Entity Properties
                ----------------------------------
                */
                    // ### mandatory properties ###

                    // classname
                    if (string_equals(key, "classname"))
                        strcpy(current_entity.classname, value);

                    // origin
                    if (string_equals(key, "origin"))
                        sscanf(value, "%f %f %f", &current_entity.origin.x, &current_entity.origin.z, &current_entity.origin.y);

                /*
                ----------------------------------
                */
            }
        }
        /*
        ----------------------------------
        */


        /*
        Parse Brush Face
        ----------------------------------
        */
        if (in_brush)
        {
            BrushFace brushface = {0};
            char texture_name[64];

            int matched = sscanf(trimmed,
                "( %f %f %f ) ( %f %f %f ) ( %f %f %f ) %63s [ %f %f %f %f ] [ %f %f %f %f ] %i %i %i",
                &brushface.pos_1.x, &brushface.pos_1.y, &brushface.pos_1.z,
                &brushface.pos_2.x, &brushface.pos_2.y, &brushface.pos_2.z,
                &brushface.pos_3.x, &brushface.pos_3.y, &brushface.pos_3.z,
                texture_name,
                &brushface.uv_s.x, &brushface.uv_s.y, &brushface.uv_s.z, &brushface.uv_s.w,
                &brushface.uv_t.x, &brushface.uv_t.y, &brushface.uv_t.z, &brushface.uv_t.w,
                &brushface.uv_rotation, &brushface.u_scale, &brushface.v_scale
            );

            int SUCCESS = 21;
            if (matched == SUCCESS)
            {
                // success
                // get texture name
                strncpy(brushface.texture, texture_name, sizeof(brushface.texture));
                brushface.texture[sizeof(brushface.texture) - 1] = '\0';

                if (current_brushface_index < BRUSH_FACE_COUNT)
                {
                    current_brush.brush_faces[current_brushface_index++] = brushface;
                    current_brush.brush_face_count = current_brushface_index;
                }
            } 
            else 
            {
                // failed
                printf("!!! Failed to parse brush face line: %s (matched %d)\n", trimmed, matched);
            }
        }
        /*
        ----------------------------------
        */
    }
    printf("-----------------------------\n\n");
    printf("### MAP OBJECTS CREATED ### \n");
    printf("%i brushes. \n", map.brush_count);
    printf("\n");


    fclose(file);
    return true;
}
```

We have now successfully parsed the map data!

If you add `map_parse("test.map");` (or whatever you named your map file to...)
to your init() function you should have a very basic .map parser for your game.

In the terminal you should see the properties about the various brushes/entities appearing.

The next step is to create the various helper function we will need to turn this data we parsed into actual visible geometry.

We will need to make these functions next in this order:
- polygon_generate_from_brush()
- brushface_to_plane()
- polygon_sort_vertices()

These are the functions that will be doing most of the geometry math and making brushes into data we can turn into raylib models later.

## Generate Map Geometry
### TO BE CONTINUED...