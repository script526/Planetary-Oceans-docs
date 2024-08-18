# Using with Static Mesh

Add `BP_PlanetaryOcean` to your level. Optionally, place `BP_Boat` , `BP_FishBoat`, or `BP_Buoy` on the ocean surface, and hit `Play`. You should immediately observe these objects floating, regardless of their placement on the ocean sphere.

`BP_PlanetaryOcean` utilizes the `SM_OceanMeshGenerated` as its default mesh. It includes:

* A radius of 30,000 Unreal units (300 m).
* 3,486,252 triangles.
* The size of one quad is 78.68 cm.
* This gives you 1.27 quads per meter. Another words, that there are 2.54 quads along the height of the character, that is 200 units.

If you wish to modify any of these parameters, see Generating ocean mesh.
