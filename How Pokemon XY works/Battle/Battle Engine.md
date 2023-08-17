# The Pokemon Battle Engine

The Pokemon Battle engine in generation 6 games reuses a lot of code dating back to gen 3 games. This is because the battle calculations remain mostly unchanged (outside of the fairy type getting introduced in XY) so all the changes between generations can be summarized as new battle modes or side features getting added (e.g. Inverse battles in XY).

The Battle AI in gen 6 games is implemented as a number of really long Pawn Scripts (inside `btl_ai.garc`). These have a huge labyrinth of if-elses that evaluate the options the AI has in each turn of a battle and assign scores to each possibility. The game then executes the possibility with the highest scoring.

The AI operates in multiple modes with different scoring for battle possibilities. This lets pokemon trainers be classified into different skill groups and enables a progression in difficulty. [TODO: investigate AI modes].

[TODO: investigate how Trainer Classes are implemented]

[TODO: investigate how encounter tables work]

[TODO: investigate how Battle Cheatu and Battle Maison work]

[TODO: investigate how Live Cup challenges work]