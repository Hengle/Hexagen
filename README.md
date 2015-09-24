# Hexagen
Hexagon grid generator for Dota 2 custom games

Hexagen utilizes cube coordinates as presented by Amit Patel for generation
http://www.redblobgames.com/grids/hexagons/

Example Results:  
http://i.imgur.com/ZU7MQvs.jpg  
http://i.imgur.com/eY94qGS.jpg  
http://i.imgur.com/a2DKdzC.jpg  
http://i.imgur.com/yqYCS8o.jpg

# How To Use
```lua
Hexagen:GenerateHexagonGrid(GridCenter, HexRadius, PathWidth, LengthTable)
```
GridCenter  (Vector): The center of the hex grid  
HexRadius  (Number): The distance from the center of a hex tile to one of the corners  
PathWidth  (Number): The distance to leave between adjacent hex tiles  
LengthTable (Table): A table that defines the length of each of the 6 legs

Example:  
```lua
TileList = Hexagen:GenerateHexagonGrid(Vector(0, 0, 128), 64, 32, {3, 2, 2, 3, 2, 2}))
```

TileList stores a list of all Hexes and Nodes, as well as the count of each

Hexagen also includes iterators to iterate over the results of a TileList
```lua
-- Iterate over all Hexes
for HexData in TileList:AllHexes() do
	...
end

-- Iterate over all Nodes
for NodeData in TileList:AllNodes() do
	...
end
```

To run a pathfinding query on a grid, use 
```lua
PathList = TileList:FindPath(PathType, StartingName, EndingName)
PathList = TileList:FindPath("Node", "Node_21", "Node_1")
PathList = TileList:FindPath("Hex", "Hex_12", "Hex_3")
```
Where PathType is either "Hex" or "Node" to run a hex or node query. Starting/Ending Name are the name of the tiles for the path to start and end at

PathList will be a list of all the names of the tiles in the path, or nil if no route was found

For more information about how to use HexList, see addon_game_mode.lua
