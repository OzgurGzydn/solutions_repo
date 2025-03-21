# Problem 3
# Trajectories of a Freely Released Payload Near Earth

## Introduction

When an object is released from a moving rocket near Earth, its trajectory depends on initial conditions and gravitational forces. This scenario presents a rich problem, blending principles of orbital mechanics and numerical methods. Understanding the potential trajectories is vital for space missions, such as deploying payloads or returning objects to Earth.

## Possible Trajectories

The trajectories of a payload released near Earth can be classified into three main types based on the object's energy and velocity:

1. **Elliptical Trajectory**:
   - Occurs when the total mechanical energy of the payload is negative. This trajectory is characteristic of objects in stable orbits around Earth.

2. **Parabolic Trajectory**:
   - Occurs when the total mechanical energy is zero. This trajectory represents the boundary between bound (elliptical) and unbound (hyperbolic) orbits.

3. **Hyperbolic Trajectory**:
   - Occurs when the total mechanical energy is positive. This trajectory indicates that the payload has enough velocity to escape Earth's gravitational influence.

## Numerical Analysis

To compute the path of the payload based on given initial conditions (position, velocity, and altitude), we can use Newton's Law of Gravitation and numerical methods to simulate the motion under Earth's gravity.

### Equations of Motion

The gravitational force acting on the payload can be described by Newton's Law of Gravitation:
$$
F = \frac{GMm}{r^2}
$$
where:
- \( F \) = gravitational force
- \( G \) = gravitational constant (\(6.674 \times 10^{-11} \, \text{m}^3 \text{kg}^{-1} \text{s}^{-2}\))
- \( M \) = mass of the Earth (\(5.972 \times 10^{24} \, \text{kg}\))
- \( m \) = mass of the payload
- \( r \) = distance from the center of the Earth to the payload

The equations of motion can be derived from this force, leading to a system of differential equations that can be solved numerically.

### Python Script

Below is a Python script that simulates the motion of a payload released near Earth, accounting for initial velocities and directions.

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp

# Constants
G = 6.674 * 10**-11  # gravitational constant in m^3 kg^-1 s^-2
M = 5.972 * 10**24   # mass of the Earth in kg
R = 6.371 * 10**6    # radius of the Earth in meters

# Function to compute the derivatives
def derivatives(t, y):
    x, y_pos, vx, vy = y
    r = np.sqrt(x**2 + y_pos**2)  # distance from the center of the Earth
    ax = -G * M * x / r**3  # acceleration in x
    ay = -G * M * y_pos / r**3  # acceleration in y
    return [vx, vy, ax, ay]

# Initial conditions
initial_position = [R + 1000, 0]  # 1000 meters above the Earth's surface
initial_velocity = [0, 500]  # initial velocity in m/s (horizontal)
initial_conditions = initial_position + initial_velocity

# Time span for the simulation
t_span = (0, 200)  # seconds
t_eval = np.linspace(t_span[0], t_span[1], 500)  # time points

# Solve the differential equations
solution = solve_ivp(derivatives, t_span, initial_conditions, t_eval=t_eval)

# Extract the results
x = solution.y[0]
y = solution.y[1]

# Plotting the trajectory
plt.figure(figsize=(10, 6))
plt.plot(x, y, label='Payload Trajectory')
plt.plot(0, 0, 'ro', markersize=10, label='Earth')  # Earth at the origin
plt.xlim(-1.5e7, 1.5e7)
plt.ylim(-1.5e7, 1.5e7)
plt.xlabel('X Position (m)')
plt.ylabel('Y Position (m)')
plt.title('Trajectory of a Freely Released Payload Near Earth')
plt.axhline(0, color='black', lw=0.5, ls='--')
plt.axvline(0, color='black', lw=0.5, ls='--')
plt.grid()
plt.legend()
plt.axis('equal')
plt.show()