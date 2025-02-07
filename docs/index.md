Throughout this documentation here, we're going to be using an example Roblox Studio object hierarchy:
```
game      # Class: DataModel
├─ Workspace
│  ├─ Camera      # Class: Camera
│  ├─ Camera2      # Class: Camera
│  │  ├─ SurfaceGui      # Class: Camera
│  │  ├─ SurfaceGui      # Class: BasePart
│  │  ├─ SurfaceGui      # Class: BasePart
│  │  ├─ SomethingElse      # Class: Camera
│  │  │  └─ Bar      # Class: TextLabel
│  │  ├─ ASimpleTruss      # Class: TrussPart
│  │  └─ Foo      # Class: Camera
│  ├─ GreenTheBlaze      # Class: Model
│  ├─ GreenTheBlaze      # Class: Part
│  ├─ FakeCamera      # Class: BasePart
│  ├─ Part      # Class: BasePart
│  ├─ Part      # Class: BasePart
│  ├─ Part1      # Class: BasePart
│  ├─ Part2      # Class: BasePart
│  ├─ Part2      # Class: BasePart
│  ├─ Part2      # Class: Union
│  ├─ Part2      # Class: MeshPart
│  └─ Terrain     # Class: Terrain
└─ Lighting
   ├─ ANormalLight      # Class: PointLight
   ├─ Sky      # Class: Sky
   └─ ANormalLightLol      # Class: MeshPart
```
*Don't mind the weird names LOL.*
**Also, note that the way in which the objects are ordered here is not necessarily compliant with the order that Roblox puts instances in - any outputs in examples are to be in the order from which they are presented in the above. MAKE SURE TO READ THIS OR YOU MAY BE CONFUSED!**

## Miscellanious Functions

### createInstance
[needs doing]

**Syntax:** `InstanceUtils:createInstance(className: Instance, propertiesTable: {any}) → Instance`

**Parameters:**
* `child`: The instance to whom the siblings are going to be searched from.

**Returns:**
* `Array`: An array containing the `child`'s siblings.

**Code Example:**
```lua
local siblingsOfSky = InstanceUtils:getSiblings(game.Lighting.Sky) --> {game.Lighting.ANormalLight, game.Lighting.ANormalLightLol}
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
* `Array`: An array containing the `child`'s siblings.

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
* `Array`: An array containing the `descendant`'s ancestors.

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
* `Array`: An array containing the `parent`'s children.

**Code Example:**
```lua
local childrenOfCamera2 = InstanceUtils:getChildrenOfName(workspace.Camera2, "SurfaceGui") --> {workspace.Camera2.SurfaceGui, workspace.Camera2.SurfaceGui, workspace.Camera2.SurfaceGui}

for _, child in childrenOfCamera2 do
   print(child.Name)
   -- Output:
   --> SurfaceGui (ClassName: Camera)
   --> SurfaceGui (ClassName: BasePart)
   --> SurfaceGui (ClassName: BasePart)
```
----
### getSiblingsOfName
Returns an array containing all siblings of the given `parent` of which their `Object.Name` properties are equal to the given `name`.

**Syntax:** `InstanceUtils:getSiblingsOfName(child: Instance, name: string) → {Instance}`

**Parameters:**
* `sibling`: The instance to whom the siblings are going to be searched from.

**Returns:**
* `Array`: An array containing the `sibling`'s siblings.

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
