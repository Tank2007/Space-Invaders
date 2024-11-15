# Game Design Plan: Galactic War Troubles

## Initialization
### Initialize Game Variables:
- **player_position:** Tracks the x-coordinate of the spaceship.
- **enemy_positions:** List of (x, y) positions for all enemies.
- **projectiles:** List of active bullets fired by the player.
- **power_ups:** List of active power-up objects in the game.
- **score:** `0`
- **lives:** `3`
- **power_up_active:** `None` (Tracks active power-up effects, if any).
- **mouse_position:** `(x, y)`.

### Load Game Assets:
- **Images:** Spaceship, enemies, projectiles, power-ups.
- **Sounds:** Firing, explosions, power-ups.

### Set Up the Game Window and Event Listeners:
- Detect **mouse movement** to update `player_position`.
- Detect **mouse clicks** to fire bullets.

---

## Game Loop
**Repeat until the player has no lives or all enemies are destroyed:**

### Update Player Movement:
- Set `player_position.x` to the x-coordinate of `mouse_position`.

### Update Projectiles:
- For each projectile in `projectiles`:
  - Move the projectile upward (reduce its y-coordinate).
  - Check for collisions with enemies:
    - If collision occurs:
      - Remove the enemy and the projectile.
      - Increase the score.
      - Play explosion sound.
  - Remove projectiles that go out of bounds.

### Spawn and Update Enemies:
- Move all `enemy_positions` downward slightly.
- If an enemy reaches the player’s level:
  - Decrease `lives`.
  - Reset the enemy’s position or remove it.
- Occasionally fire enemy bullets toward the player.

### Spawn and Update Power-ups:
- Periodically spawn a power-up at a random position.
- Move power-ups downward.
- Check for collision with the player:
  - If collision occurs, activate the power-up effect:
    - **Double Fire:** Allow firing two bullets at once.
    - **Shield:** Temporarily make the player invincible.
    - **Extra Life:** Increase `lives` by 1.
  - Set `power_up_active` and start a timer to deactivate after a duration.

### Render Game Elements:
- Clear the screen.
- Draw the spaceship at `player_position`.
- Draw all active `enemy_positions`.
- Draw all `projectiles`.
- Draw all `power_ups`.
- Display the score and lives.

### Check Game Over Conditions:
- If `lives <= 0`: End the game.
- If all `enemy_positions` are cleared: End the game.

---

## End Screen
- Display a message: `"Game Over"` or `"You Win!"`.
- Show the final score.