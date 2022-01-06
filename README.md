
# Laser Defender 

## Introduction
Laser Defender is a 2D Space Shoot’em up game which is built in Unity game engine.
This game was built as a project In the University course Topics In Applications of Computer Science an was built by Or Smolarski, Dan Atzmi and Lital Feldman.
Most Art assets in this game were taken from Kenney assets - kenney.nl .
The game is shared on ShareMyGame.com by GameDev.tv .
https://sharemygame.com/@orsmo/laser-defender-battle-to-the-end
Link to public github repository of the project
https://github.com/orsmolarski/LaserDefender

This Document contains:

- Game Design 
- Scene overview & UI
- Feature analysis 
  - Core features
  - Secondary features
  - Effects 
  - Visual Effects
  - Sound Effects
  - Art assets
- Future versions
- Project experience



## Game Design

### Theme 
The Theme of Laser Defender is 2D space shoot’em up. This Genre is a sub genre of shooter games and was popular in the 1980’s. The genre is defined by a game in which the protagonist combats a large number of enemies by shooting at them while dodging their fire. The controlling player must rely primarily on reaction times to succeed.

### Core Mechanic 
The Core mechanics of Laser Defender in the players point of view are 
Controlling/Flying the spacecraft/player
Shooting enemies
Dodging bullets

### Game Loop
The game loop is a single level with endless enemy waves. The player shoots enemies for points and to eliminate danger until player health reaches zero and game ends.

### Objective
The players objective in Laser Defender is to gain the highest score as possible.
This derives the objectives of shooting as many enemies as possible and staying alive as long as possible.

### Player Experience
The player experience in 2D shoot’em up games and in specific in Laser Defender is frantic.  The player - a protagonist/hero , alone and outnumbered  in space battling endless waves of enemy spacecrafts while being shoot at. The stakes of winning the battle and achieving the highest score are all on the shoulders of the lone player, all along with the fear of blowing up and the game ending.
Scene overview & UI
Laser defender is composed of three scenes - Main menu scene, Game scene and Game over scene.

The Game begins in the Main Menu scene, when pressing “start” button the game scene loads and the game loop begins. When the player’s health reaches zero, the player’s spacecraft blows up and after a small delay the Game over scene is loaded which presents the options of loading the main menu scene or the game screen.

Music effect and background visual effect persists on all scenes and will be detailed in feature analysis. 
The UIDisplay script handles UI elements and is attached to canvas unity element.


### Main Menu Scene 
Presents the game title and subtitle, features soundtrack and background parallax scrolling.

### Game Scene
Features spacecraft which the player controls/flies and player projectiles, 
Enemies that shoot enemy projectiles and the player needs to dodge and avoid these enemies and their projectiles. The enemies follow fixed paths and spawn in waves. Explosions are displayed when an enemies or players health reaches zero and are created using the unity particle system.
Laser sounds effects occur when player/enemy shoots.
Has features of visual, audio effects, soundtrack and background parallax scrolling.
Displays a non interactable status panel that displays health on a slider and current score, the panel scales to fit screen. 

### Game Over scene
Displays a game over message and displays the players achieved score.
Contains “Play Again?” button which restarts the gameplay and a “Main Menu” button which loads the Main Menu scene.
Features soundtrack and background parallax scrolling.



## Feature Analysis
### Core features
### Player movement 
For player movement we are using the Unity input system.
The player game object is a component that listens to the input system and the behavior in reaction to input is defined in the Player script.
In player’s update method we take the vector from the input manager and calculate a new position for the player object which  depends on serializable fields such as padding and speed. The new position is restricted to the bounds we define with viewport and padding that is serializable.

### Enemies
The enemies are game object which are created at runtime.
They can cause damage to the player by collision and by shooting projectiles.
Enemies can have different attack behaviors and the shooting behaviors is defined in shooter script and can be tuned with serializable fields in the  unity inspector.
Enemies are spawned in waves and move in pre defined paths.

### Enemy movement
Enemy movement is defined in paths. The paths are constructed of waypoint game objects  which are located in the scene. The Pathfinder script is attached to enemy prefab and defines the movement along these paths, transforming the enemy’s position to each waypoint along the path by iterating over the waypoints on update, after passing through all waypoints the enemy object is destroyed.
The EnemySpawner gameobject which behavior is defined in EnemySpawner script manages the spawn of enemy waves during gameplay by iteration over the WaveConfig’s.

### Enemy Waves
A wave is a self contained moment in gameplay.
Waves in the game are defined as a scriptable object in WaveConfigSO script.
Each wave has a path prefab attached ( the path which enemies spawned in this waves will follow) and defines the move speed of the enemies and bounds spawn time between enemies which is random.

### Player Health
Player health is defined by heath and damage dealer script and can be tuned in serializable fields. Damage is taken and heath is deducted on onCollision events as player, enemy, and projectiles all have rigidbody elements.
When the players heath reaches zero, the player game object is destroyed and game over scene is loaded.




### Secondary 
### Shooting
Shooting behavior is defined in shooter script which is attached to enemies and player prefabs and receives a projectile prefab as a serializable field.
Shooting behavior can be tuned to differ between enemies by serializable fields.
For the purpose of eliminating friendly fire we constructed two new layers (Player and Enemy) in order for player projectiles to not hit player and edited in physics2D layer collision matrix.

### Enemy Health
The enemies are also prone to taking damage from collision with player and getting hit by play projectiles. The functionality of health and damage is defined in heath script and damage dealer script which are attached to the enemy prefabs.

### Score
Score is managed by a singleton of ScoreKeeper and is updated when enemies die in health script.

### Effects
Visual effects
Explosion effect 
The explosion effect is intended to highlight to the player when he has taken damage and also when enemies have taken damage.
The explosion effect is applied by the health script attached to enemy and player prefabs and is provided a unity particle system effect prefab that we made.
The effect is played on trigger events from rigid body colliders which are on player, enemies and projectiles.

### Camera Shake
The Camera Shake effect is intended to highlight and intensify the UX of the player getting hit and taking damage.
Camera shake effect is played when the player gets hit by Heath script and is defined in CameraShake script.
The core of the effect is randomly transforming main camera position in the unit circle for a 1 second.

### Background scrolling - Parallax Scrolling 
The Background parallax scrolling effect is intended to give the feeling of continuous flying through space.
It is achieved by first of all having two layers of background.
The sprite scroller script offsets the background layer on the y axis on update while the background is continuous and is concatenated continuously.
The top layer’s move speed is defined to be slightly faster than the bottom layer giving the parallax effect. 


### Sound effects

### SoundTrack
The soundtrack is an audio source attached to the AudioPlayer singleton which is looped and is played continuously throughout all scenes.

### Shooting and Damage 
These Sound effects are Instantiated as gameObject that lives for the duration of the runtime of the audio clip and then get destroyed.
The behavior is managed by AudioPlayer script which is attached to a singleton game object which gets called by Health script.

### Art Assets
We used various free art assets from the internet community in our game which include:
- Player ship
- Multiple enemy ships
- Projectiles 
- Backgrounds 
- Fonts 
- Audio clips 

All the Art assets can be found in the projects repository.

### Future Versions
Despite the nature of the game having one infinite level, it would be possible to add levels, but this would deform the game design.
Adding more enemy paths, enemy types, power ups , random asteroids and bosses could all be possible to add in future patches/version of Laser Defender.


### Project Experience
Although building this game was a not a trivial task, We learned about Unity game engine and the magnificent power of it, worked our way through the unknown of a new technology and found ourselves doing something amazing that we have yet to have done in the academic process of studying computer science -  expressing ourselves artistically through applications of computer science.


