# Voxel Plugin Integration

{% hint style="danger" %}
Only Voxel Plugin 2.0 versions 340.0, 340.1 340.3 are supported. It might work with dev versions with minimal node replacement in the Voxel Graph.
{% endhint %}

Unfortunately, distributing drag-and-drop type of solution as a separate Blueprint doesn't work due to parent class corruption after pasting/migrating the asset. So, some additional steps are required to make everything work, but the process was simplified as much as possible.

Once the Voxel Plugin is installed, download this Voxel Graph, You should drag and drop the file in the Windows explorer from your download folder to your project Content folder, you can do this also while the project is opened.

FILE HERE

This Voxel Graph should look like this:

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

Create a new Blueprint named something like BP\_VoxelOceanSurface and open it.

In the Class Defaults search for Tags, add a tag with the name  BP\_VoxelOceanSurface. By this tag BP\_PlanetaryOcean will find this blueprint in the level.

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

Add VoxelComponent (you may rename it to OceanSurface for clarity), and assign the downloaded in the first step VG\_OceanSphereSurface to the Graph slot.

<div align="left">

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

</div>

In the list of overridable functions there are 4 functions you need to override like so:

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

Add to the level both BP\_PlanetaryOcean and newly created BP\_VoxelOceanSurface. In the BP\_PlaneratyOcean settings switch MeshMode to VoxelPluginsMesh

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

Now you should see the Voxel sphere instead of a static mesh, but there're no waves yet. The reason is, in versions 340.0, 340.1 and 340.3 of the Voxel Plugin world position offset didn't work in the material. To fix that, go to VoxelPlugin/Shaders/VoxelMarchingCubeVertexFactory.ush file and on the line 135 replace (you don't have to close the editor)

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

Now you should see the waves, initialized with the default wave parameters in the Voxel Graph (with the same values as in the default BP\_PlanetaryOcean). If you have changed some parameters in the BP before switching MeshMode to VoxelPluginsMesh, you have to tweak them again to trigger the update. Changing some parameter in the BP updates the same parameter in the Voxel Graph.

{% hint style="warning" %}
If you're trying to apply this guide to one of the dev versions of the Voxel Plugin, you might need to replace some nodes in the Voxel Graph to make it work.
{% endhint %}
