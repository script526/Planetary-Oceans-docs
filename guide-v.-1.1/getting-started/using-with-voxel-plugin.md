# Voxel Plugin Integration

{% hint style="danger" %}
Only Voxel Plugin 2.0 versions 340.0, 340.1, and 340.3 are supported. Compatibility with `dev` versions may be possible by replacing outdated nodes in the Voxel Graph.
{% endhint %}

Unfortunately, distribution of some kind of a drag-and-drop solution as a separate Blueprint is hindered by parent class corruption following the pasting or migration of the asset. So, additional steps are necessary to ensure functionality, although the process was made as easy as possible.

Once the Voxel Plugin is installed, download this Voxel Graph asset. You should drag and drop the file from your download folder in Windows Explorer to your project's folder (don't drag it directly to the editor's content folder). You can also do this while the project is open.

{% file src="../../.gitbook/assets/VG_OceanSphereSurface.uasset" %}

This Voxel Graph should look like this:

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

Create a new Blueprint based on `VoxelOceanSurface` class, let's name it `BP_VoxelOceanSurface`. In the Class Defaults search for Tags, add a tag with the name `BP_VoxelOceanSurface`. This tag will allow `BP_PlanetaryOcean` to locate this blueprint in the level (as it is hardcoded there).

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

Add `VoxelComponent` (you may rename it to `OceanSurface` for clarity), and assign the downloaded `VG_OceanSphereSurface` from the first step to the Graph slot.

<div align="left">

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

</div>

In the list of overridable functions there are 4 `BlueprintImplementable` functions derived from the VoxelOceanSurface class:

<div align="left">

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

</div>

You need to implement them like so:

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

Add both `BP_PlanetaryOcean` and the newly created `BP_VoxelOceanSurface` to the level. In the `BP_PlanetaryOcean` settings, switch `MeshMode` to `VoxelPluginsMesh`.

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

Now you should see the Voxel sphere instead of a static mesh, but there are no waves yet. The reason is, in versions 340.0, 340.1, and 340.3 of the Voxel Plugin, the material's world position offset doesn't work. To fix that, go to `Voxel/Shaders/VoxelMarchingCubeVertexFactory.ush` file and on line 135, replace (you don't have to close the editor):

```hlsl
FMaterialVertexParameters Parameters = (FMaterialVertexParameters)0;
```

with

```hlsl
#if VOXEL_ENGINE_VERSION >= 503
	FMaterialVertexParameters Parameters = MakeInitializedMaterialVertexParameters();
#else
	FMaterialVertexParameters Parameters = (FMaterialVertexParameters)0;
#endif
```

{% hint style="info" %}
This edit was taken from the commit [3b7b6b6](https://github.com/VoxelPlugin/VoxelPlugin/commit/3b7b6b6d3ce16eb555bbc757dd50128298223d4f) in the Voxel Plugin's dev branch.
{% endhint %}

Now you should see the waves initialized with the default wave parameters in the Voxel Graph (with the same values as in the default `BP_PlanetaryOcean`). If you have changed some parameters in the Blueprint before switching `MeshMode` to `VoxelPluginsMesh`, you have to tweak them again to trigger the update. Changing a parameter in the Blueprint updates the same parameter in the Voxel Graph, one at a time.
