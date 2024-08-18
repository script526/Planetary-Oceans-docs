---
coverY: 0
layout:
  cover:
    visible: false
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Overview

<figure><img src=".gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

{% hint style="danger" %}
The plugin is targeted at Unreal Engine versions 5.3 and 5.4.
{% endhint %}

The Unreal engine plugin offers an ocean material with Gerstner waves for a sphere.&#x20;

It can be used either on a highly subdivided sphere (such a sphere made in 3d modeling software is included in the plugin), or in any other mesh with a quadtree/octree system offered by other plugins.&#x20;

The only requirement to any procedural mesh is that it should support world position offset.

{% embed url="https://www.unrealengine.com/marketplace/en-US/product/planetary-oceans" %}

#### Technical Details

Features:

* Gerstner waves on a sphere
* Can be moved and rotated at runtime
* Any amount of oceans in the level
* Waves foam, beach foam
* Subsurface scattering
* Distance field based waves attenuation (to flatten the ocean on the shore)
* Texture based normals on top of wave normals

\


Planned features:

* Ocean quadtree (LOD) system
* Buoyancy system
* Wave presets blending
* Custom physically based atmosphere (any amount in the level)
* Network replication

FAQ: [Discord](https://discord.com/channels/1224220810110308415/1224221149731491892)

Support: [Discord](https://discord.gg/SvHcuCcjMX)
