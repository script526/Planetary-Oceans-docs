# Using with Static Mesh

Add `BP_PlanetaryOcean` to your level. Optionally, place `BP_Boat` , `BP_FishBoat`, or `BP_Buoy` on the ocean surface, and hit Play. You should immediately see those things floating, regardless of what side of the ocean sphere they are.

`BP_PlanetaryOcean` , by default, uses `SM_OceanMeshGenerated` as a mesh. It has:

* A radius of 30,000 Unreal units (300 m)
* 3,486,252 triangles
* Size of one quad: 78,68 Cm
* Quads per meter:  1,27. Which means, you have 2,54 quads along the height of the character (which is 200 units)

If you'd like to change any of those parameters, see [Generating ocean mesh](generating-ocean-mesh.md).



