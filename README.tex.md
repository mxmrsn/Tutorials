# Tutorials for Steerable Needle Project

1. [x] Rigid Registration, Meshlab, and Slicer
2. [ ] Building a 6DOF Needle
3. [ ] Building a 5DOF Needle
4. [ ] Designing Lasercut Tube Designs
    - [ ] NIH Flexure Hinge Needle
    - [ ] Notched Wrists
5. [ ] Needle Model and Simulation
6. [ ] Sliding Mode Control of Needles
7. [ ] Electronics Swap Overview


### Rigid Point-Based Registration Solves:

$\min_{T \in SE(3)} \sum_{i=1}^{N} \hspace{1mm} \rVert Tp^{m_i} - p^{s_i} \lVert^2$

### Iterative Closest Point (ICP) Registration Solves:

$\min_{T \in SE(3), C} \sum_{i=1}^{N_s} \sum_{j=1}^{N_m} C_{ij} \hspace{1mm} \lVert Tp^{m_j} - p^{s_i} \rVert^2$
