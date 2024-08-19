# Generating ocean mesh

{% hint style="danger" %}
Make sure the `BP_PlanetaryOcean` is placed in the world zero. You can move it to the desired location once mesh generation is done. Otherwise, there will be artifacts on the generated mesh.
{% endhint %}

Hit `Edit Mode` in `BP_PlanetaryOcean`. Change `Sphere Radius`, `Steps` and `Tessellation Level`. In the `Outliner` you should see the `BP_OceanMeshGenerator` spawned, it levarages the Dynamic Mesh Component to generate the mesh and bake it into the static mesh.

<div align="left">

<figure><img src="../../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

</div>

Different values give different polygon density.

<div align="left">

<figure><img src="../../../.gitbook/assets/image (4) (1).png" alt=""><figcaption><p>Tesselation Level: 10</p></figcaption></figure>

</div>

<div align="left">

<figure><img src="../../../.gitbook/assets/image (5) (1).png" alt=""><figcaption><p>Tesselation Level: 2</p></figcaption></figure>

</div>

Every time you change any of those values, the resulting mesh stats is printed on the screen. If it's not there, look at the output log.

<div align="left">

<figure><img src="../../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

</div>

Once you're satisfied with the values, hit `Generate Static Mesh` and give it some time to generate, it might freeze the editor. At this point, the wireframe dynamic mesh you see on the screen is being baked into the static mesh, assigned to the `Generated Static Mesh` slot of the ocean BP. This will override the default `SM_OceanMeshGenerated`, but you may replace it with a different mesh before hitting `Generate Static Mesh`, or before entering the `Edit Mode`.

Once the generation is finished, the wireframe dynamic mesh is removed from the level, and you should now see the ocean.

{% hint style="warning" %}
The more triangle count you have, the more expensive it gets for the GPU. The vertex shader calculates waves for every vertex, so you should have as few vertices as possible.&#x20;
{% endhint %}

The current limitation of this approach is that you can't get a large ocean sphere with enough polygon density to make visually acceptable waves. In the next big update, there will be a dynamic LOD system (a quadtree) that will allow you to have an ocean sphere of any size without significant performance impact. Meanwhile, some users leverage Voxel Plugin's mesh, that has an octree LOD system that is dynamically updated.&#x20;
