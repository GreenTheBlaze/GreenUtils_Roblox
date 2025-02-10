Below listed are the methods/functions used in InstanceUtils!

## Miscellanious Functions

### createInstance
Creates a new [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) of type `className` using the provided `propertyTable` to set the object's properties. Similar to the default constructor [Instance.new](https://create.roblox.com/docs/reference/engine/datatypes/Instance#new) which is already provided by Roblox.

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
   This works too, however, it's recommended you follow what was done with the
   redPart as it's more efficient. If you're going to use this way, you MUST
   set the ClassName first before any other properties!
]]
local yellowPart = InstanceUtils:createInstance(nil, {
   ClassName = "Part",
   Name = "YellowPart",
   BrickColor = BrickColor.new(1, 1, 0),
   Parent = workspace
})

-- Used to show the properties of created objects.
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

-- Used to show the properties of the created instances.
print(typeof(redPart)) --> Instance
print(redPart.Parent.Name) --> SpawnLocation

print(typeof(yellowPart)) --> Instance
print(yellowPart.Parent.Name) --> Workspace
```

----

### setInstanceProperties
Sets an existing [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance)'s properties to the specified values provided in the `propertyTable`. Any invalid parameters will result in program execution terminating.

**Syntax:** `InstanceUtils:setInstanceProperties(targetInstance: Instance, propertyTable: {[string]: any}) → ()`

**Parameters:**

* `targetInstance`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The object that's to have its properties changed.

**Returns:**

* `void`

**Code Example:**
```lua
-- Use the createInstance method to make an example object.
local foo = InstanceUtils:createInstance("Part", {
   Name = "Foo",
   Parent = workspace
})

-- Output an example property, in this case the parent's Name to see the value
-- before setting.
print(foo.Parent.Name) --> Workspace

InstanceUtils:setInstanceProperties(foo, {
   Parent = game.Lighting
})

-- Output the property after setting change so we can confirm that it has been
-- changed correctly.
print(foo.Parent.Name) --> Lighting
```

----

### setInstancesProperties
Sets existing [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance)'s properties to the specified values provided in the `propertyTable`. Any invalid parameters will result in program execution terminating.

**Syntax:** `InstanceUtils:setInstancesProperties(...: {[string]: any}) → ()`

**Parameters:**

* `instanceConfigTables...`: [Dictionary](https://create.roblox.com/docs/luau/tables#dictionaries) - The configuration dictionaries for each individual [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) that is to have their properties changed, which must contain a `cloneInstance` entry and a `propertyTable` entry.

**Returns:**

* `void`

**Code Example:**
```lua
-- Use the createInstance method to make an example object.

local foo, bar = InstanceUtils:createInstances(
   {
      ClassName = "Part",
      Name = "Foo",
      Parent = workspace
   },
   {
      ClassName = "Part",
      Name = "Bar",
      Parent = game.Lighting
   }
)

-- Output an example property(s) from each instance, to see the value before
-- setting.
print(foo.Name) --> Foo
print(bar.Name) --> Bar

InstanceUtils:setInstancesProperties(
   {
      targetInstance = foo,
      propertyTable: {
         Name = "FooBar"
      }
   },
   {
      targetInstance = bar,
      propertyTable: {
         Name = "BarFoo"
      }
   }
)

print(foo.Name) --> FooBar
print(bar.Name) --> BarFoo
```

----

### cloneAnd
Creates a full copy of the provided `cloneInstance` including all of its descendants, ignoring all instances that are not [Archivable](https://create.roblox.com/docs/reference/engine/classes/Instance#Archivable).

**Syntax:** `InstanceUtils:cloneAndSetProperties(cloneInstance: Instance, propertyTable: {[string]: any}) → Instance`

**Parameters:**

* `cloneInstance`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The object to be cloned.

* `propertyTable`: [Dictionary](https://create.roblox.com/docs/luau/tables#dictionaries) - The configuration table for the properties of each individual [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) being cloned.

**Returns:**

* [`Instance`](https://create.roblox.com/docs/reference/engine/classes/Instance) - The cloned object.

**Code Example:**
```lua
local spawnLocation = workspace:FindFirstChild("SpawnLocation")

-- Used to show the properties of the original instances before they are cloned.
print(spawnLocation.BrickColor) --> Medium stone grey
print(spawnLocation.Parent.Name) --> Workspace

local spawnLocation2 = InstanceUtils:cloneAndSetProperties(spawnLocation, {
   Name = "SpawnLocation2",
   BrickColor = BrickColor.new("Really red"),
   Parent = game.Lighting
})

-- Used to show the changes in properties of the newly cloned instances.
print(spawnLocation2.BrickColor) --> Really red
print(spawnLocation2.Parent.Name) --> Lighting
```

----

### clonesAndSetProperties
Creates a full copy of the provided `cloneInstance` including all of its descendants, ignoring all instances that are not [Archivable](https://create.roblox.com/docs/reference/engine/classes/Instance#Archivable). Extended version of [cloneAndSetProperties](#cloneAndSetProperties).

**Syntax:** `InstanceUtils:clonesAndSetProperties(...: {[string]: any}) → ...Instance`

**Parameters:**

* `cloneConfigTables...`: [Dictionary](https://create.roblox.com/docs/luau/tables#dictionaries) - The configuration dictionaries for each individual [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) being cloned, which must contain a `cloneInstance` entry and a `propertyTable` entry.

**Returns:**

* [`Tuple`](https://create.roblox.com/docs/luau/tuples) - The created instances.

**Code Example:**
```lua
local spawnLocation = workspace:FindFirstChild("SpawnLocation")
local baseplate = workspace:FindFirstChild("Baseplate")

-- Shows the properties of the original instances so we can compare them
-- to after cloning.
print(spawnLocation.BrickColor) --> Medium stone grey
print(spawnLocation.Parent.Name) --> Workspace

print(baseplate.BrickColor) --> Medium stone grey
print(baseplate.Parent.Name) --> Workspace

local spawnLocation2, baseplate2 = InstanceUtils:clonesAndSetProperties(
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

-- Here we can see the new changes in the properties.
print(spawnLocation2.Name) --> SpawnLocation2
print(spawnLocation2.Parent.Name) --> Lighting

print(baseplate2.Name) --> Baseplate2
print(baseplate2.Parent.Name) --> Terrain
```

----

## Get
This method extension focusses mainly on retrieving instances and outputting them in the form of an [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) array. Exceptions to this include the getting instances from path methods.

### getSiblings
Returns an array (a numerically indexed table) containing all direct siblings of the given `searchObject`. In other words, it retrieves every [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) that shares the same [Parent](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Parent) as the `searchObject`.

**Syntax:** `InstanceUtils:getSiblings(searchObject: Instance) → {Instance}`

**Parameters:**

* `searchObject`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The object to whom the siblings are going to be fetched from.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the `searchObject`'s siblings.

**Code Example:**
```lua
local siblingsOfPointLight1 = InstanceUtils:getSiblings(game.Lighting.PointLight1) --> {Object 30, Object 31, Object 32}
```

----

### getAncestors
Returns an array containing all ancestors of the given `searchObject`. Specifically, it retrieves every [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) in the hierarchy above the `searchObject` starting from its immediate [Parent](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Parent), working up towards the [DataModel](https://create.roblox.com/docs/en-us/reference/engine/classes/DataModel).

**Syntax:** `InstanceUtils:getAncestors(searchObject: Instance) → {Instance}`

**Parameters:**

* `searchObject`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The object to whom the ancestors are going to be fetched from.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the `searchObject`'s ancestors.

**Code Example:**
```lua
-- Note that it's retrieving ancestors from Object 20 here.
local ancestorsOfBar = InstanceUtils:getAncestors(workspace.Part1.FooGui.TextLabel) --> {Object 19, Object 18, Object 1, DataModel}
```

----

### getChildrenOfName
Returns an array containing all children of the given `searchObject` of which their [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) properties are equal to the given `name`.

**Syntax:** `InstanceUtils:getChildrenOfName(searchObject: Instance, name: string) → {Instance}`

**Parameters:**

* `searchObject`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The object to whom the children are going to be fetched from.

* `name`: [string](https://create.roblox.com/docs/en-us/luau/strings) - The [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) of the children to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the `searchObject`'s children.

**Code Example:**
```lua
local childrenOfLighting = InstanceUtils:getChildrenOfName(game.Lighting, "PointLight") --> {Object 31, Object 32}

print("Name is '" .. childrenOfLighting[1].Name .. "' and ClassName is '" .. childrenOfCamera2[1].ClassName .. "'") --> Name is 'PointLight' and ClassName is 'PointLight'
print("Name is '" .. childrenOfLighting[2].Name .. "' and ClassName is '" .. childrenOfCamera2[2].ClassName .. "'") --> Name is 'PointLight' and ClassName is 'Part'
```

----

### getSiblingsOfName
Returns an array containing all siblings of the given `searchObject` of which their [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) properties are equal to the given `name`.

**Syntax:** `InstanceUtils:getSiblingsOfName(searchObject: Instance, name: string) → {Instance}`

**Parameters:**

* `searchObject`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The instance to whom the siblings are going to be fetched from.

* `name`: [string](https://create.roblox.com/docs/en-us/luau/strings) - The [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) of the siblings to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the `searchObject`'s siblings.

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
