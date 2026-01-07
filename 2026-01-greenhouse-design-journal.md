# Design Journal: Greenhouse Minigame  
*Technical Reflection with Code References*

## Project Overview
The greenhouse minigame was developed in Twine using Twee syntax as a systems-driven interactive environment rather than a traditional branching narrative. Instead of prioritizing dialogue or plot progression, the project centers on **player movement, spatial constraints, and state-based interaction**. The greenhouse operates as a small simulation in which player input updates variables, variables govern valid actions, and conditional logic determines both movement and visual feedback.

## Grid Logic & Player Position
The core system is a grid-based movement model. Player location is tracked using `$playerRow` and `$playerCol`, which are converted into a single tile index for comparison against walkable tiles. This conversion appears throughout the movement logic, for example:

```twee
(($playerRow - 1) * $cols) + ($playerCol - 1)
```

This abstraction allows the greenhouse to treat space numerically rather than narratively. Instead of writing bespoke logic for each location, movement checks are generalized across the grid. As a result, the system scales cleanly: adding or removing tiles does not require rewriting core movement logic.

## Walkability & Conditional Movement
Movement is validated through layered conditional checks that confirm both **grid boundaries** and **tile walkability**. A representative example from the movement logic checks whether a destination tile is within bounds and contained in the `$walkable` set:

```twee
if $playerCol > 1 and $walkable contains ((($playerRow - 1) * $cols) + ($playerCol - 2))
```

This structure ensures that invalid movement never resolves. The player cannot leave the grid or enter tiles that are not explicitly permitted. Importantly, the system fails safely: if a condition is not met, movement simply does not occur, rather than producing an error state.

This approach reflects a deliberate design choice to prioritize **constraint-based design**. Instead of allowing movement everywhere and correcting mistakes afterward, the system only permits actions that are valid according to the current state.

## Interface Feedback & Tile Representation
The greenhouse visually reinforces its underlying logic through conditional rendering. Tiles change appearance based on whether they are walkable, blocked, or occupied by the player. These visual distinctions are driven directly by the same variables that control movement, creating a tight feedback loop between logic and presentation.

Tile states are checked against `$walkable` to determine styling, meaning that the interface itself acts as a readable map of the system’s rules. This reduces the need for explanatory text and allows players to infer affordances through interaction.

From a technical standpoint, this required careful synchronization between movement conditions and display logic. Any inconsistency between the two immediately surfaced as a visual bug, which made debugging both easier and more necessary.

## Iteration, Bugs, and Edge Cases
Early iterations exposed how sensitive grid-based systems are to small logical errors. Off-by-one mistakes in index calculations or incomplete boundary checks caused unintended behavior, such as allowing movement into nonexistent tiles or blocking valid paths.

These issues highlighted the importance of consistent tile math. By standardizing the index calculation formula and reusing it everywhere movement or rendering depended on position, I reduced redundancy and made the system more reliable. Debugging became a matter of checking assumptions about state rather than hunting for isolated errors.

## Reflection on Systems Design
This project reframed how I think about Twine as a platform. Rather than using it primarily for branching narrative, I treated it as a **rules engine** capable of supporting procedural interaction. Variables, conditionals, and presentation logic work together to produce meaning through structure rather than text alone.

The greenhouse minigame demonstrates how spatial logic and constraint-based design can function as expressive tools. Understanding where the player *cannot* go is just as important as where they can, and those limitations are communicated through consistent systems rather than narrative explanation.

If extended further, this architecture could support more complex mechanics such as evolving tile states, interaction history, or time-based changes, all without fundamentally altering the existing movement system.
