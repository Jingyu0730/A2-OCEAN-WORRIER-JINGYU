# A2-OCEAN-WORRIER-JINGYU

Add project detail below

@namespace
class SpriteKind:
    Decoration = SpriteKind.create()
    FISH = SpriteKind.create()
# set other coral reef to myDecor
# Player animation control 

def on_left_pressed():
    animation.run_image_animation(mySprite,
        assets.animation("""
            swim right
            """),
        200,
        True)
controller.left.on_event(ControllerButtonEvent.PRESSED, on_left_pressed)

# set game rules and game over

def on_countdown_end():
    game.game_over(False)
    game.set_game_over_message(False, "GAME OVER!")
info.on_countdown_end(on_countdown_end)
# collision logic 

def on_on_overlap(sprite3, otherSprite3):
    otherSprite3.destroy(effects.bubbles, 80)
    info.change_life_by(-1)
sprites.on_overlap(SpriteKind.player, SpriteKind.enemy, on_on_overlap)

# if player collects the bleach coral, the score will be +1 and the effect will be smiles

def on_on_overlap2(sprite2, otherSprite2):
    otherSprite2.destroy(effects.smiles, 100)
    info.change_score_by(1)
sprites.on_overlap(SpriteKind.player, SpriteKind.food, on_on_overlap2)

# if player touches the sharks, the score wil be -1 and the effects will be fire

def on_on_overlap3(sprite, otherSprite):
    otherSprite.destroy(effects.fire, 80)
    info.change_score_by(-1)
sprites.on_overlap(SpriteKind.player, SpriteKind.FISH, on_on_overlap3)
# game intital setup

# Define variables for all sprites used in the game
myFood: Sprite = None
Myenemy: Sprite = None
Myfish: Sprite = None
myDecor: Sprite = None
mySprite3: Sprite = None
mySprite2: Sprite = None
mySprite: Sprite = None

# set background color
scene.set_background_color(9)

# add instruction before game starts

game.splash("WELCOME TO OCEAN WARRIOR, PRESS A TO START")
game.show_long_text("TIPS: DON'T GET EATEN BY THE SHARKS, YOU HAVE THREE LIFE, GAME OVER IF USED ALL",
    DialogLayout.BOTTOM)
# set player and player control
mySprite = sprites.create(img("""
        . . . . . . . . . . . . . . . .
        . . . . . f f f f f f . . . . .
        . . . f f e e e e f 2 f . . . .
        . . f f e e e e f 2 2 2 f . . .
        . . f e e e f f e e e e f . . .
        . . f f f f e e 2 2 2 2 e f . .
        . . f e 2 2 2 f f f f e 2 f . .
        . f f f f f f f e e e f f f . .
        . f f e 4 4 e b f 4 4 e e f . .
        . f e e 4 d 4 1 f d d e f f . .
        . . f e e e 4 d d d d f d d f .
        . . . . f e e 4 e e e f b b f .
        . . . . f 2 2 2 4 d d e b b f .
        . . . f f 4 4 4 e d d e b f . .
        . . . f f f f f f e e f f . . .
        . . . . f f . . . f f f . . . .
        """),
    SpriteKind.player)
# set player life to 3
info.set_life(3)
# Enable arrow-key movement and keep player within the screen
controller.move_sprite(mySprite)
mySprite.set_stay_in_screen(True)
# set up total game time
info.start_countdown(30)

# for moving object
# Create fish that move horizontally and bounce off walls

for index in range(2):
    mySprite2 = sprites.create(img("""
            . . . . . . . . . . . . . . . .
            . . . . c c c c . . . . . . . .
            . . . c d d d d c c . . . . . .
            . . . c d c c c c c c . . . . .
            . . . c c d 4 4 4 4 c c . . . .
            c c . c 1 4 4 4 4 4 d 4 c . . .
            c 4 c 1 d 4 4 4 4 1 4 4 4 c . .
            c 4 c 1 4 4 4 4 4 1 4 4 4 4 c .
            f 4 4 1 4 4 4 4 4 1 4 4 4 4 4 f
            f 4 f 1 4 4 4 c c 1 4 f 4 4 4 f
            f 4 f d 4 4 f 4 4 1 4 4 4 4 4 f
            f f f f d 4 f 4 c 1 4 4 4 4 f .
            . . c f c 4 f f 4 4 d 4 f f . .
            . . c b d c 4 4 4 4 f f . . . .
            . . c d d d f f f f . . . . . .
            . . . c c c . . . . . . . . . .
            """),
        SpriteKind.player)
    mySprite2.vx = 10
    mySprite2.set_bounce_on_wall(True)
    mySprite2.y = randint(10, 80)

    
for index2 in range(2):
    mySprite3 = sprites.create(img("""
            . . c c c c c . . . . . . . . .
            . c c 5 5 5 5 c c c . . . . . .
            . c 5 5 5 5 5 5 5 5 c c . . . .
            . c 5 5 5 b b b b b b c . . . .
            . . c c b b 1 b b 1 1 1 c . . .
            c c . c 1 1 1 b 1 1 1 1 c . . .
            c 5 b c 1 1 1 b 1 1 1 d c . . .
            c 5 b b 1 1 1 b 1 c 1 d c c . .
            c 5 5 5 1 b 1 b 1 1 1 d d c c c
            c c b b 1 b 1 1 1 1 1 1 d d d f
            . . . f 1 b b 1 1 1 1 1 1 f f .
            . . . f b b b 1 1 1 1 1 f . . .
            . . . f 5 5 b b 1 1 f f . . . .
            . . . f 5 5 5 5 5 f . . . . . .
            . . . f f f f f f . . . . . . .
            . . . . . . . . . . . . . . . .
            """),
        SpriteKind.player)
    mySprite3.vx = 20
    mySprite3.set_bounce_on_wall(True)
    mySprite3.y = randint(10, 80)

   # Add simple swimming animation to the player 
animation.run_image_animation(mySprite,
    assets.animation("""
        swim right
        """),
    400,
    True)
    
    # DECORATION / CORAL REEF
for index3 in range(8):
    # Randomly place decorative coral sprites along the bottom
    myDecor = sprites.create(img("""
            . . . . . . c c . . . . . c c .
            . . . c c . c 3 c . c c . c 3 c
            . . c 3 6 c 3 3 c . c 3 c 6 3 c
            . . c 3 3 3 3 6 c . c 3 6 3 3 c
            . . . c 6 3 6 6 c c c 3 3 3 c .
            . . . . c c 6 6 c 6 c 6 3 3 c .
            . . . . c 3 c 6 c 3 3 c 6 6 c .
            c c . c 3 3 c c c c 3 3 c 6 c .
            c 3 c c 3 6 6 c 3 c 3 6 c 6 c .
            c 3 3 6 3 6 3 6 3 3 3 c c c c c
            . c 3 3 3 c 3 3 6 3 6 c c 3 3 c
            . . c 3 3 c c 3 3 3 6 c 3 3 6 .
            c c c 6 3 6 c c 6 3 6 6 3 6 c c
            c 3 3 3 3 3 c c c 3 6 3 3 3 3 c
            . c c 6 6 3 6 6 c 6 3 3 6 c c .
            . . . c 6 3 3 6 6 6 6 3 c . . .
            """),
        SpriteKind.Decoration)
    myDecor.set_position(randint(0, 180), 105)
    myDecor = sprites.create(img("""
            . . . . . . c c . . . . . c c .
            . . . c c . c b c . c c . c b c
            . . c b e c b b c . c b c e b c
            . . c b b b b e c . c b e b b c
            . . . c e b b b c c c b b b c .
            . . . . c c b e c e c e b b c .
            . . . . c b c e c b b c e e c .
            c c . c b b c c c c b b c e c .
            c b c c b e e c b c b e c e c .
            c b b e b e b e b b b c c c c c
            . c b b b c b b e b e c c b b c
            . . c b b c c b b b e c b b e .
            c c c e b e c c e b e e b e c c
            c b b b b b c c c b e b b b b c
            . c c e e b e e c e b b e c c .
            . . . c e b b e e e e b c . . .
            """),
        SpriteKind.Decoration)
    myDecor.set_position(randint(0, 180), 102)
    myDecor = sprites.create(img("""
            . . . . . c c . . . . . . c c .
            . c c . . c d c . . c c . c d c
            . c d c c d d c . . c d c e d c
            . c d d c d e c . . c d e d d c
            c c c e d e e c . c c d d d c .
            d d c c e e c e c e c e d d c .
            e d d c c c d e c d d c e e c .
            d e d d e d d c c c d d c e c .
            d c e d d d c c d c d e c e c .
            c c c d d c d e d d d c c c c c
            c c c e d c d d e d e c c d d c
            e d c e d e d d d d e c d d e .
            e d d e e d d d e d e e d e c c
            c e d d e d c c c d e d d d d c
            . c e e e c c e c e d d e c c .
            . . c e e c c e e e e d c . . .
            """),
        SpriteKind.Decoration)
    myDecor.set_position(randint(0, 180), 97)
    myDecor = sprites.create(img("""
            ....88..........
            ....868.........
            .....868........
            ......868.......
            .......868......
            .......868......
            ........868.....
            ........868.....
            ........8668....
            ........8668....
            ........8668....
            ........8768....
            ........8768....
            .......86768....
            .......87768....
            .......6778.....
            ......67676.....
            ......67676.....
            .....65656......
            ....655656......
            ....65656.......
            ...876756.......
            ..876776...8....
            ..67678....8....
            .876668...88....
            .67868....86....
            .86868...876....
            868668..8768....
            86868..87678....
            86868..8766.....
            86868.87678.....
            86878.8766......
            8787887678......
            876768768.88....
            876778668.678...
            876676668..678..
            .676778668..678.
            .8766778668.6778
            .877667688885678
            ..87667768885656
            ..86766778887856
            ...8776677876876
            ....877667768668
            .....87766768668
            ......877677668.
            .......87667668.
            ........876768..
            ........87688...
            """),
        SpriteKind.Decoration)
    myDecor.set_position(randint(0, 180), 97)
    myDecor = sprites.create(img("""
            . . . . . c c . . . . . . c c .
            . c c . . c 3 c . . c c . c 3 c
            . c 3 c c 3 3 c . . c 3 c 6 3 c
            . c 3 3 c 3 6 c . . c 3 6 3 3 c
            c c c 6 3 6 6 c . c c 3 3 3 c .
            3 3 c c 6 6 c 6 c 6 c 6 3 3 c .
            6 3 3 c c c 3 6 c 3 3 c 6 6 c .
            3 6 3 3 6 3 3 c c c 3 3 c 6 c .
            3 c 6 3 3 3 c c 3 c 3 6 c 6 c .
            c c c 3 3 c 3 6 3 3 3 c c c c c
            c c c 6 3 c 3 3 6 3 6 c c 3 3 c
            6 3 c 6 3 6 c 3 3 3 6 c 3 3 6 .
            6 3 3 6 6 6 3 c 6 3 6 6 3 6 c c
            c 6 3 3 6 3 c c c 3 6 3 3 3 3 c
            c c 6 6 6 c c 6 c 6 3 3 6 c c .
            c c c 6 6 c c 6 6 6 6 3 c . . .
            """),
        SpriteKind.Decoration)
    myDecor.set_position(randint(0, 180), 109)

def on_update_interval():
# moving fish sprites every few seconds
    global Myfish
    Myfish = sprites.create(assets.image("""
        food
        """), SpriteKind.FISH)
    Myfish.set_position(scene.screen_width(), randint(5, 80))
    Myfish.vx = -75
game.on_update_interval(5000, on_update_interval)

def on_update_interval2():
 # enemy sprites (e.g., sharks) that move toward the player
    global Myenemy
    Myenemy = sprites.create(assets.image("""
        food
        """), SpriteKind.enemy)
    Myenemy.set_position(scene.screen_width(), randint(5, 80))
    Myenemy.vx = -75
game.on_update_interval(5000, on_update_interval2)

def on_update_interval3():
# Collect coral (food) that increases score when collected
    global myFood
    myFood = sprites.create(img("""
            . . . . . . d d . . . . . d d .
            . . . d d . d 1 d . d d . d 1 d
            . . d 1 1 d 1 1 d . d 1 d 1 1 d
            . . d 1 1 1 1 1 d . d 1 1 1 1 d
            . . . d 1 1 1 1 d d d 1 1 1 d .
            . . . . d d 1 1 d 1 d 1 1 1 d .
            . . . . d 1 d 1 d 1 1 d 1 1 d .
            d d . d 1 1 d d d d 1 1 d 1 d .
            d 1 d d 1 1 1 d 1 d 1 1 d 1 d .
            d 1 1 1 1 d 1 1 1 1 1 d d d d d
            . d 1 1 1 d 1 1 1 1 1 1 d 1 1 d
            . . d 1 1 d d 1 1 1 d d 1 1 d .
            d d d 1 1 1 d d 1 1 1 d 1 1 d d
            d 1 1 1 1 1 d d d 1 1 1 1 1 1 d
            d d d d 1 1 1 1 d 1 1 1 1 d d .
            . . . d d d 1 1 1 d 1 1 d . . .
            """),
        SpriteKind.food)
    myFood.set_position(scene.screen_width(), randint(5, 115))
    myFood.vx = -75
game.on_update_interval(1800, on_update_interval3)

# THE END
