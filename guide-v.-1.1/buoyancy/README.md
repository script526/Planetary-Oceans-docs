# Buoyancy

`PlanetaryBuoyancy` component must be attached to an Actor to enable floating. This component computes the depth below (or above) water for a specified array of `BuoyancyPoints` on the CPU. Using this data, it applies forces to the BuoyancyPoints. It also includes built-in gravity.

`PlanetaryOcean` blueprint synchronizes wave parameters between the ocean Dynamic Material Instance and the `PlanetaryBuoyancy` to ensure consistent values for the buoyancy system.

