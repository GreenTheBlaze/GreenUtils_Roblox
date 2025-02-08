Greetings!

If you're one of Green's friends or people authorized to use GreenUtils and you'd like to understand more on how to use the Roblox package, you've come to the right place!

This documentation serves as a knowledge base for our package, everything here is kept up-to-date and should be referred to over anything else!

Now, before we begin, first I'd like to introduce you to our example instance hierarchy tree which will be referred to throughout every API page you'll come across:
```
.
├─ Workspace           # Object 1 - ClassName: Workspace
│  ├─ Camera           # Object 2 - ClassName: Camera
│  ├─ Terrain          # Object 3 - ClassName: Terrain
│  ├─ SpawnLocation    # Object 4 - ClassName: SpawnLocation
│  │  └─ Decal         # Object 5 - ClassName: Decal
│  ├─ Part1            # Object 6 - ClassName: MeshPart; BrickColor: Really red
│  ├─ Part1            # Object 7 - ClassName: UnionOperation; BrickColor: Really red
│  ├─ Part1            # Object 8 - ClassName: UnionOperation; BrickColor: Lime green
│  ├─ Part1            # Object 9 - ClassName: UnionOperation; BrickColor: Really red
│  ├─ Baseplate        # Object 10 - ClassName: Part; BrickColor: Dark grey metallic
│  │  └─ Texture       # Object 11 - ClassName: Texture
│  ├─ Part             # Object 12 - ClassName: Part
│  ├─ Part             # Object 13 - ClassName: Part
│  ├─ Part1            # Object 14 - ClassName: Part
│  │  └─ Gui           # Object 15 - ClassName: SurfaceGui
│  │     └─ Text       # Object 16 - ClassName: TextLabel
│  ├─ Part1            # Object 17 - ClassName: Part
│  ├─ Part1            # Object 18 - ClassName: Part
│  │  └─ FooGui        # Object 19 - ClassName: SurfaceGui
│  │     └─ TextLabel  # Object 20 - ClassName: TextLabel
│  ├─ Part1            # Object 21 - ClassName: Part; BrickColor: Really red
│  ├─ Part1            # Object 22 - ClassName: Part
│  │  └─ Gui           # Object 23 - ClassName: SurfaceGui
│  │     └─ Label      # Object 24 - ClassName: TextLabel
│  ├─ Part1            # Object 25 - ClassName: TrussPart
│  ├─ Part1            # Object 26 - ClassName: BillboardGui
│  └─ Part1            # Object 27 - ClassName: SurfaceGui
│  └─ Part1            # Object 28 - ClassName: SurfaceGui
└─ Lighting            # Object 29 - ClassName: Lighting
   ├─ ALight           # Object 30 - ClassName: SurfaceLight
   ├─ PointLight       # Object 31 - ClassName: PointLight
   ├─ PointLight       # Object 32 - ClassName: Part
   └─ PointLight1      # Object 33 - ClassName: Part
```

Here's some additional info you may need to know about the way I've structured this before we continue:

* The default `BrickColor` for `BasePart` instances if not mentioned is **Medium stone grey**.

* All examples of code within the API sheets and anything relating to indexing of the hierarchy should relate to how it's been structured above, NOT how Roblox chooses to output results in Studio. The reason for this is that, Roblox is really weird about object finding, e.g., if I want to print out what `workspace.Part1.ClassName` is, on here it might look output "MeshPart" (Object 6), but on Roblox, it may have looked up differently. Unfortunately I cannot resolve this on the place file provided, so this will have to remain the same...

You can also download the place file if needed from [here](https://github.com/GreenTheBlaze/GreenUtils_Roblox/blob/main/dependencies/GreenUtilsHierarchyReference.rbxl) that the instances were originally arranged in!
