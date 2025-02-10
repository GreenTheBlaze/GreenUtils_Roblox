Below listed are the methods/functions used in InstanceUtils!

## Miscellanious Functions

### createInstance
Creates a new [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) of type `className` using the provided configuration dictionary to set the object's properties. Similar to the default constructor [Instance.new](https://create.roblox.com/docs/reference/engine/datatypes/Instance#new) which is already provided by Roblox.

**Syntax:** `InstanceUtils:createInstance(className: string, propertyTable: {[string]: any}) → Instance`

**Parameters:**

* `className`: [string](https://create.roblox.com/docs/luau/strings) - Class name of the new object to create.

* `propertyTable`: [Dictionary](https://create.roblox.com/docs/luau/tables#dictionaries) - The configuration dictionary in which the properties to configure for the new object should be listed.

**Returns:**

* [`Instance`](https://create.roblox.com/docs/reference/engine/classes/Instance) - The object created.

**Code Example:**
```lua
local redPart = InstanceUtils:createInstance("Part", {
   Name = "RedPart",
   BrickColor = BrickColor.new(1, 0, 0),
   Parent = workspace.SpawnLocation
})

--[[
   This works too, however, it's recommended you follow what was done with the redPart as it's more efficient
   If you're going to use this way, you MUST set the ClassName first before any other properties
]]
local yellowPart = InstanceUtils:createInstance(nil, {
   ClassName = "Part",
   Name = "YellowPart",
   BrickColor = BrickColor.new(1, 1, 0),
   Parent = workspace
})

-- Example output results of the instances' properties:
print(typeof(redPart)) --> Instance
print(redPart.Parent.Name) --> SpawnLocation

print(typeof(yellowPart)) --> Instance
print(yellowPart.Parent.Name) --> Workspace
```

----

### createInstances
Creates multiple instances based on the provided configuration dictionary. Extended version of [createInstance](#createInstance). Invalid properties provided will be flagged.

**Syntax:** `InstanceUtils:createInstances(...: {[string]: any}) → ...Instance`

**Parameters:**

* `propertyTables...`: [Dictionary](https://create.roblox.com/docs/luau/tables#dictionaries) - The dictionaries containing each individual object's property settings, which will be used to create the intended [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance)(s) correctly.

**Returns:**

* [`Tuple`](https://create.roblox.com/docs/luau/tuples) - The created instances.

**Code Example:**
```lua
local redPart, yellowPart = InstanceUtils:createInstances(
   {
      ClassName = "Part",
      Name = "RedPart",
      BrickColor = BrickColor.new(1, 0, 0),
      Parent = workspace.SpawnLocation
   },
   {
      ClassName = "Part",
      Name = "YellowPart",
      BrickColor = BrickColor.new(1, 1, 0),
      Parent = workspace
   }
)

-- Example output results of the instances' properties:
print(typeof(redPart)) --> Instance
print(redPart.Parent.Name) --> SpawnLocation

print(typeof(yellowPart)) --> Instance
print(yellowPart.Parent.Name) --> Workspace
```

----

### cloneAndReplaceProperties
Creates a full copy of the provided `cloneInstance` including all of its descendants, ignoring all instances that are not [Archivable](https://create.roblox.com/docs/reference/engine/classes/Instance#Archivable).

**Syntax:** `InstanceUtils:cloneAndReplaceProperties(cloneInstance: Instance, propertyTable: {[string]: any}) → Instance`

**Parameters:**

* `cloneInstance`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The object to be cloned.

* `propertyTable`: [Dictionary](https://create.roblox.com/docs/luau/tables#dictionaries) - The configuration table for the properties of each individual [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) being cloned.

**Returns:**

* [`Instance`](https://create.roblox.com/docs/reference/engine/classes/Instance) - The cloned object.

**Code Example:**
```lua
local spawnLocation = workspace:FindFirstChild("SpawnLocation")

print(spawnLocation.BrickColor) --> Medium stone grey
print(spawnLocation.Parent.Name) --> Workspace

-- Creates a clone of spawnLocation
local spawnLocation2 = InstanceUtils:cloneAndReplaceProperties(spawnLocation, {
   Name = "SpawnLocation2",
   BrickColor = BrickColor.new("Really red"),
   Parent = game.Lighting
})

print(spawnLocation2.BrickColor) --> Really red
print(spawnLocation2.Parent.Name) --> Lighting
```

----

### clonesAndReplaceProperties
Creates a full copy of the provided `cloneInstance` including all of its descendants, ignoring all instances that are not [Archivable](https://create.roblox.com/docs/reference/engine/classes/Instance#Archivable).
Creates full copies Instance objects based on the provided configuration array. Extended version of [cloneAndReplaceProperties](#cloneAndReplaceProperties).

**Syntax:** `InstanceUtils:clonesAndReplaceProperties(...: {[string]: any}) → ...Instance`

**Parameters:**

* `cloneConfigTables...`: [Dictionary](https://create.roblox.com/docs/luau/tables#dictionaries) - The configuration dictionaries for each individual [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) being cloned, which must contain a `cloneInstance` entry and a `propertyTable` entry.

**Returns:**

* [`Tuple`](https://create.roblox.com/docs/luau/tuples) - The created instances.

**Code Example:**
```lua
local spawnLocation = workspace:FindFirstChild("SpawnLocation")
local baseplate = workspace:FindFirstChild("Baseplate")

print(spawnLocation.BrickColor) --> Medium stone grey
print(spawnLocation.Parent.Name) --> Workspace

print(baseplate.BrickColor) --> Medium stone grey
print(baseplate.Parent.Name) --> Workspace

local spawnLocation2, baseplate2 = InstanceUtils:clonesAndReplaceProperties(
   {
      cloneInstance = spawnLocation,
      propertyTable = {
         Name = "SpawnLocation2",
         BrickColor = BrickColor.new("Really red"),
         Parent = game.Lighting
      }
   },
   {
      cloneInstance = baseplate,
      propertyTable = {
         Name = "Baseplate2",
         Parent = workspace.Terrain
      }
   }
)

print(typeof(fooBar)) --> Instance
print(typeof(aRedMeshPart)) --> FooBar

print(fooBar.Name) --> Camera
```

----

## Get
This method extension focusses mainly on retrieving instances and outputting them in the form of an `Instance` array. Exceptions to this include the getting instances from path methods.

### getSiblings
Returns an array (a numerically indexed table) containing all direct siblings of the given `child`. In other words, it retrieves every `Instance` that shares the same `Parent` as the `child`.

**Syntax:** `InstanceUtils:getSiblings(child: Instance) → {Instance}`

**Parameters:**

* `child`: The instance to whom the siblings are going to be searched from.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays): An array containing the `child`'s siblings.

**Code Example:**
```lua
local siblingsOfSky = InstanceUtils:getSiblings(game.Lighting.Sky) --> {game.Lighting.ANormalLight, game.Lighting.ANormalLightLol}
```

----

### getAncestors
Returns an array containing all ancestors of the given `descendant`. Specifically, it retrieves every `Instance` in the hierarchy above the `descendant`, starting from its immediate `Parent`, working up towards the `DataModel`.

**Syntax:** `InstanceUtils:getAncestors(descendant: Instance) → {Instance}`

**Parameters:**

* `descendant`: The instance to whom the ancestors are going to be searched from.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays): An array containing the `descendant`'s ancestors.

**Code Example:**
```lua
local ancestorsOfBar = InstanceUtils:getSiblings(workspace.Camera2.SomethingElse.Bar) --> {workspace.Camera2.SomethingElse, workspace.Camera2, workspace, game}
```

----

### getChildrenOfName
Returns an array containing all children of the given `parent` of which their `Object.Name` properties are equal to the given `name`.

**Syntax:** `InstanceUtils:getChildrenOfName(parent: Instance, name: string) → {Instance}`

**Parameters:**

* `parent`: The instance to whom the children are going to be searched from.

* `name`: The `Object.Name` to be looked for.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays): An array containing the `parent`'s children.

**Code Example:**
```lua
local childrenOfCamera2 = InstanceUtils:getChildrenOfName(workspace.Camera2, "FakeThing1") --> {workspace.Camera2.FakeThing1, workspace.Camera2.FakeThing1, workspace.Camera2.FakeThing1}

print("Name is '" .. childrenOfCamera2[1].Name .. "' and ClassName is '" .. childrenOfCamera2[1].ClassName .. "'") --> Name is 'FakeThing1' and ClassName is 'Camera'
print("Name is '" .. childrenOfCamera2[2].Name .. "' and ClassName is '" .. childrenOfCamera2[2].ClassName .. "'") --> Name is 'FakeThing1' and ClassName is 'Part'
print("Name is '" .. childrenOfCamera2[3].Name .. "' and ClassName is '" .. childrenOfCamera2[3].ClassName .. "'") --> Name is 'FakeThing1' and ClassName is 'Part'
```

----

### getSiblingsOfName
Returns an array containing all siblings of the given `parent` of which their `Object.Name` properties are equal to the given `name`.

**Syntax:** `InstanceUtils:getSiblingsOfName(child: Instance, name: string) → {Instance}`

**Parameters:**

* `sibling`: The instance to whom the siblings are going to be searched from.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays): An array containing the `sibling`'s siblings.

**Code Example:**
```lua
local siblingsOfWorkspace = InstanceUtils:getSiblingsOfName(workspace.Part1, "Part2") --> {workspace.Part2, workspace.Part2, workspace.Part2, workspace.Part2}

for _, sibling in siblingsOfASimpleTruss do
   print(sibling.Name)
   -- Output:
   --> Part2
   --> Part2
   --> Part2
   --> Part2
```
