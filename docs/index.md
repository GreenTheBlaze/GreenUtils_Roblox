Greetings!

If you're one of Green's friends or people authorized to use GreenUtils and you'd like to understand more on how to use the Roblox package, you've come to the right place!

This documentation serves as a knowledge base for our package, everything here is kept up-to-date and should be referred to over anything else!

Now, before we begin, first I'd like to introduce you to our example instance hierarchy tree which will be referred to throughout every API page you'll come across...
```
.
├─ Workspace           -  Object 1 - ClassName: Workspace
│  ├─ Camera           -  Object 2 - ClassName: Camera
│  ├─ Terrain          -  Object 3 - ClassName: Terrain
│  ├─ SpawnLocation    -  Object 4 - ClassName: SpawnLocation
│  │  └─ Decal         -  Object 5 - ClassName: Decal
│  ├─ Part1            -  Object 6 - ClassName: MeshPart
│  ├─ Part1            -  Object 7 - ClassName: UnionOperation
│  ├─ Part1            -  Object 8 - ClassName: UnionOperation
│  ├─ Part1            -  Object 9 - ClassName: UnionOperation
│  ├─ BasePart         -  Object 10 - ClassName: Part
│  ├─ Part             -  Object 11 - ClassName: Part
│  ├─ Part             -  Object 12 - ClassName: Part
│  ├─ Part1            -  Object 13 - ClassName: Part
│  │  └─ Gui           -  Object 14 - ClassName: Decal
│  │     └─ Text       -  Object 15 - ClassName: Decal
│  ├─ Part1            -  Object 16 - ClassName: Part
│  ├─ Part1            -  Object 17 - ClassName: Part
│  │  └─ FooGui        -  Object 18 - ClassName: Decal
│  │     └─ TextLabel  -  Object 19 - ClassName: Decal
│  ├─ Part1            -  Object 20 - ClassName: Part
│  ├─ Part1            -  Object 21 - ClassName: Part
│  │  └─ Gui           -  Object 22 - ClassName: Decal
│  │     └─ Label      -  Object 23 - ClassName: Decal
│  ├─ Part1            -  Object 24 - ClassName: TrussPart
│  ├─ Part1            -  Object 25 - ClassName: SurfaceGui
│  └─ Part1            -  Object 26 - ClassName: SurfaceGui
│  └─ Part1            -  Object 27 - ClassName: BillboardGui
└─ Lighting            -  Object 28 - ClassName: Lighting
   ├─ ALight           -  Object 29 - ClassName: PointLight
   ├─ PointLight       -  Object 30 - ClassName: Sky
   ├─ PointLight       -  Object 31 - ClassName: Sky
   └─ PointLight2      -  Object 32 - ClassName: MeshPart
```

You can also download the place file if needed from [here](https://github.com/GreenTheBlaze/GreenUtils_Roblox/blob/main/dependencies/GreenUtilsHierarchyReference.rbxl) that the instances were originally arranged in!
