# Buoyancy

PlanetaryBuoyancy component should be attached to an Actor to make it float. This component calculates the height below (or above water) on the CPU for specified array of BuoyancyPoints. Based on this data, it apply forces to BuoyancyPoints. It also has built-in gravity.

PlanetaryOcean blueprint makes sure to sync wave parameters between the ocean Dynamic Material Instance and the PlanetaryBuoyancy, so that the buoyancy system always gets the same wave parameter values as the material.

