# Gravitational Dynamics Simulation

## From Keplerian Orbits to Full Three-Body Barycentric Motion

---

## Overview

This notebook explores gravitational dynamics progressively, starting from simplified two-body motion and building up to the full Sun–Earth–Jupiter three-body system using a symplectic Leapfrog (Velocity Verlet) integrator.

The project demonstrates:

* Keplerian motion
* Circular orbit derivation
* Energy conservation properties
* Barycentric dynamics
* Restricted three-body approximation
* Fully interacting three-body dynamics

All realistic simulations use physical SI units.

---

# Development Structure

The notebook is organized into stages of increasing physical realism.

---

## 1️⃣ Dimensionless Kepler Problem (Fixed Central Potential)

* Sun fixed at origin.
* Dimensionless gravitational potential:

$$
\mathbf{a} = -\frac{\mathbf{r}}{|\mathbf{r}|^3}
$$

* Demonstrates:

  * Leapfrog stability
  * Energy conservation
  * Elliptical trajectories

Energy computed as:

$$
E = \frac{1}{2} v^2 - \frac{1}{r}
$$

Purpose: Validate numerical integrator in simplest setting.

---

## 2️⃣ Real Circular Orbit (Sun Fixed)

Using SI units:

$$
v = \sqrt{\frac{G M}{r}}
$$

* Earth initialized in circular orbit.
* Sun fixed at origin.
* Demonstrates analytical circular motion.

Purpose: Verify orbital velocity formula.

---

## 3️⃣ Barycentric Two-Body System (Sun–Earth)

Both bodies move under mutual gravity.

System shifted to center-of-mass frame:

$$
\mathbf{R}_{cm} =
\frac{m_E \mathbf{r}_E}{M + m_E}
$$

Ensures:

$$
\sum m_i \mathbf{v}_i = 0
$$

Demonstrates:

* Solar wobble
* Proper two-body dynamics
* Energy conservation in symplectic scheme

---

## 4️⃣ Natural Orbital Development from Arbitrary Initial Conditions

* Earth initialized with arbitrary position and velocity.
* Orbit emerges naturally from gravitational evolution.
* Demonstrates sensitivity to initial conditions.

Purpose:
Understand how eccentricity and orbital geometry arise dynamically.

---

## 5️⃣ Restricted Three-Body Approximation

* Jupiter forced to move in prescribed circular orbit.
* Earth feels both Sun and Jupiter.
* Jupiter does not feel Earth.

This is a **restricted three-body model**.

Energy is not conserved because:

* Jupiter's motion is externally imposed.

Purpose:
Observe perturbative effects without full mutual interaction.

---

## 6️⃣ Three-Body System (Sun Fixed)

* Earth and Jupiter both move dynamically.
* Sun remains fixed.
* Demonstrates mutual perturbations.

Energy not fully conserved due to artificial Sun constraint.

Purpose:
Illustrate inconsistency of fixing massive body.

---

## 7️⃣ Full Barycentric Three-Body System

All three bodies interact mutually:

$$
\mathbf{a}*i =
\sum*{j \neq i}
G m_j
\frac{\mathbf{r}_j - \mathbf{r}_i}
{|\mathbf{r}_j - \mathbf{r}_i|^3}
$$

System transformed into barycentric frame.

Properties:

* Momentum conserved
* Energy approximately conserved
* Solar barycentric wobble visible
* Jupiter perturbs Earth orbit

Simulation:

* Time step: 1 hour
* Duration: 30 years
* Units: SI

Total energy:

$$
E =
\sum_i \frac{1}{2} m_i v_i^2
----------------------------

\sum_{i<j}
\frac{G m_i m_j}{|\mathbf{r}_i - \mathbf{r}_j|}
$$

---

# Numerical Method

All systems use the Leapfrog (Velocity Verlet) integrator:

$$
\mathbf{v}_{n+1/2}
==================

\mathbf{v}_n
+
\frac{\Delta t}{2}\mathbf{a}_n
$$

$$
\mathbf{r}_{n+1}
================

\mathbf{r}*n
+
\Delta t,\mathbf{v}*{n+1/2}
$$

$$
\mathbf{v}_{n+1}
================

\mathbf{v}*{n+1/2}
+
\frac{\Delta t}{2}\mathbf{a}*{n+1}
$$

Why Leapfrog?

* Second-order accurate
* Time reversible
* Symplectic
* Energy stable over long time scales

---

# Scientific Observations

* Symplectic integration prevents secular energy drift.
* Fixing massive bodies breaks conservation laws.
* Restricted models violate energy conservation.
* Full barycentric dynamics restores physical consistency.
* Jupiter induces measurable perturbations on Earth.

---

# How to Run

```
pip install -r requirements.txt
jupyter notebook
```

Run all cells sequentially.

---


