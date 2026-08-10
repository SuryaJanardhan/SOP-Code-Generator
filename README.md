# SOP-Code-Generator

Phase 1 includes deep research and analysis of problem statement.

Problem statement: SOP code document provides error/bug along with proper steps to follow for its resolve- it includes clear step by step instructions written in general language which is needed to apply for the resolve of that bug and produce a code an alternate code snippet as output.

Possible solution: Multiple individual agents in charge within a supervisor who handles invocation and global state of all these agents, once the user gives all required inputs includes (code base git url, sop doc) - post receiving the inputs supervisor agents reads the complete sop doc understands the error and its solution meanwhile another git agent in a sandbox env clones the repo understands repo tries to generates a proper knowledge graph, readme summary. Once both the agents return their responses to root agent! It uses further agents to do the neccessary actions inside the codebase using sop doc + knowledge graph. These sub agents are not static as the agent requirements depends on the flow of sop doc( write, read, cmd, planner... agents).

## Abv stated is not the only feasible solutions once the research is done we can fix 1 solution as root solution to the prblm statement.

