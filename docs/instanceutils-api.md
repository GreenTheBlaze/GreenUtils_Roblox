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

--[[
   Here, you can create children too within the method if you wanted to save
   lines of space within programs, however these will not be returned.

   This is the example tree structure that was created here:

   GreenPart
   ├─ Baz
   │  ├─ Garb
   │  └─ Jarp
   └─ Bazifyer
]]
local greenPart = InstanceUtils:createInstance("Part", {
   Name = "GreenPart",
   BrickColor = BrickColor.new(0, 1, 0),
   Parent = workspace.SpawnLocation,
   Children = {
      {
         ClassName = "SurfaceGui",
         Name = "Baz",
         Children = {
            {
               ClassName = "TextLabel",
               Name = "Garb"
            },
            {
               ClassName = "TextBox",
               Name = "Jarp"
            }
         }
      },
      {
         ClassName = "UIGradient",
         Name = "Bazifyer"
      }
   }
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
Sets an existing [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance)'s properties to the specified values provided in the `propertyTable`. Any invalid parameters will result in program execution termination.

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
Sets existing [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance)'s properties to the specified values provided. Any invalid parameters will result in program execution termination.

**Syntax:** `InstanceUtils:setInstancesProperties(...: {[string]: any}) → ()`

**Parameters:**

* `instanceConfigTables...`: [Dictionary](https://create.roblox.com/docs/luau/tables#dictionaries) - The configuration dictionaries for each individual [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) that is to have their properties changed, which must contain a `cloneInstance` entry and a `propertyTable` entry.

**Returns:**

* `void`

**Code Example:**
```lua
-- Use the createInstances method to make the example objects.
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

### cloneAndSetProperties
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

* `cloneConfigTables...`: [Dictionary](https://create.roblox.com/docs/luau/tables#dictionaries) - The configuration dictionaries for each individual [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) being cloned, which must contain both a `cloneInstance` entry and a `propertyTable` entry in each dictionary to be validated.

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

----

### getDescendantsOfName
Returns an array containing all descendants of the given `searchObject` of which their [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) properties are equal to the given `name`.

**Syntax:** `InstanceUtils:getDescendantsOfName(searchObject: Instance, name: string) → {Instance}`

**Parameters:**

* `searchObject`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The instance to whom the descendants are going to be fetched from.

* `name`: [string](https://create.roblox.com/docs/en-us/luau/strings) - The [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) of the descendants to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the `searchObject`'s descendants.

**Code Example:**
```lua
-- Confirm there are no instances named "Jarp" beforehand so we can confirm this
-- works.
local descendantsOfLightning = InstanceUtils:getDescendantsOfName(game.ReplicatedStorage, "Jarp") --> {}

local jarp, baz = InstanceUtils:createInstances(
   {
      ClassName = "SurfaceGui",
      Name = "Jarp",
      Parent = game.ReplicatedStorage
      Children = {
         {
            ClassName = "TextLabel",
            Name = "Jarp"
         }
      }
   },
   {
      ClassName = "SurfaceGui",
      Name = "Frobulator",
      Parent = game.ReplicatedStorage
   }
)

descendantsOfLightning = InstanceUtils:getDescendantsOfName(game.ReplicatedStorage, "Jarp") --> {game.ReplicatedStorage.Jarp, game.ReplicatedStorage.Jarp.Jarp}
```

----

### getAncestorsOfName
Returns an array containing all ancestors of the given `searchObject` of which their [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) properties are equal to the given `name`.

**Syntax:** `InstanceUtils:getAncestorsOfName(searchObject: Instance, name: string) → {Instance}`

**Parameters:**

* `searchObject`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The instance to whom the ancestors are going to be fetched from.

* `name`: [string](https://create.roblox.com/docs/en-us/luau/strings) - The [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) of the ancestors to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the `searchObject`'s ancestors.

**Code Example:**
```lua
-- TODO: Make this.
```

----

### getChildrenOfNameRange
Returns an array containing all children of the given `searchObject` of which their [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) properties are equal to any of values in `nameRangeTable`.

**Syntax:** `InstanceUtils:getChildrenOfNameRange(searchObject: Instance, nameRangeTable: {string}) → {Instance}`

**Parameters:**

* `searchObject`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The instance to whom the children are going to be fetched from.

* `nameRangeTable`: [Array](https://create.roblox.com/docs/luau/tables#arrays) - The individual [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) values of the children to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the `searchObject`'s children.

**Code Example:**
```lua
-- TODO: Make this.
```

----

### getSiblingsOfNameRange
Returns an array containing all siblings of the given `searchObject` of which their [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) properties are equal to any of values in `nameRangeTable`.

**Syntax:** `InstanceUtils:getChildrenOfNameRange(searchObject: Instance, nameRangeTable: {string}) → {Instance}`

**Parameters:**

* `searchObject`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The instance to whom the siblings are going to be fetched from.

* `nameRangeTable`: [Array](https://create.roblox.com/docs/luau/tables#arrays) - The individual [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) values of the siblings to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the `searchObject`'s siblings.

**Code Example:**
```lua
-- TODO: Make this.
```

----

### getDescendantsOfNameRange
Returns an array containing all descendants of the given `searchObject` of which their [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) properties are equal to any of values in `nameRangeTable`.

**Syntax:** `InstanceUtils:getDescendantsOfNameRange(searchObject: Instance, nameRangeTable: {string}) → {Instance}`

**Parameters:**

* `searchObject`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The instance to whom the descendants are going to be fetched from.

* `nameRangeTable`: [Array](https://create.roblox.com/docs/luau/tables#arrays) - The individual [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) values of the descendants to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the `searchObject`'s descendants.

**Code Example:**
```lua
-- TODO: Make this.
```

----

### getAncestorsOfNameRange
Returns an array containing all ancestors of the given `searchObject` of which their [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) properties are equal to any of values in `nameRangeTable`.

**Syntax:** `InstanceUtils:getAncestorsOfNameRange(searchObject: Instance, nameRangeTable: {string}) → {Instance}`

**Parameters:**

* `searchObject`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The instance to whom the ancestors are going to be fetched from.

* `nameRangeTable`: [Array](https://create.roblox.com/docs/luau/tables#arrays) - The individual [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) values of the ancestors to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the `searchObject`'s ancestors.

**Code Example:**
```lua
-- TODO: Make this.
```

----

### getChildrenOfClass
Returns an array containing all children of the given `searchObject` of which their [Object.ClassName](https://create.roblox.com/docs/en-us/reference/engine/classes/Object#ClassName) properties are equal to the given `className`.

**Syntax:** `InstanceUtils:getChildrenOfClass(searchObject: Instance, className: string) → {Instance}`

**Parameters:**

* `searchObject`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The object to whom the children are going to be fetched from.

* `className`: [string](https://create.roblox.com/docs/en-us/luau/strings) - The [Object.ClassName](https://create.roblox.com/docs/en-us/reference/engine/classes/Object#ClassName) of the children to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the `searchObject`'s children.

**Code Example:**
```lua
local childrenOfLighting = InstanceUtils:getChildrenOfClass(game.Lighting, "Part") --> {Object 32, Object 33}

print("Name is '" .. childrenOfLighting[1].Name .. "' and ClassName is '" .. childrenOfCamera2[1].ClassName .. "'") --> Name is 'PointLight' and ClassName is 'Part'
print("Name is '" .. childrenOfLighting[2].Name .. "' and ClassName is '" .. childrenOfCamera2[2].ClassName .. "'") --> Name is 'PointLight1' and ClassName is 'Part'
```

----

### getSiblingsOfClass
Returns an array containing all siblings of the given `searchObject` of which their [Object.ClassName](https://create.roblox.com/docs/en-us/reference/engine/classes/Object#ClassName) properties are equal to the given `className`.

**Syntax:** `InstanceUtils:getSiblingsOfClass(searchObject: Instance, className: string) → {Instance}`

**Parameters:**

* `searchObject`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The object to whom the siblings are going to be fetched from.

* `className`: [string](https://create.roblox.com/docs/en-us/luau/strings) - The [Object.ClassName](https://create.roblox.com/docs/en-us/reference/engine/classes/Object#ClassName) of the siblings to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the `searchObject`'s siblings.

**Code Example:**
```lua
-- TODO: Make this.
```

----

### getDescendantsOfClass
Returns an array containing all descendants of the given `searchObject` of which their [Object.ClassName](https://create.roblox.com/docs/en-us/reference/engine/classes/Object#ClassName) properties are equal to the given `className`.

**Syntax:** `InstanceUtils:getDescendantsOfClass(searchObject: Instance, className: string) → {Instance}`

**Parameters:**

* `searchObject`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The object to whom the descendants are going to be fetched from.

* `className`: [string](https://create.roblox.com/docs/en-us/luau/strings) - The [Object.ClassName](https://create.roblox.com/docs/en-us/reference/engine/classes/Object#ClassName) of the descendants to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the `searchObject`'s descendants.

**Code Example:**
```lua
-- TODO: Make this.
```

----

### getAncestorsOfClass
Returns an array containing all ancestors of the given `searchObject` of which their [Object.ClassName](https://create.roblox.com/docs/en-us/reference/engine/classes/Object#ClassName) properties are equal to the given `className`.

**Syntax:** `InstanceUtils:getAncestorsOfClass(searchObject: Instance, className: string) → {Instance}`

**Parameters:**

* `searchObject`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The object to whom the ancestors are going to be fetched from.

* `className`: [string](https://create.roblox.com/docs/en-us/luau/strings) - The [Object.ClassName](https://create.roblox.com/docs/en-us/reference/engine/classes/Object#ClassName) of the ancestors to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the `searchObject`'s ancestors.

**Code Example:**
```lua
-- TODO: Make this.
```

----

### getChildrenOfClassRange
Returns an array containing all children of the given `searchObject` of which their [Object.ClassName](https://create.roblox.com/docs/en-us/reference/engine/classes/Object#ClassName) properties are equal to any of values in `classNameRangeTable`.

**Syntax:** `InstanceUtils:getChildrenOfClassRange(searchObject: Instance, classNameRangeTable: {string}) → {Instance}`

**Parameters:**

* `searchObject`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The instance to whom the children are going to be fetched from.

* `classNameRangeTable`: [Array](https://create.roblox.com/docs/luau/tables#arrays) - The individual [Object.ClassName](https://create.roblox.com/docs/en-us/reference/engine/classes/Object#ClassName) values of the children to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the `searchObject`'s children.

**Code Example:**
```lua
-- TODO: Make this.
```

----

### getSiblingsOfClassRange
Returns an array containing all siblings of the given `searchObject` of which their [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) properties are equal to any of values in `classNameRangeTable`.

**Syntax:** `InstanceUtils:getSiblingsOfClassRange(searchObject: Instance, nameRangeTable: {string}) → {Instance}`

**Parameters:**

* `searchObject`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The instance to whom the siblings are going to be fetched from.

* `classNameRangeTable`: [Array](https://create.roblox.com/docs/luau/tables#arrays) - The individual [Object.ClassName](https://create.roblox.com/docs/en-us/reference/engine/classes/Object#ClassName) values of the siblings to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the `searchObject`'s siblings.

**Code Example:**
```lua
-- TODO: Make this.
```

----

### getDescendantsOfClassRange
Returns an array containing all descendants of the given `searchObject` of which their [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) properties are equal to any of values in `classNameRangeTable`.

**Syntax:** `InstanceUtils:getDescendantsOfClassRange(searchObject: Instance, nameRangeTable: {string}) → {Instance}`

**Parameters:**

* `searchObject`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The instance to whom the descendants are going to be fetched from.

* `classNameRangeTable`: [Array](https://create.roblox.com/docs/luau/tables#arrays) - The individual [Object.ClassName](https://create.roblox.com/docs/en-us/reference/engine/classes/Object#ClassName) values of the descendants to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the `searchObject`'s descendants.

**Code Example:**
```lua
-- TODO: Make this.
```

----

### getAncestorsOfClassRange
Returns an array containing all ancestors of the given `searchObject` of which their [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) properties are equal to any of values in `classNameRangeTable`.

**Syntax:** `InstanceUtils:getAncestorsOfClassRange(searchObject: Instance, nameRangeTable: {string}) → {Instance}`

**Parameters:**

* `searchObject`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The instance to whom the ancestors are going to be fetched from.

* `classNameRangeTable`: [Array](https://create.roblox.com/docs/luau/tables#arrays) - The individual [Object.ClassName](https://create.roblox.com/docs/en-us/reference/engine/classes/Object#ClassName) values of the ancestors to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the `searchObject`'s ancestors.

**Code Example:**
```lua
-- TODO: Make this.
```

----

### getChildrenOfNameAndClass
Returns an array containing all children of the given `searchObject` of which their [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) properties are equal to the given `name` and their [Object.ClassName](https://create.roblox.com/docs/en-us/reference/engine/classes/Object#ClassName) properties are equal to the given `className`.

**Syntax:** `InstanceUtils:getChildrenOfNameAndClass(searchObject: Instance, name: string, className: string) → {Instance}`

**Parameters:**

* `searchObject`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The object to whom the children are going to be fetched from.

* `name`: [string](https://create.roblox.com/docs/en-us/luau/strings) - The [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) of the children to be compared to.

* `className`: [string](https://create.roblox.com/docs/en-us/luau/strings) - The [Object.ClassName](https://create.roblox.com/docs/en-us/reference/engine/classes/Object#ClassName) of the children to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the `searchObject`'s children.

**Code Example:**
```lua
-- TODO: Make this.
```

----

### getSiblingsOfNameAndClass
Returns an array containing all siblings of the given `searchObject` of which their [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) properties are equal to the given `name` and their [Object.ClassName](https://create.roblox.com/docs/en-us/reference/engine/classes/Object#ClassName) properties are equal to the given `className`.

**Syntax:** `InstanceUtils:getSiblingsOfNameAndClass(searchObject: Instance, name: string, className: string) → {Instance}`

**Parameters:**

* `searchObject`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The object to whom the siblings are going to be fetched from.

* `name`: [string](https://create.roblox.com/docs/en-us/luau/strings) - The [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) of the siblings to be compared to.

* `className`: [string](https://create.roblox.com/docs/en-us/luau/strings) - The [Object.ClassName](https://create.roblox.com/docs/en-us/reference/engine/classes/Object#ClassName) of the siblings to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the `searchObject`'s siblings.

**Code Example:**
```lua
-- TODO: Make this.
```

----

### getDescendantsOfNameAndClass
Returns an array containing all descendants of the given `searchObject` of which their [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) properties are equal to the given `name` and their [Object.ClassName](https://create.roblox.com/docs/en-us/reference/engine/classes/Object#ClassName) properties are equal to the given `className`.

**Syntax:** `InstanceUtils:getDescendantsOfNameAndClass(searchObject: Instance, name: string, className: string) → {Instance}`

**Parameters:**

* `searchObject`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The object to whom the descendants are going to be fetched from.

* `name`: [string](https://create.roblox.com/docs/en-us/luau/strings) - The [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) of the descendants to be compared to.

* `className`: [string](https://create.roblox.com/docs/en-us/luau/strings) - The [Object.ClassName](https://create.roblox.com/docs/en-us/reference/engine/classes/Object#ClassName) of the descendants to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the `searchObject`'s descendants.

**Code Example:**
```lua
-- TODO: Make this.
```

----

### getAncestorsOfNameAndClass
Returns an array containing all ancestors of the given `searchObject` of which their [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) properties are equal to the given `name` and their [Object.ClassName](https://create.roblox.com/docs/en-us/reference/engine/classes/Object#ClassName) properties are equal to the given `className`.

**Syntax:** `InstanceUtils:getAncestorsOfNameAndClass(searchObject: Instance, name: string, className: string) → {Instance}`

**Parameters:**

* `searchObject`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The object to whom the ancestors are going to be fetched from.

* `name`: [string](https://create.roblox.com/docs/en-us/luau/strings) - The [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) of the ancestors to be compared to.

* `className`: [string](https://create.roblox.com/docs/en-us/luau/strings) - The [Object.ClassName](https://create.roblox.com/docs/en-us/reference/engine/classes/Object#ClassName) of the ancestors to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the `searchObject`'s ancestors.

**Code Example:**
```lua
-- TODO: Make this.
```

----

### getChildrenOfNameRangeAndClassRange
Returns an array containing all children of the given `searchObject` of which their [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) properties are equal to any of the values in `nameRangeTable` and their [Object.ClassName](https://create.roblox.com/docs/en-us/reference/engine/classes/Object#ClassName) properties are equal to any of the values in `classNameRangeTable`.

**Syntax:** `InstanceUtils:getChildrenOfNameRangeAndClassRange(searchObject: Instance, nameRangeTable: {string}, classNameRangeTable: {string}) → {Instance}`

**Parameters:**

* `searchObject`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The instance to whom the children are going to be fetched from.

* `nameRangeTable`: [Array](https://create.roblox.com/docs/luau/tables#arrays) - The individual [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) values of the children to be compared to.

* `classNameRangeTable`: [Array](https://create.roblox.com/docs/luau/tables#arrays) - The individual [Object.ClassName](https://create.roblox.com/docs/en-us/reference/engine/classes/Object#ClassName) values of the children to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the `searchObject`'s children.

**Code Example:**
```lua
-- TODO: Make this.
```

----

### getSiblingsOfNameRangeAndClassRange
Returns an array containing all siblings of the given `searchObject` of which their [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) properties are equal to any of the values in `nameRangeTable` and their [Object.ClassName](https://create.roblox.com/docs/en-us/reference/engine/classes/Object#ClassName) properties are equal to any of the values in `classNameRangeTable`.

**Syntax:** `InstanceUtils:getSiblingsOfNameRangeAndClassRange(searchObject: Instance, nameRangeTable: {string}, classNameRangeTable: {string}) → {Instance}`

**Parameters:**

* `searchObject`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The instance to whom the siblings are going to be fetched from.

* `nameRangeTable`: [Array](https://create.roblox.com/docs/luau/tables#arrays) - The individual [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) values of the siblings to be compared to.

* `classNameRangeTable`: [Array](https://create.roblox.com/docs/luau/tables#arrays) - The individual [Object.ClassName](https://create.roblox.com/docs/en-us/reference/engine/classes/Object#ClassName) values of the siblings to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the `searchObject`'s siblings.

**Code Example:**
```lua
-- TODO: Make this.
```

----

### getDescendantsOfNameRangeAndClassRange
Returns an array containing all descendants of the given `searchObject` of which their [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) properties are equal to any of the values in `nameRangeTable` and their [Object.ClassName](https://create.roblox.com/docs/en-us/reference/engine/classes/Object#ClassName) properties are equal to any of the values in `classNameRangeTable`.

**Syntax:** `InstanceUtils:getDescendantsOfNameRangeAndClassRange(searchObject: Instance, nameRangeTable: {string}, classNameRangeTable: {string}) → {Instance}`

**Parameters:**

* `searchObject`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The instance to whom the descendants are going to be fetched from.

* `nameRangeTable`: [Array](https://create.roblox.com/docs/luau/tables#arrays) - The individual [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) values of the descendants to be compared to.

* `classNameRangeTable`: [Array](https://create.roblox.com/docs/luau/tables#arrays) - The individual [Object.ClassName](https://create.roblox.com/docs/en-us/reference/engine/classes/Object#ClassName) values of the descendants to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the `searchObject`'s descendants.

**Code Example:**
```lua
-- TODO: Make this.
```

----

### getAncestorsOfNameRangeAndClassRange
Returns an array containing all ancestors of the given `searchObject` of which their [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) properties are equal to any of the values in `nameRangeTable` and their [Object.ClassName](https://create.roblox.com/docs/en-us/reference/engine/classes/Object#ClassName) properties are equal to any of the values in `classNameRangeTable`.

**Syntax:** `InstanceUtils:getAncestorsOfNameRangeAndClassRange(searchObject: Instance, nameRangeTable: {string}, classNameRangeTable: {string}) → {Instance}`

**Parameters:**

* `searchObject`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The instance to whom the ancestors are going to be fetched from.

* `nameRangeTable`: [Array](https://create.roblox.com/docs/luau/tables#arrays) - The individual [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) values of the ancestors to be compared to.

* `classNameRangeTable`: [Array](https://create.roblox.com/docs/luau/tables#arrays) - The individual [Object.ClassName](https://create.roblox.com/docs/en-us/reference/engine/classes/Object#ClassName) values of the ancestors to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the `searchObject`'s ancestors.

**Code Example:**
```lua
-- TODO: Make this.
```

----

### getChildrenOfProperties
Returns an array containing all children of the given `searchObject` of which their properties match the given ones from the `propertyTable`.

**Syntax:** `InstanceUtils:getChildrenOfProperties(searchObject: Instance, propertyTable: {[string]: any}) → {Instance}`

**Parameters:**

* `searchObject`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The instance to whom the children are going to be fetched from.

* `propertyTable`: [Array](https://create.roblox.com/docs/luau/tables#arrays) - The individual [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) values of the children to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the `searchObject`'s children.

**Code Example:**
```lua
-- TODO: Make this.
```

----

### getSiblingsOfProperties
Returns an array containing all siblings of the given `searchObject` of which their properties match the given ones from the `propertyTable`.

**Syntax:** `InstanceUtils:getSiblingsOfProperties(searchObject: Instance, propertyTable: {[string]: any}) → {Instance}`

**Parameters:**

* `searchObject`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The instance to whom the siblings are going to be fetched from.

* `propertyTable`: [Array](https://create.roblox.com/docs/luau/tables#arrays) - The individual [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) values of the siblings to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the `searchObject`'s siblings.

**Code Example:**
```lua
-- TODO: Make this.
```

----

### getDescendantsOfProperties
Returns an array containing all descendants of the given `searchObject` of which their properties match the given ones from the `propertyTable`.

**Syntax:** `InstanceUtils:getDescendantsOfProperties(searchObject: Instance, propertyTable: {[string]: any}) → {Instance}`

**Parameters:**

* `searchObject`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The instance to whom the descendants are going to be fetched from.

* `propertyTable`: [Array](https://create.roblox.com/docs/luau/tables#arrays) - The individual [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) values of the descendants to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the `searchObject`'s descendants.

**Code Example:**
```lua
-- TODO: Make this.
```

----

### getAncestorsOfProperties
Returns an array containing all ancestors of the given `searchObject` of which their properties match the given ones from the `propertyTable`.

**Syntax:** `InstanceUtils:getAncestorsOfProperties(searchObject: Instance, propertyTable: {[string]: any}) → {Instance}`

**Parameters:**

* `searchObject`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The instance to whom the ancestors are going to be fetched from.

* `propertyTable`: [Array](https://create.roblox.com/docs/luau/tables#arrays) - The individual [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) values of the ancestors to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the `searchObject`'s ancestors.

**Code Example:**
```lua
-- TODO: Make this.
```

----

### getChildrenOfPropertiesRange
Returns an array containing all children of the given `searchObject` of which their properties match at least one of the given ones from the `propertyRangeTable`.

**Syntax:** `InstanceUtils:getChildrenOfPropertiesRange(searchObject: Instance, propertyRangeTable: {[string]: any}) → {Instance}`

**Parameters:**

* `searchObject`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The instance to whom the children are going to be fetched from.

* `propertyRangeTable`: [Array](https://create.roblox.com/docs/luau/tables#arrays) - The individual [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) values of the children to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the `searchObject`'s children.

**Code Example:**
```lua
-- TODO: Make this.
```

----

### getSiblingsOfPropertiesRange
Returns an array containing all siblings of the given `searchObject` of which their properties match at least one of the given ones from the `propertyRangeTable`.

**Syntax:** `InstanceUtils:getSiblingsOfPropertiesRange(searchObject: Instance, propertyRangeTable: {[string]: any}) → {Instance}`

**Parameters:**

* `searchObject`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The instance to whom the siblings are going to be fetched from.

* `propertyRangeTable`: [Array](https://create.roblox.com/docs/luau/tables#arrays) - The individual [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) values of the siblings to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the `searchObject`'s siblings.

**Code Example:**
```lua
-- TODO: Make this.
```

----

### getDescendantsOfPropertiesRange
Returns an array containing all descendants of the given `searchObject` of which their properties match at least one of the given ones from the `propertyRangeTable`.

**Syntax:** `InstanceUtils:getDescendantsOfPropertiesRange(searchObject: Instance, propertyRangeTable: {[string]: any}) → {Instance}`

**Parameters:**

* `searchObject`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The instance to whom the descendants are going to be fetched from.

* `propertyRangeTable`: [Array](https://create.roblox.com/docs/luau/tables#arrays) - The individual [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) values of the descendants to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the `searchObject`'s descendants.

**Code Example:**
```lua
-- TODO: Make this.
```

----

### getAncestorsOfPropertiesRange
Returns an array containing all ancestors of the given `searchObject` of which their properties match at least one of the given ones from the `propertyRangeTable`.

**Syntax:** `InstanceUtils:getAncestorsOfPropertiesRange(searchObject: Instance, propertyRangeTable: {[string]: any}) → {Instance}`

**Parameters:**

* `searchObject`: [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) - The instance to whom the ancestors are going to be fetched from.

* `propertyRangeTable`: [Array](https://create.roblox.com/docs/luau/tables#arrays) - The individual [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) values of the ancestors to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the `searchObject`'s ancestors.

**Code Example:**
```lua
-- TODO: Make this.
```

----

### getInstancesFromTable
Add desc

**Syntax:** `InstanceUtils:getInstancesFromTable(searchTable: {any}) → {Instance}`

**Parameters:**

* `searchTable`: [table](https://create.roblox.com/docs/luau/tables) - The table of values that will be checked through to retrieve the [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) objects present in the table.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the found instances.

**Code Example:**
```lua
-- TODO: Make this.
```

----

### getInstancesOfNameFromTable
Add desc

**Syntax:** `InstanceUtils:getInstancesOfNameFromTable(searchTable: {any}, name: string) → {Instance}`

**Parameters:**

* `searchTable`: [table](https://create.roblox.com/docs/luau/tables) - The table of values that will be checked through to retrieve the [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) objects present in the table that match the given `name`.

* `name`: [string](https://create.roblox.com/docs/en-us/luau/strings) - The [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) of the found instances to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the found instances.

**Code Example:**
```lua
-- TODO: Make this.
```

----

### getInstancesOfNameRangeFromTable
Add desc

**Syntax:** `InstanceUtils:getInstancesOfNameRangeFromTable(searchTable: {any}, nameRangeTable: {string}) → {Instance}`

**Parameters:**

* `searchTable`: [table](https://create.roblox.com/docs/luau/tables) - The table of values that will be checked through to retrieve the [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) objects present in the table that match at least one of the provided names from the `nameRangeTable`.

* `nameRangeTable`: [Array](https://create.roblox.com/docs/luau/tables#arrays) - The individual [Instance.Name](https://create.roblox.com/docs/en-us/reference/engine/classes/Instance#Name) values of the instances to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the found instances.

**Code Example:**
```lua
-- TODO: Make this.
```

----

### getInstancesOfClassFromTable
Add desc

**Syntax:** `InstanceUtils:getInstancesOfClassFromTable(searchTable: {any}, className: string) → {Instance}`

**Parameters:**

* `searchTable`: [table](https://create.roblox.com/docs/luau/tables) - The table of values that will be checked through to retrieve the [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) objects present in the table that match the given `name`.

* `className`: [string](https://create.roblox.com/docs/en-us/luau/strings) - The [Object.ClassName](https://create.roblox.com/docs/en-us/reference/engine/classes/Object#ClassName) of the instances to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the found instances.

**Code Example:**
```lua
-- TODO: Make this.
```

----

### getInstancesOfClassRangeFromTable
Add desc

**Syntax:** `InstanceUtils:getInstancesOfClassRangeFromTable(searchTable: {any}, classNameRangeTable: {string}) → {Instance}`

**Parameters:**

* `searchTable`: [table](https://create.roblox.com/docs/luau/tables) - The table of values that will be checked through to retrieve the [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) objects present in the table that match at least one of the provided names from the `nameRangeTable`.

* `classNameRangeTable`: [Array](https://create.roblox.com/docs/luau/tables#arrays) - The individual [Object.ClassName](https://create.roblox.com/docs/en-us/reference/engine/classes/Object#ClassName) values of the instances to be compared to.

**Returns:**

* [`Array`](https://create.roblox.com/docs/luau/tables#arrays) - An array containing the found instances.

**Code Example:**
```lua
-- TODO: Make this.
```

----

InstanceUtils:getInstancesOfClassRangeFromTable

InstanceUtils:getInstancesOfNameAndClassFromTable

InstanceUtils:getInstancesOfNameRangeAndClassRangeFromTable

InstanceUtils:getInstancesOfPropertiesFromTable

InstanceUtils:getInstancesOfPropertiesRangeFromTable

InstanceUtils:getInstancesOfPropertiesRangeFromTable
