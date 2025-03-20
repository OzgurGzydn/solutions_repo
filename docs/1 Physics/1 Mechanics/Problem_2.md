# PROBLEM 2

## Motivation
The forced damped pendulum is a captivating example of a physical system with intricate behavior resulting from the interplay of damping, restoring forces, and external driving forces. By introducing both damping and external periodic forcing, the system demonstrates a transition from simple harmonic motion to a rich spectrum of dynamics, including resonance, chaos, and quasiperiodic behavior. These phenomena serve as a foundation for understanding complex real-world systems, such as driven oscillators, climate systems, and mechanical structures under periodic stress.

Adding forcing introduces new parameters, such as the amplitude and frequency of the external force, which significantly affect the pendulum's behavior. By systematically varying these parameters, a diverse class of solutions can be observed, including synchronized oscillations, chaotic motion, and resonance phenomena. These behaviors not only highlight fundamental physics principles but also provide insights into engineering applications such as energy harvesting, vibration isolation, and mechanical resonance.

---

## Task 1: Theoretical Foundation

### Differential Equation
The motion of a forced damped pendulum is governed by the following nonlinear differential equation:

$$
\frac{d^2\theta}{dt^2} + b\frac{d\theta}{dt} + \frac{g}{L}\sin(\theta) = F\cos(\omega t)
$$

Where:
- \(\theta\): Angular displacement (radians)
- \(b\): Damping coefficient (s⁻¹)
- \(g\): Gravitational acceleration (m/s²)
- \(L\): Pendulum length (m)
- \(F\): Driving force amplitude (s⁻²)
- \(\omega\): Driving frequency (rad/s)

### Small-Angle Approximation
For small angles (\(\theta \ll 1\)), \(\sin(\theta) \approx \theta\), simplifying the equation to:

$$
\frac{d^2\theta}{dt^2} + b\frac{d\theta}{dt} + \omega_0^2\theta = F\cos(\omega t)
$$

Where \(\omega_0 = \sqrt{\frac{g}{L}}\) is the natural frequency. This is a linear second-order differential equation with a harmonic forcing term.

### General Solution
The general solution to this differential equation consists of two parts:
1. *Homogeneous solution (transient response):*
   $$
   \theta_h(t) = A e^{-\frac{b}{2}t} \cos(\omega_r t + \phi)
   $$

   where \(\omega_r = \sqrt{\omega_0^2 - \left(\frac{b}{2}\right)^2}\).

2. *Particular solution (steady-state response):*
   $$
   \theta_p(t) = A_p \cos(\omega t - \delta)
   $$

   where
   $$
   A_p = \frac{F}{\sqrt{(\omega_0^2 - \omega^2)^2 + (b\omega)^2}}
   $$

   and
   $$
   \delta = \tan^{-1}\left(\frac{b\omega}{\omega_0^2 - \omega^2}\right).
   $$

### Resonance
Resonance occurs when the driving frequency \(\omega\) approaches the natural frequency \(\omega_0\). For light damping (\(b \ll \omega_0\)), the amplitude \(A_p\) peaks sharply near \(\omega = \omega_0\), amplifying the system's energy significantly.

---

## Task 2: Analysis of Dynamics

### Parameter Effects
- *Damping Coefficient (b):* Higher \(b\) reduces oscillation amplitude and suppresses chaos, stabilizing the system.
- *Driving Amplitude (F):* Larger \(F\) can push the system from periodic to chaotic motion.
- *Driving Frequency (\(\omega\)):* Near \(\omega_0\), resonance amplifies motion; far from \(\omega_0\), the system may exhibit quasiperiodic or chaotic behavior.

### Transition to Chaos
For large \(F\) or specific \(\omega\), the nonlinear term \(\sin(\theta)\) dominates, leading to chaotic motion. This transition is evident in phase portraits and Poincaré sections, where trajectories shift from closed loops (periodic) to scattered points (chaotic).

---

## Task 3: Practical Applications

- *Energy Harvesting:* Oscillatory motion in forced pendulums can be converted to electrical energy.
- *Suspension Bridges:* Damping and forcing model wind-induced vibrations.
- *Oscillating Circuits:* Analogous to driven RLC circuits, where resonance and damping play similar roles.

---

## Task 4: Implementation

Below is a Python script simulating the forced damped pendulum using the 4th-order Runge-Kutta (RK4) method. It includes visualizations of motion, phase portraits, and Poincaré sections.


# Parameters
Gravitational acceleration:

$$ g = 9.81 \text{ m/s}^2 $$

Pendulum length:

$$ L = 1.0 \text{ m} $$

Damping coefficient:

$$ b = 0.5 \text{ s}^{-1} $$

Driving amplitude:

$$ F = 1.2 \text{ s}^{-2} $$

Driving frequency:

$$ \omega = \frac{2}{3} \text{ rad/s} $$

Natural frequency:

$$ \omega_0 = \sqrt{\frac{g}{L}} $$

### Differential Equation

The equation governing the forced damped pendulum is:

$$ \frac{d^2\theta}{dt^2} + b \frac{d\theta}{dt} + \omega_0^2 \sin\theta = F \cos(\omega t) $$

## Differential Equation and Simulation

The forced damped pendulum follows the equation:

$$ \frac{d^2\theta}{dt^2} + b \frac{d\theta}{dt} + \omega_0^2 \sin\theta = F \cos(\omega t) $$

import numpy as np

def pendulum_deriv(state, t, b, omega_0, F, omega):
    """
    Damped forced pendulum differential equation.

   import numpy as np

def pendulum_deriv(state, t, b, omega_0, F, omega):
    """
    Computes the derivatives for the forced damped pendulum.

    Parameters:
        state (tuple): (theta, theta_dot)
        t (float): time
        b (float): damping coefficient
        omega_0 (float): natural frequency
        F (float): forcing amplitude
        omega (float): forcing frequency

    Returns:
        tuple: (dtheta_dt, dtheta_dot_dt)
    """
    theta, theta_dot = state
    dtheta_dt = theta_dot  # Angular velocity
    dtheta_dot_dt = -b * theta_dot - omega_0**2 * np.sin(theta) + F * np.cos(omega * t)
    return dtheta_dt, dtheta_dot_dt

# Example usage (and showcasing the equation):
# The forced damped pendulum follows the equation:
# $$ \frac{d^2\theta}{dt^2} + b \frac{d\theta}{dt} + \omega_0^2 \sin\theta = F \cos(\omega t) $$
# where:
# - theta is the angle of the pendulum
# - b is the damping coefficient
# - omega_0 is the natural frequency
# - F is the forcing amplitude
# - omega is the forcing frequency
# - t is time.

# Example parameters:
b = 0.25
omega_0 = 1.0
F = 0.3
omega = 1.5

# Example initial conditions:
initial_state = (np.pi / 4, 0.0) # (theta, theta_dot)

# Example time:
t = 0.0

# Example derivative calculation:
dtheta_dt, dtheta_dot_dt = pendulum_deriv(initial_state, t, b, omega_0, F, omega)

print(f"dtheta/dt: {dtheta_dt}")
print(f"d^2theta/dt^2: {dtheta_dot_dt}")