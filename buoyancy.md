# Buoyancy

PlanetaryBuoyancy component should be attached to an Actor to make it float. This component calculates the height below (or above water) on the CPU for specified array of BuoyancyPoints. Based on this data, it apply forces to BuoyancyPoints. It also has built-in gravity.

PlanetaryOcean blueprint makes sure to sync wave parameters between the ocean Dynamic Material Instance and the PlanetaryBuoyancy, so that the buoyancy system always gets the same wave parameter values as the material.

{% hint style="info" %}
Requirements

* Actor that you want to be floating in the ocean should have Static Mesh as a root component.
* Static Mesh has to have `Simulate Physics` set to true, `Gravity` set to false. If any of these values are different, the Buoyancy Component will set them on `BeginPlay`.
{% endhint %}
