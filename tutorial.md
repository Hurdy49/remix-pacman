# Pacman Remix Tutorial
### @explicitHints true

### ~button /#tutorial:/tutorials/pacman-remix

Rebuild and reimagine Pacman to explore how games communicate meaning.

### ~

## Introduction @showdialog

What happens when we change the audience’s experiences—such as the visuals or rules—within a game?  

How can we, as game designers and developers, communicate meaning?

In this tutorial, you will:
1. Recreate a minimalist version of *Pacman* using Microsoft MakeCode Arcade. This will help you understand how visuals, logic, and interaction work together to shape a player’s experience. 


2. Remix your game to communicate a new message, theme, or purpose — transforming entertainment into something more meaningful.

---

## Step 1: Create your Maze

Open the `||scene:Scene||` drawer and drag  
 `||scene:set tilemap to||` into the `||loops(noclick):on start||` block.


Click the grey square to open the tilemap editor.  
 Design a simple maze using walls and paths.


‼️Set your canvas size to at least **64x32** tiles.

&nbsp;

~hint Why does the canvas size matter? 🤔

---

A small canvas will limit your maze design.  

Use the dimension values in the bottom left corner to alter the size.
Make sure to unlock the ratio!

hint~

## Step 2: Create your Pacman Sprite

Open the `||sprites:Sprites||` drawer and drag  
  `||variables:set [mySprite] to sprite [ ] of kind [Player]||`  
  into the `||loops(noclick):on start||` block.

Click the grey square to draw your Pacman-style character.

&nbsp;

~hint What is a sprite? 👾

---

A sprite is a character or object that can move and interact in your game.

hint~

#### ~ tutorialhint
```
let mySprite = sprites.create(img`
. . . . . . . . 
. . 2 2 2 2 . . 
. 2 2 2 2 2 2 . 
. 2 2 2 2 2 2 . 
. . 2 2 2 2 . . 
. . . 2 2 . . . 
. . . . . . . . 
`, SpriteKind.Player)
```

---

## Step 3: Add Movement and Animation

From `||controller:Controller||`, drag  
`||controller:move [mySprite] with buttons||`  
into the `||loops(noclick):on start||` block.

(Optional) Add animation using `||animation:run image animation||`

&nbsp;

~hint Show me how

---

Use a short loop of images to animate your sprite’s mouth opening and closing.

hint~

#### ~ tutorialhint
```
controller.moveSprite(mySprite)
```

---

## Step 4: Place your Player in the Maze

Open the `||scene:Scene||` drawer and drag  
`||scene:place [mySprite] on top of random [tile]||`  
into the `||loops(noclick):on start||` block.

Choose a tile in your tilemap where the player should begin.

&nbsp;

#### ~ tutorialhint
```
scene.place(mySprite, tiles.getTileLocation(1, 1))
```

---

## Step 5: Add and Chomp Pellets

Create a new sprite of kind `||sprites:Food||` and place it on specific tiles using a loop.

Use `||sprites:on [sprite] of kind [Player] overlaps [otherSprite] of kind [Food]||` to detect when the player eats a pellet.

Increase score using `||info:change score by [1]||`

&nbsp;

~hint Why use a loop?

---

You can place multiple pellets at once by looping through tile locations.

hint~

#### ~ tutorialhint
```
for (let value of tiles.getTilesByType(assets.tile`pelletTile`)) {
    let pellet = sprites.create(img`
        . . . 
        . 5 . 
        . . . 
    `, SpriteKind.Food)
    tiles.placeOnTile(pellet, value)
}
sprites.onOverlap(SpriteKind.Player, SpriteKind.Food, function (player, pellet) {
    pellet.destroy()
    info.changeScoreBy(1)
})
```

---

## Step 6: Add a Ghost Enemy

Create a new sprite of kind `||sprites:Enemy||` and place it in the maze.

Use `||sprites:set velocity||` and `||sprites:set bounce on wall||` to make it move.

&nbsp;

~hint What is AI logic?

---

AI logic means the ghost moves on its own.  
Start simple - just bouncing off walls is enough.

hint~

#### ~ tutorialhint
```
let ghost = sprites.create(img`
. . . 3 3 3 3 . . . 
. 3 3 3 3 3 3 3 . . 
3 3 . 3 3 . 3 3 3 . 
3 3 3 3 3 3 3 3 3 . 
3 3 . . . . 3 3 3 . 
`, SpriteKind.Enemy)
ghost.setVelocity(50, 0)
ghost.setBounceOnWall(true)
```

---

## Step 7: Add Game Logic

Use `||info:start countdown [60] (s)||` to add a timer.

Use `||info:set life to [3]||` and reduce life on ghost collision.

End the game when all pellets are gone or lives run out.

&nbsp;

#### ~ tutorialhint
```
info.startCountdown(60)
info.setLife(3)
sprites.onOverlap(SpriteKind.Player, SpriteKind.Enemy, function (player, ghost) {
    info.changeLifeBy(-1)
})
```

---

## Step 8: Test Your Game!

Use the simulator to test your maze, movement, pellets, and ghost.

Fix any bugs before moving on.

&nbsp;

---

## Step 9: Remix the game to change its meaning! @showdialog

Now that you’ve built the core game, it’s time to remix it!


Your goal is to change the purpose of the game by modifying the player experience.

&nbsp;

---

## Remix with Purpose

Add, remove and modify elements within your game to communicate a different intent.

‼️Every decision you make should support what you are trying to communicate!
**Start with a clear goal or message.**

---

&nbsp;

Think about the various ways you can alter player experience to communicate meaning.

How may your audience's interpretation change if:

- The ghost was sick, and every time it caught you, you heard a sneeze?

- The entire game was black and white, with no sound at all?

- The time limit reduced everytime you ate a pellet?

&nbsp;

---

## Reflect and extend

What were you trying to communicate, and how did your modifications support this vision?

&nbsp;

**Testing and Reiteration**

1. Ask a peer to play your game without telling them your intent.  
What did they think the game was about? Did they respond as expected?

2. Do the same for your peer. What did you interpret from their game?

3. With your peer, brainstorm one idea each to enhance each other’s message.  
Implement the idea by modifying your game.

4. Repeat this process with other students in your class, taking note of how meaning is communicated and interpreted as you go.

&nbsp;

---

## Great work!

You’ve rebuilt and reimagined *Pacman* to explore how games can communicate meaning.  
Now you’re ready to design your own original serious game.

Click **Done** to finish this tutorial and begin your next project!


```blockconfig
let mySprite: Sprite = null
let ghost: Sprite = null
let pellet: Sprite = null
scene.setBackgroundColor(1)

```

```package
tutorial_asset_example=github:riknoll/tutorial_asset_example
```
