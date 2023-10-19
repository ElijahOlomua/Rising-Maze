# Rising Maze

&nbsp;&nbsp;&nbsp;&nbsp; This is a project I worked on in Unreal Engine 5.2 where you traverse a maze by wall-running and double-jumping to avoid the rising lava. The game file is located <a href = "">here</a>. Upon launch of the game you might receive an error saying "Error: CDO Constructor Failed to find BP_ThirdPersonCharacter_C" which occurred when I deleted the starter character blueprint and am still trying to fix.

&nbsp;&nbsp;&nbsp;&nbsp; I've always thought wall-running was a cool game mechanic and thought it would be fun to try and build a game around it. It turns out that implementing a wall-running mechanic into a game is much more difficult than I anticipated with many layers of programming as this was one of my first projects in Unreal Engine. In fact, I used this project as a learning opportunity to learn more about Unreal Engine and its visual scripting language blueprints. Wall running like other movement-oriented game mechanics can get a bit complicated, so after struggling to implement it myself I looked over various other implementations on YouTube and game development forums to give myself a starting point. A large majority of the examples I saw followed the same pattern:
## Wall Run Pattern

- ### Can we Wall Run?
  - Check for collision
  - Is the object we collided with able to be wall-run? (Not walkable Z-axis value)
  - Are we falling?
  - Are we sprinting/holding a key down? (Optional)
  - Find wall run side and direction
- ### Begin Wall Run
  - Reduce air control and gravity
  - Constrain the Z-axis on the player (Plane constraint)
  - Tilt camera away from wall run-side
- ### Wall Run Loop
  - Line trace towards wall
  - Check if we are still in contact with the wall
  - Check if we are still in contact with the same wall (To prevent switching wall run directions)
  - Push character along wall run direction
- ### End Wall Run
  - If player falls off wall (Line trace has no collision or player tries to turn around to other wall run direction), if player jumps off wall
  - Set default air control and gravity
  - Set default plane constraints
  - End camera tilt
## Problems and bugs while developing
&nbsp;&nbsp;&nbsp;&nbsp; As mentioned at the top there is an error of a missing CDO which happened when I deleted the started third-person character blueprint, but this error has no effect on the gameplay.  

&nbsp;&nbsp;&nbsp;&nbsp; Another bug that I encountered during development was continuing wall running when wall running is supposed to be false effectively making you fly. This bug would occur when wall running for longer than 5 seconds because I have a timeline (A blueprint node that executes code every x seconds) that would run the wall run loop. Because this loop was used to check if we can still wall run, wall run never gets switched to false making the player float in mid-air. It was a simple fix by just changing the timeline to loop itself instead of running once.  

&nbsp;&nbsp;&nbsp;&nbsp; A recent and current bug involves the rendering of the walls when the wall running/jumping past them making the wall twitch and showing the lava underneath it. I have tried changing the render order of the wall and the lava mesh with no luck. This bug also does not affect the core gameplay but does make it a bit disorienting when trying to traverse the maze.  
