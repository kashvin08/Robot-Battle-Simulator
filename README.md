# C++
------------------------

A turn-based simulation where various types of robots with unique abilities (Moving, Shooting, Seeing, Thinking) battle on a 2D grid. Robots can level up through an upgrade tree, revive
after death, and utilize special tactical abilities like jumping, hiding, or lifesteal

------------------------
Key Features:

Inheritance: Uses virtual public inheritance to create a "GenericRobot" that combines multiple modular skill sets.

Dynamic Upgrade System: Robots earn "Upgrade Points" by hitting enemies, allowing them to evolve into specialized tiers (e.g., Generic -> JumpBot -> JumpLongshotBot -> JumpLongshotScoutBot, etc).

Graveyard & Revival: When a robot dies, it enters a graveyard queue. The battlefield attempts to revive robots with a limited revival pool, resetting them to their base forms.

Automated Simulation: Reads initial configuration (grid size, steps, robot placement) from an external txt file and runs the battle until a victor is declared.

Detailed Logging: Every action—movement, shots fired, and upgrades—is logged both to the console and a log.txt file.

------------------------------

Robot upgrades tierlist:

Tier 1: Base Class (GenericRobot)
Tier 2: Hidebot, Jumpbot, Scoutbot
Tier 3 (originals): Juggernautbot, LifeStealbot, TrueDamagebot
Tier 4 (upgrade): JumpLifeStealbot etc...

Note: Upgrades can only be done with different types. For instance, a type of MovingRobot can be upgraded to a MovingShootingRobot which can also be eventually upgraded to a 
MoovingShootingSeeingRobot. A MovingRobot cannot upgrade to a MovingMovingRobot, MovingMovingMovingRobot etc..
------------------------------

Class Overview:

Battlefield: The engine of the simulation. Manages the 2D grid, the robot registry, the graveyard queue, and the simulation loop.

Robot (Abstract): The base interface.

MovingRobot: Handles grid navigation.

ShootingRobot: Manages ammo (shells) and hit detection.

SeeingRobot: Implements "Look" mechanics to find nearby enemies.

Specialized Bots:

JuggernautBot: Charges in straight lines, damaging everything in its path.

HideBot: Has a chance to avoid damage entirely.

SemiautoBot: Fires 3-round bursts with a 70% hit chance.

--------------------------------------------------------

Input File Format:

The program expects an input file of format:

M by N : 20 20
steps: 100
GenericRobot Alpha random random
GenericRobot Bravo 5 10

M by N: Defines the rows and columns.
steps: Total turns to simulate.
GenericRobot ((Name) (X) (Y)) Use random for coordinates to let the engine decide.

---------------------------------------------------------

Technical Implementation Details:

Diamond Problem: Resolved using virtual base classes for the four primary ability classes.

Operator Overloading: The << operator is overloaded for the Battlefield class to provide a clean syntax for adding robots: battlefield << newRobot;.

Memory Management: Implements a custom destructor in Battlefield to properly clean up all dynamically allocated Robot and Logger pointers.

Randomization: Utilises srand(time(0)) for varied simulation outcomes each run.

------------------------------------------------------------

Compilation:

C++11 compliant compiler or higher:

g++ -o robot_battle main.cpp
./robot_battle
