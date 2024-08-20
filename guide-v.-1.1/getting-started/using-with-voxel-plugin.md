# Voxel Plugin Integration

{% hint style="danger" %}
Only Voxel Plugin 2.0 versions 340.0, 340.1, and 340.3 are supported. Compatibility with `dev` versions may be possible by replacing outdated nodes in the Voxel Graph.
{% endhint %}

Unfortunately, distribution of some kind of a drag-and-drop solution as a separate Blueprint is hindered by parent class corruption following the pasting or migration of the asset. So, additional steps are necessary to ensure functionality, although the process was made as easy as possible.

### Preparations

Once the Voxel Plugin is installed, download this Voxel Graph asset. It makes a sphere surface and has all necessary wave parameters that will be updated by the ocean BP. You should drag and drop the file from your download folder in Windows Explorer to your project's folder (dragging it directly to the editor's content folder will not work). You can also do this while the project is open.

{% file src="../../.gitbook/assets/VG_OceanSphereSurface (3).uasset" %}

This Voxel Graph should look like this:

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

### Creating a BP for Voxel integration

Create a new Blueprint based on `VoxelOceanSurface` class, let's name it `BP_VoxelOceanSurface`.

Add `VoxelComponent` (you may rename it to `OceanSurface` for clarity), and assign the downloaded earlier `VG_OceanSphereSurface` to the Graph slot.

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

Now you should see the Voxel sphere instead of a static mesh, but there's no displacement yet (only the normals).

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

### Fixing WPO in Voxel Plugin

In versions 340.0, 340.1, and 340.3 of the Voxel Plugin, the material's world position offset doesn't work. To fix that, go to `Voxel/Shaders/VoxelMarchingCubeVertexFactory.ush` file and on line 135, replace:

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

Restart the editor. Now you should see the waves initialized with the default wave parameters in the Voxel Graph (with the same values as in the default `BP_PlanetaryOcean`).

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

If you have changed some parameters in the Blueprint before switching `MeshMode` to `VoxelPluginsMesh`, you have to tweak them again to trigger the update. Changing a parameter in the Blueprint updates the same parameter in the Voxel Graph, one at a time.

### If you're on UE 5.4

{% hint style="danger" %}
If you're using Unreal Engine 5.4, you must make one extra edit (see commit [15c86df](https://github.com/VoxelPlugin/VoxelPlugin/commit/15c86df02b7819b4977da843954fba47f765bf3c)) in addition to the one mentioned above.
{% endhint %}

In the `Voxel/Shaders/VoxelMarchingCubeVertexFactory.ush` on line 145 (considering you have already made the edit above), paste:

```
#if VOXEL_ENGINE_VERSION >= 504
    Parameters.LWCData = MakeMaterialLWCData(Parameters);
#endif
```
