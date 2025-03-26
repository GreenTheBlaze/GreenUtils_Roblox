# GreenPathfindingService

!!! info "In Development"

    This service is currently under development and may not work as intended, if at all.

Like the default [PathfindingService](https://create.roblox.com/docs/reference/engine/classes/PathfindingService) that Roblox uses, **GreenPathfindingService** is used to find logical paths between two points so that characters can move to different destinations without coming in contact with obstacles. However, this service differentiates from its inspirator, allowing for more advanced path generation in the air, as well as on ground. The service also takes into account obstacles and gap distances, which [PathfindingService](https://create.roblox.com/docs/reference/engine/classes/PathfindingService) fails to do in some circumstances.


## Summary
### Properties


### Methods
## createPath
Creates a `GreenPath` class based on the provided `agentParameters`. Valid keys and values in the agentParameters table are as follows:
| Method              | Type    | Default                       | Description |
| :------------------ | :------ | :---- | ----------- |
| **agentRadius**     | integer | 2     | Determines the minimum amount of horizontal space required for empty space to be considered traversable.
| **agentHeight**     | integer | 5     | Determines the minimum amount of vertical space required for empty space to be considered traversable.
| **agentCanJump**    | boolean | true  | Determines whether jumping during pathfinding is allowed.
| **agentCanClimb**   | boolean | false | Determines whether climbing [`TrussParts`](https://create.roblox.com/docs/reference/engine/classes/TrussPart) during pathfinding is allowed.
| **agentIsGrounded** | boolean | true  | 
| **waypointSpacing** | number  | 4     | Determines the spacing between intermediate waypoints in path. |
| **costs**           | table   | {}    | Table of materials or defined [`PathfindingModifiers`](https://create.roblox.com/docs/reference/engine/classes/PathfindingModifier) and their "cost" for traversal. Useful for making the agent prefer certain materials/regions over others. See [here](https://create.roblox.com/docs/characters/pathfinding#pathfinding-modifiers) for details. |
### Events

## Properties

## Methods

## Events

----

## [Ignore] Discard Reference
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
