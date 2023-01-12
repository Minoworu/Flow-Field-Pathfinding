# ReadMe
## PathFinding - Flow Field
Pathfinding has always been a big thing in video games and there are numerous ways of implementing them.
> Examples
 - AStar
 - DStar
 - Flowfield
 
> AStar and DStar calculate the shortest path from point A to point B.
This is a good method to implement if there aren't many objects in your game that require the pathfinding.
However, what if you do have a lot of objects?
 
## Goal Based Vector Field
A goal based vector field or also know as a flow field creates a grid where each cell has a direction vector.
The direction of the the vector will point towards the end goal.
Each cell also contains a cost. A cell is more costly if its an obstacle for example, or a different field terrain type like dirt.
The flow field directs the vectors by calculating the shortest path to the end goal from any given point in the map.
Sometimes it might direct the object through the dirt. 
This means that the cost through the dirt is cheaper than the around it.

 > A flow field is made up of 3 big components
 
| Component |
| ------ |
| Heat Map / Cost Field |
| Integration Field | 
| Flow Field |
 ## Heat Map / Cost Field
Each cell contains a byte, assigning a cost to a number between 0 - 255. By default they're assigned a value of 1.
The cost of the end goal is 0. Only the end goal can have a cost of 0.
Impassble objects will get assigned a cost of 255, meaning you are forced to "flow" around it 
Any cell that has a value between 2-254 means that you can walk on but should be avoided if possible.

Everytime the cost field would get modified, everything would have to get recalculated.

 ## Integration field
 The integration field is the biggest step of the process. This is where all the major calculations will be done.
 The intergration field algorithm is based on Dijkstra's Algorithm.
- First, All the cells are assigned a super high value. (People tend to go for 65535).
-  Second, The goal node gets its cost assigned to 0 and added to the open list.
-  Third, loop through the list and while its not empty, grab the first element, look at neighbouring cells,
   only add the cells if the new calculated cost is lower than the old cost
   Add the cost of the neighbouring cell with the cost of the original cell, add the cell to the open list.
   if the cell has a cost of 65535, the cell gets ignored.

 ## Flow field
 The final step of the creating the flow field is creating the flow field itself.
 All you need to do is loop over all cells and compare it with its neighbouring cells.
 Look for the lowest value of the neighbouring cells and point the vector of the cell towards that neighbour.
 To apply this to your objects, set the direction of your object to the direction of the current cell.
 
 
 ## Usage
 > When are flow fields used?
 
  To sum it up, flow fields are used to generate a huge crowd without having the calculations be really costly for your performances.
  They're commonly used in RTS games but also in general computer science

# Sources
https://www.youtube.com/watch?v=zr6ObNVgytk
https://leifnode.com/2013/12/flow-field-pathfinding/
https://howtorts.github.io/2014/01/04/basic-flow-fields.html



