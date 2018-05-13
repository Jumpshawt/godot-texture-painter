# Godot Texture Painter

This is a prototype for a PBR texture painter in Godot 3.0. It's meant to be mostly a proof-of-concept, to show that it's possible at all - but I might turn it into a full blown application one day (but no promises!).

![Paint](images/demo.gif)

The painting algorithm is GPU-accelerated, so you can paint on extremely large textures with huge brushes on very high poly models without lag.

You can paint albedo, roughness, metalness and emission. Also, you can right click to place decals, and use the slider on the top right to change the brush softness. Other controls are displayed on the GUI.

I'll upload a video soon.

# How it works

The program works using two kinds of textures: `mesh` and `paint` textures. They are organized in the scene tree like this:

![Tree](images/tree.png)

Mesh textures store information about triangle position and normal on a per-pixel basis, which is used as input for the paint shader to do GPU accelerated painting. This already reveals a fundamental limitation of the algorithm, though: since a texture can store only one value per pixel, a texel can only be at 1 point in space at the same time. As such, the algorithm only works for models that have non-overlapping UVs (so every texel appears exactly once on the model). 

Paint textures store the actual texture you see on the model, and it is generated by mixing the output from the paint shader with the previous frame. There are 4 of them: albedo, roughness, metalness and emission. I might make a 5th one, for painting normals, although that will be a little more difficult to implement.

# Limitations/Known Issues
- You can only paint on models that have non-overlapping UVs.
