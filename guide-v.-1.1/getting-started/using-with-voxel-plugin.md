# Voxel Plugin Integration

{% hint style="danger" %}
Only Voxel Plugin 2.0 versions 340.0, 340.1, and 340.3 are supported. Compatibility with `dev` versions may be possible by replacing outdated nodes in the Voxel Graph.
{% endhint %}

Integration with the Voxel Plugin made as easy as it gets.

1. Create a Voxel Graph with a sphere surface and assign a `MI_PlanetOcean` in the Generate Marching Cube Surface node. Alternatively, you can download a simple graph made for convenience (don't forget to assign the material instance in there).

{% file src="../../.gitbook/assets/VG_OceanSphereSurface.uasset" %}

2. Drag and drop the Voxel Graph to the world. Go to the `BP_PlanetaryOcean` and switch the `MeshMode` to the `VoxelPluginsMesh`.

The integration complete. There a couple things you should be aware of:

* Ocean material uses material collection parameters that are updated from a `BP_PlanetaryOcean`'s parent class `APlanetaryOcean`. This way, all wave parameters are synchronized with the buoyancy system.
* You must make sure that `SphereRadius` in `BP_PlanetaryOcean` matches the radius of the sphere in the Voxel Graph. Otherwise, buoyancy will have issues.
* You don't necessarily have to have a solid sphere in the Voxel Graph. You may remove parts of the sphere using noise that represents your continents, so that the surface appears only where you want it to be. This approach may be used to remove water from the areas below continents, if you'd like to dig in there. The only requirement is, all parts of the surface should match the overall shape of a perfect sphere.

### Fixing WPO in Voxel Plugin in UE 5.3

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption><p>This is how the oceanlooks when WPO doesn't do anything.</p></figcaption></figure>

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

Restart the editor. Now you should see the waves.

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

### Fixing WPO in Voxel Plugin in UE 5.4

{% hint style="danger" %}
If you're using Unreal Engine 5.4, you must make one extra edit (see commit [15c86df](https://github.com/VoxelPlugin/VoxelPlugin/commit/15c86df02b7819b4977da843954fba47f765bf3c)) in addition to the one mentioned above.
{% endhint %}

In the `Voxel/Shaders/VoxelMarchingCubeVertexFactory.ush` on line 145 (considering you have already made the edit above), paste:

```hlsl
#if VOXEL_ENGINE_VERSION >= 504
    Parameters.LWCData = MakeMaterialLWCData(Parameters);
#endif
```
