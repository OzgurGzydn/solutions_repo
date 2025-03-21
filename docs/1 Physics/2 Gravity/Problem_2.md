# Problem 2
## Escape Velocities and Cosmic Velocities

## Motivation
Escape velocity is the minimum speed required for an object to break free from a celestial body's gravitational influence without further propulsion. Expanding on this, the first, second, and third cosmic velocities define the thresholds for stable orbits, escaping a planet, and leaving a star system. These velocities are fundamental for space exploration, enabling satellite launches, interplanetary travel, and potential interstellar missions.

## Definitions
1. **First Cosmic Velocity (Orbital Velocity)**
   - The velocity required to maintain a stable circular orbit around a celestial body.
   - Given by:
     $ v_1 = \sqrt{\frac{GM}{r}} $

2. **Second Cosmic Velocity (Escape Velocity)**
   - The velocity needed to escape a celestial body's gravitational pull.
   - Derived from energy conservation:
     $ v_2 = \sqrt{2 \frac{GM}{r}} = \sqrt{2} v_1 $

3. **Third Cosmic Velocity (Interstellar Escape Velocity)**
   - The velocity required to leave a star system, overcoming the gravitational pull of both the planet and the star.
   - Dependent on the Sun’s influence at planetary distances:
     $ v_3 = \sqrt{2} \cdot v_{escape, planet} + v_{orbit, star} $

## Python Simulation
The following Python script calculates and visualizes these velocities for Earth, Mars, and Jupiter.
```

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.constants import G

# Constants
bodies = {
    "Earth": {"mass": 5.972e24, "radius": 6.371e6},
    "Mars": {"mass": 6.417e23, "radius": 3.389e6},
    "Jupiter": {"mass": 1.898e27, "radius": 6.9911e7},
}

# Compute velocities
velocities = {}
for body, data in bodies.items():
    M, R = data["mass"], data["radius"]
    v1 = np.sqrt(G * M / R)  # First Cosmic Velocity
    v2 = np.sqrt(2) * v1      # Second Cosmic Velocity
    v3 = np.sqrt(2) * v2      # Approximate Third Cosmic Velocity
    velocities[body] = (v1, v2, v3)

# Plot results
labels = list(bodies.keys())
x = np.arange(len(labels))
v1_vals, v2_vals, v3_vals = zip(*velocities.values())

plt.figure(figsize=(10, 6))
plt.bar(x - 0.2, v1_vals, 0.2, label="First Cosmic Velocity")
plt.bar(x, v2_vals, 0.2, label="Second Cosmic Velocity")
plt.bar(x + 0.2, v3_vals, 0.2, label="Third Cosmic Velocity")
plt.xticks(x, labels)
plt.ylabel("Velocity (m/s)")
plt.title("Cosmic Velocities for Different Planets")
plt.legend()
plt.grid(True, linestyle="--", alpha=0.6)
plt.show()
```

```markdown
## Discussion
- **First Cosmic Velocity** determines whether an object can stay in orbit around a planet.
- **Second Cosmic Velocity** is crucial for missions leaving planetary surfaces.
- **Third Cosmic Velocity** is necessary for interstellar travel and escaping the Sun's gravity.
- These calculations are vital for spacecraft trajectory planning and deep-space exploration.

## Conclusion
Understanding cosmic velocities is essential for space exploration. From launching satellites to interplanetary and interstellar travel, these velocities define the fundamental thresholds required to move