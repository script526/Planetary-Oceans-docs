# Initial setup

{% hint style="info" %}
Actor that you want to be floating in the ocean should have Static Mesh as a root component.
{% endhint %}

To set up buoyancy on your actor, follow these steps:

1. Add `PlanetaryBuoyancy` component to your Actor blueprint.
2. In the component settings fill the `Buoyancy Points` array. Vector locations it is asking for are in local space (relative to the root). It is recommended to have more than 4 Buoyancy Points for smoother buoyancy simulation.
3. Make the Static Mesh Component you want to float as root component. Static Mesh can have any other components attached to it (meshes, cameras, particles etc.)

{% hint style="info" %}
Static Mesh has to have simple collision added. Polygon count doesn't matter, but the complexity of the collision may affect performance. Make sure, you don't have excessive amount of collision primitives with complex geometry.
{% endhint %}

1. Buoyancy Component will set on the Static Mesh Component `Simulate Physics` to true and `Gravity` to false on BeginPlay. You will see the corresponding warnings in the engine output log. If you'd like to avoid these warnings, set those variables yourself.
2. If your Actor is added to the level, you can navigate to the Primary Ocean category in the component settings and set the PlanetaryOcean to the ocean you'd like this Actor to float on. If not set, the Buoyancy Component will assign the first found APlanetaryOcean in the level on BeginPlay.

{% hint style="info" %}
To change the primary ocean at runtime, use SetPrimaryOcean function that is exposed to blueprint. You may also want to uncheck the`bSearchForPlanetaryOceanOnBeginPlay`since every time you change some component parameter at runtime the component's constructor is called and then the BeginPlay again.
{% endhint %}

1. Now you can hit Play and tweak the buoyancy settings.
