Greetings!

If you're one of Green's friends or people authorized to use GreenUtils and you'd like to understand more on how to use the Roblox package, you've come to the right place!

This documentation serves as a knowledge base for our package, everything here is kept up-to-date and should be referred to over anything else!

Now, before we begin, first I'd like to introduce you to our example instance hierarchy tree which will be referred to throughout every API page you'll come across:
```
game      # Class: DataModel
├─ Workspace
│  ├─ Camera      # Class: Camera
│  ├─ Camera2      # Class: Camera
│  │  ├─ FakeThing1      # Class: Camera
│  │  ├─ FakeThing1      # Class: Part
│  │  ├─ FakeThing1      # Class: Part
│  │  ├─ SomethingElse      # Class: Camera
│  │  │  └─ Bar      # Class: TextLabel
│  │  ├─ ASimpleTruss      # Class: TrussPart
│  │  └─ Foo      # Class: Camera
│  ├─ GreenTheBlaze      # Class: Model
│  ├─ GreenTheBlaze      # Class: Part
│  ├─ FakeCamera      # Class: BasePart
│  ├─ Part      # Class: Part
│  ├─ Part      # Class: Part
│  ├─ Part1      # Class: Part
│  ├─ Part2      # Class: Part
│  ├─ Part2      # Class: Part
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
