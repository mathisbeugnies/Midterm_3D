Project: Third-Person Combat Game (Midterm UE5)
Student Name: Mathis Beugnies
Student ID: 7702283

==================================================
1. Features Added Beyond Requirements
==================================================

* Enhanced Player Mobility: 
I expanded the standard Third Person Character movement system by implementing crouching and aiming mechanics. This allows the player to utilize low obstacles for cover and engage in more tactical, precise ranged combat, which goes beyond the basic run-and-shoot requirements.

* Dynamic HUD Feedback: 
In addition to the required health bars and ammo counter, I added a dynamic "Enemies Remaining" text counter to the UI to provide better immediate feedback to the player.


==================================================
2. Design Decisions Differing from Specifications
==================================================

* Event-Driven Game State: 
The specification suggested a "CheckGameState" custom event called on every HP change. Instead, I opted for a more performant, event-driven architecture. I used Event Dispatchers (OnPlayerDied and OnEnemyDied) bound in the BP_GameMode at BeginPlay. This ensures win/lose logic only runs exactly when a death occurs, rather than polling constantly.

* Projectile Collision Handling: 
Instead of using the standard BeginOverlap event for the projectile, I changed the collision preset to BlockAllDynamic and used Event Hit. This generates actual physical impacts and blocking responses, which felt more robust for shooting mechanics.

* Retreat Distance: 
The prompt suggested computing a retreat distance of a minimum of 1500 units. During testing, I found that multiplying the retreat vector by 1200.0 units provided much better gameplay pacing and kept the AI within the boundaries of the 5000x5000 arena while still respecting the minimum distance rule.


==================================================
3. Known Bugs or Incomplete Features
==================================================

* Enemy Health Logic Delay: 
There is a minor order-of-operations issue in my TakeDamage_Enemy Blueprint logic. The Branch checking if the enemy's HP is <= 0 evaluates before the actual damage value is subtracted. As a result, an enemy that is at 1 HP and takes a hit will correctly drop to 0 HP on the HUD, but the death logic will not trigger immediately. The enemy survives at 0 HP and requires one additional hit to be destroyed. Other than this minor delay, the core logic works perfectly.
