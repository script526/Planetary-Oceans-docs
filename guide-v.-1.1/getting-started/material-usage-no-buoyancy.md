# Material usage (no buoyancy)

Assign the `MI_PlanetOcean` to the sphere mesh of your choice or use the `SM_OceanMeshGenerated` mesh. To adjust the polygon density, see [Generating ocean mesh](using-with-static-mesh/generating-ocean-mesh.md).

{% hint style="success" %}
The mesh you'd like to use the material with doesn't have to be a Static Mesh. It can be based on a Procedural or Dynamic Mesh Component, or on some third-party solutions like [Voxel Plugin](using-with-voxel-plugin.md).
{% endhint %}

You have a wide variety of parameters that enable you to achieve the desired style. Here are some features:

* Wave parameters (direction, length, amplitude, steepness etc.)
* Subsurface scattering
* Waves attenuation at the shoreline
* Masking out water
* Waves and beach foam
* Scrolling normals (textures) on top of wave normals

{% hint style="success" %}
Sphere with the ocean material can be moved and rotated at runtime.
{% endhint %}

Utilizing only the material results in a purely visual effect and does not offer [buoyancy](../buoyancy/).

<figure><img src="../../.gitbook/assets/mi.png" alt=""><figcaption></figcaption></figure>
