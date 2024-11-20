# Test Plan for Galactic War Troubles

## Part 1. Unit Testing the Game Mechanics
### Description
Test individual game mechanics, such as movement, shooting, and collision detection.

| **Test Case**                | **Test Data**                              | **Expected Outcome**                                                                                                                                             |
|------------------------------|--------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Player movement              | Move mouse to `(x, y)`                     | Spaceship follows the mouse's `x` coordinate.                                                                                                                   |
| Bullet firing                | Left mouse click while playing             | A projectile spawns at the player’s position and moves upward.                                                                                                  |
| Collision with enemy         | Projectile intersects with an enemy sprite | Enemy is removed from the screen, score increases, explosion sound plays, and projectile is removed.                                                            |
| Boundary limits for enemies  | Enemy at `(screen_width, y)` tries to move | Enemy wraps to the other side of the screen or stops depending on design.                                                                                       |
| Power-up activation          | Player touches power-up at `(x, y)`        | Power-up activates its effect (e.g., shield, double fire) and starts a countdown timer.                                                                          |

---

## Part 2. Logic Testing the Game Rules and Calculations
### Description
Verify correctness in game rules and score calculations.

| **Test Case**                 | **Test Data**                     | **Expected Outcome**                                                                                               |
|-------------------------------|-----------------------------------|-------------------------------------------------------------------------------------------------------------------|
| Score calculation             | Enemy destroyed                   | Score increases by `+10`.                                                                                         |
| Level progression             | Score milestones (100, 200, 500) | Game level increases, and enemy speed increases incrementally by `+10%`.                                          |
| Power-up duration             | Activate shield power-up          | Player is invincible for `10 seconds`. Shield deactivates, and normal gameplay resumes.                           |
| Bonus for multi-kill          | Destroy 3 enemies simultaneously | Score bonus of `+50 points` is applied.                                                                           |
| Asteroid collision            | Asteroid destroyed by projectile  | Possible random drop of power-up (e.g., `1 in 3` chance) and asteroid disappears.                                  |

---

## Part 3. Boundary Testing: Edge Cases and Limits
### Description
Test game functionality under extreme or unusual scenarios.

| **Test Case**                     | **Test Data**                              | **Expected Outcome**                                                                                   |
|-----------------------------------|--------------------------------------------|-------------------------------------------------------------------------------------------------------|
| Maximum score                     | Player score reaches `9999`                | Score stops increasing, becomes visually distinct (e.g., gold frame), and gameplay continues smoothly. |
| Minimum lives                     | Lives reach `0`                            | Game Over screen appears, and gameplay stops.                                                         |
| Power-up collision at boundary    | Power-up spawns at `(screen_width, y)`     | Power-up remains within screen boundaries and is collectible by the player.                           |
| Fastest enemy speed               | Enemy speed maxes out after level `10`     | Gameplay continues smoothly without glitches.                                                         |
| Clearing all enemies simultaneously | All enemies hit by explosion power-up    | Game transitions to the next wave without skipping or freezing.                                       |

---

## Part 4. Integration Testing: System Interaction
### Description
Test how different parts of the game work together.

| **Test Case**                     | **Test Data**                            | **Expected Outcome**                                                                                       |
|-----------------------------------|------------------------------------------|-----------------------------------------------------------------------------------------------------------|
| Scoring after enemy hit           | Projectile collides with enemy           | Score updates on-screen immediately after enemy is destroyed.                                             |
| Menu interaction                  | Click on "Pause Menu" button             | Gameplay freezes, and menu options are displayed. Clicking "Resume" restarts gameplay seamlessly.         |
| Power-up collection with enemies  | Collect power-up while enemies are active | Power-up effect is applied, and enemies continue normal behavior.                                         |
| Collision during level transition | Player at level boundary during level up | Player maintains position, and enemies update correctly without glitches.                                 |

---

## Part 5. Handling Bad Input and Run-Time Errors
### Description
Ensure that invalid input or errors do not crash the game.

| **Test Case**                     | **Test Data**                            | **Expected Outcome**                                                                                       |
|-----------------------------------|------------------------------------------|-----------------------------------------------------------------------------------------------------------|
| Invalid key press                 | Key press: `z`                           | Game ignores input, and no errors occur.                                                                  |
| Corrupt save file                 | Simulate a corrupted save file           | Game notifies the player of error and allows a new game to be started without crashing.                    |
| Infinite loop prevention          | Enemy spawns collide repeatedly          | Game processes each event separately, and loop prevention logic prevents freezing.                        |
| Missing assets                    | Remove `enemy.png` from assets folder    | Game loads with placeholder image and logs an error without crashing.                                     |

---

## Part 6. Test Table

| **Test Case**             | **Test Data**                 | **Expected Outcome**                                                                                                                                                          |
|---------------------------|-------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Player count              | `0`, `1`, `4`, `5` players    | Game prompts for user input. For invalid input (`>4`), it displays: "Please enter a number 1 through 4."                                                                      |
| Score increase            | Destroy enemies (`10`, `100`) | Score increases based on enemies destroyed. At `9999`, score freezes and is visually highlighted.                                                                             |
| Invalid input             | Key presses: `bc`, `#@!`      | Game ignores all keys except `a`, `d`, left/right arrow, and spacebar.                                                                                                       |
| Menu interaction          | Click "Pause Menu"            | Gameplay halts, menu displays options, and upon resume, the game continues seamlessly.                                                                                        |
| Edge collision            | Enemy at `(screen_width, y)`  | Enemy wraps to the opposite side or stops at the boundary, depending on design.                                                                                              |
