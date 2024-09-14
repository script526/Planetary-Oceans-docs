# Generating ocean mesh

{% hint style="danger" %}
Ensure that the `BP_PlanetaryOcean` is placed in world zero. Following the completion of mesh generation, it can be relocated to the preferred location. Generating mesh outside of world zero may result in artifacts appearing on the generated mesh.
{% endhint %}

Press the `Edit Mode` button in the `BP_PlanetaryOcean`. This will spawn the `BP_OceanMeshGenerator`  that utilizes the Dynamic Mesh Component to create the mesh and bake it into a Static Mesh. Adjust the `Sphere Radius`, `Steps`, and `Tessellation Level` in the `BP_PlanetaryOcean`.

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

Whenever you modify any of these values, the corresponding mesh stats are displayed on the screen. If not, it is printed in the output log.

<div align="left">

<figure><img src="../../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

</div>

Once the desired values have been set, click on the `Generate Static Mesh` button and give it some time, as it may cause the editor to freeze.

At this stage, the wireframe dynamic mesh visible on the screen is currently being baked into the Static Mesh. It is then assigned to the `Generated Static Mesh` slot within in the ocean BP.

This action will override the default `SM_OceanMeshGenerated`, however, you have the option to substitute it with an alternative mesh prior to pressing the `Generate Static Mesh` button or before entering `Edit Mode`.

Once the generation is finished, the wireframe dynamic mesh is removed from the level, and you should now see the ocean.

{% hint style="warning" %}
The more triangle count you have, the more expensive it gets for the GPU. The vertex shader calculates waves for every vertex, so you should have as few vertices as possible.&#x20;
{% endhint %}

The current limitation of this approach is the inability to achieve a large ocean sphere with sufficient polygon density to produce visually acceptable waves. In the next major update, a dynamic Level of Detail (LOD) system in the form of a quadtree will be implemented, enabling users to create ocean spheres of any size without experiencing any significant performance impact.

Meanwhile, some users are [utilizing](../voxel-plugin-integration.md) the Voxel Plugin's mesh, which features an octree LOD system that is dynamically updated at runtime.
