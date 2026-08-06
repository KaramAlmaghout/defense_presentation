# Speaker notes — 23:45 target

These notes correspond to the 27-slide main defense in `main.pdf`. The five appendix
slides are untimed and intended for committee questions. The planned delivery is
23 minutes 45 seconds, leaving approximately 1.25 minutes within a 25-minute slot for
pauses and transitions.

| # | Slide | Target | Cumulative |
|---:|---|---:|---:|
| 1 | Title | 0:25 | 0:25 |
| 2 | Relevance | 0:55 | 1:20 |
| 3 | Problem formulation | 1:05 | 2:25 |
| 4 | Research methodology | 0:55 | 3:20 |
| 5 | Goal and objectives | 0:55 | 4:15 |
| 6 | Problem setup | 0:55 | 5:10 |
| 7 | DLO representation: Ordered state | 0:55 | 6:05 |
| 8 | DLO perception: VFP reconstruction | 0:55 | 7:00 |
| 9 | DLO model | 0:45 | 7:45 |
| 10 | DLO planning: Interpolation methods | 0:55 | 8:40 |
| 11 | DLO planning: Angular–linear interpolation | 1:00 | 9:40 |
| 12 | DLO control: Architecture | 0:55 | 10:35 |
| 13 | DLO control: Geometric Jacobian | 1:00 | 11:35 |
| 14 | DLO control: Experimental setup | 0:45 | 12:20 |
| 15 | DLO control: Results | 0:55 | 13:15 |
| 16 | DLO control: Concavity reversal | 0:55 | 14:10 |
| 17 | DLO routing: Problem formulation | 1:00 | 15:10 |
| 18 | DLO routing: Candidate generation | 0:55 | 16:05 |
| 19 | DLO routing: Transition admissibility | 1:05 | 17:10 |
| 20 | DLO routing: GCR algorithm | 0:55 | 18:05 |
| 21 | DLO routing: Computational results | 1:00 | 19:05 |
| 22 | DLO routing: Simulation validation | 0:55 | 20:00 |
| 23 | Principal statements of the thesis | 1:10 | 21:10 |
| 24 | Scientific and practical significance | 0:55 | 22:05 |
| 25 | Principal scientific results | 0:40 | 22:45 |
| 26 | Publications and conferences | 0:45 | 23:30 |
| 27 | Questions | 0:15 | 23:45 |

## Slide-by-slide talk track

### 1. Title — 0:25

Good afternoon. I present my dissertation on mathematical modeling and motion planning
for robotic manipulation of deformable linear objects, prepared under specialty 1.2.2.
The defense is organized around the scientific problem, five novelty results, four
principal statements of the thesis, and their verification.

### 2. Relevance — 0:55

Deformable linear objects occur in cable assembly, hose routing, medical procedures,
and related manipulation tasks. Their state is distributed along the complete object;
their mechanics and contact conditions vary; and collision freedom must hold for the
cable, not only for its grippers. The central difficulty addressed by the dissertation
is the transition from local shape correction to large, obstacle-constrained
deformation.

### 3. Problem formulation — 1:05

Read the diagram by rows, not as a processing pipeline. The formal problem is planar
dual-arm DLO manipulation under large deformation and workspace obstacles without prior
identification of dynamic or material parameters. Existing approaches have distinct
limitations in reconstruction, shape control, and motion planning. Chapters 2–4 answer
these limitations with the ordered VFP state, ALI with the geometric Jacobian and
constrained control, and GCR with transition-admissibility tests. The three columns are
independent; no perception-to-GCR data flow is implied.

### 4. Research methodology — 0:55

The dissertation contains two separate methodological branches. In Chapters 2–3,
top-view RGB data are transformed into VFPs; a prescribed target is connected by ALI;
and the geometric Jacobian with constrained optimization produces robot motion. In
Chapter 4, prescribed start and goal cable configurations together with known obstacles
are inputs to GCR. The routing study does not use the perception pipeline.

### 5. Goal and objectives — 0:55

State the formal goal nearly verbatim: to develop a system of mathematical models and
effective numerical methods for dual-arm shape control and routing under large
deformations and obstacles, without prior identification of dynamic or material
parameters. Identify the object and subject of research, then use the five objectives
as the roadmap for the technical part of the defense.

### 6. Problem setup — 0:55

Separate the two formal problems. Shape control maps an observed current shape and a
prescribed target to bounded dual-arm motions through admissible intermediary shapes.
Global routing maps prescribed start and goal configurations plus a known obstacle map
to an ordered sequence whose states and swept transitions are admissible. Both use the
planar quasi-static and endpoint-grasp assumptions. Do not introduce the VFP contribution
on this slide.

### 7. DLO representation: Ordered state — 0:55

Introduce only the finite-dimensional state: the point order, approximate spacing, and
pointwise correspondence with the target. Its role is to convert distributed cable
geometry into a state compatible with the subsequent methods. The reconstruction method
and its scientific-result statement follow on slide 8. Do not imply that VFP images are
an input to GCR.

### 8. DLO perception: VFP reconstruction — 0:55

Explain the method before stating the result. The cable image is segmented, reduced to
a one-pixel centerline, and traversed with a circular mask; one marked gripper fixes the
starting end. The output is an ordered, approximately equidistant VFP set. Then state
Scientific Result 1: image-based reconstruction of a marker-free planar cable state that
is directly compatible with the developed discrete planning and control models.
Transition: after establishing the measured state, introduce the numerical DLO model
used to evaluate the planning and control methods.

### 9. DLO model — 0:45

The discrete mass–spring system combines linear springs for segment length, torsional
springs for bending, and damping. Backward Euler integration and a conjugate-gradient
update support repeated numerical experiments. This model is a validation instrument,
not a claimed novelty; the feedback controller uses observed geometry and does not
identify cable stiffness or damping. Transition: with the state and evaluation model
established, turn to construction of the intermediary deformation path.

### 10. DLO planning: Interpolation methods — 0:55

Pointwise linear interpolation can contract the discretized cable, while incremental
linear interpolation limits individual steps but can stagnate or fail during concavity
changes. ALI changes the interpolation coordinates: it combines translation of an
anchor point with interpolation of segment angles. The improvement is structural, not
merely a change of a tuning parameter.

### 11. DLO planning: Angular–linear interpolation — 1:00

Scientific Result 2 is the ALI method. Select the point with maximum required
displacement as the anchor, interpolate its position and all segment angles, and
reconstruct the chain forward and backward. Every reconstruction increment has the
nominal segment length; therefore length preservation is built into the construction.
This also permits transitions between configurations of opposite concavity. Transition:
ALI produces target shapes; the next question is how the robots track them.

### 12. DLO control: Architecture — 0:55

ALI determines a sequence of local target shapes, not robot velocities. At every stage,
a new image updates the VFP state, the shape error is formed, and constrained
optimization computes bounded gripper velocities using the current geometric Jacobian.
Read the single closed loop from left to right. The stage policy above it advances the
ALI target only after the prescribed error condition is satisfied and terminates at
the final stage.

### 13. DLO control: Geometric Jacobian — 1:00

Scientific Result 3 is the analytical diminishing-rigidity Jacobian and its use in
constrained control. The geometric weight approaches one for a taut cable portion and
decreases as slack increases. This maps both gripper velocities to point velocities
using observed geometry, without identified stiffness, damping, or learned dynamics.
The optimization minimizes the predicted shape error subject to this mapping and robot
velocity bounds.

### 14. DLO control: Experimental setup — 0:45

Verification has two levels: MATLAB parameter studies over cable lengths, point counts,
and ALI steps, followed by physical closed-loop tests using two KUKA LBR iiwa robots and
a RealSense camera. The real-world system is implemented in C++ with ROS communication
and robot-control nodes. The same geometry-based controller is transferred from
simulation to hardware without cable-parameter identification.

### 15. DLO control: Results — 0:55

For the U, L, S, and M targets, physical mean final error ranges from 5.2 to 11.7 mm.
All 32 parameter combinations completed the manipulation task, although six reached the
iteration limit before satisfying the stricter convergence criterion. The experimentally
supported ALI step interval for the tested systems is 10–50 mm.

### 16. DLO control: Concavity reversal — 0:55

Opposite-concavity transformations are the strongest large-deformation test. ALI passes
through an extended configuration while preserving nominal segment length, and the
physical closed loop completes all four transformations. The corresponding mean final
errors are 12.4, 9.0, 8.1, and 4.5 mm. Transition: this completes obstacle-free shape
control; the next section extends the problem to global routing among obstacles.

### 17. DLO routing: Problem formulation — 1:00

A cable configuration is a point in a (2N)-dimensional configuration space. Static
admissibility requires free space, prescribed segment length, and obstacle clearance.
These conditions are insufficient on their own: each neighboring pair of route states
must also admit a collision-free deformation. This edge condition distinguishes the
formulation from planning only isolated collision-free snapshots.

### 18. DLO routing: Candidate generation — 0:55

GCR combines goal-biased, tree-biased, and broad sampling. A whole-cable artificial
potential field biases a candidate configuration; projected relaxation then restores
local length, clearance, and elasticity constraints. Relate each panel to its displayed
formula: the mixture probabilities, the APF gradient update, and the reference-based
segment/curvature objective. The potential field is one candidate-generation operation
within the global search, not the global planner itself.

### 19. DLO routing: Transition admissibility — 1:05

Endpoint configurations may both be collision-free while the swept cable intersects an
obstacle. For every pair of corresponding segments, a convex swept polygon is tested
against the obstacle set. The complete ordered-edge predicate additionally enforces
material-point order and endpoint feasibility. It is applied during parent selection,
tree connection, and route refinement.

### 20. DLO routing: GCR algorithm — 0:55

Scientific Result 4 is the GCR configuration-space formulation and algorithm. Two trees
grow from the prescribed start and goal. Candidates pass sampling, whole-cable bias,
relaxation, and ordered transition checks; the connected path is oriented and shortcut
only under the same edge predicate and route-cost condition. The contribution is the
ordered composition of these operations for complete-cable routing. Transition: having
defined the complete algorithm, evaluate its repeatability, cost, and route refinement.

### 21. DLO routing: Computational results — 1:00

Begin with the benchmark design: ten planar scenarios and 1,000 independent seeds per
scenario. Use the selected table rows to compare Scenario 3, the easiest case, with Scenario 4,
the most constrained case, and Scenarios 1 and 10. Across 1,000 random seeds per
scenario, all 10,000 tested runs satisfied the specified static and ordered-transition
predicates. Mean single-threaded planning time is 0.008–1.306 s, and refinement reduces
13–25 raw configurations to 3–9. The 100% value is empirical, not a universal theorem.

### 22. DLO routing: Simulation validation — 0:55

Scientific Result 5 concerns implementation and verification. GCR produces complete
cable configurations, whose endpoints drive two UR10 robots through quasi-static
waypoints in MuJoCo. Compare the illustrated executions for Scenarios 1 and 7 and then
use the complete two-panel validation table. Across ten scenarios, final-shape RMSE is
1.60–4.66 mm and maximum pointwise error is 2.31–7.81 mm for the modeled 0.27 m cable.
This is independent physics-based simulation; physical GCR experiments are outside the
dissertation scope. Transition: with both research branches verified, synthesize the
principal statements and significance of the thesis.

### 23. Principal statements of the thesis — 1:10

Present the four integrated statements: ordered DLO-state reconstruction; ALI and the
geometric Jacobian with constrained large-deformation control; transition-admissible
global routing of the complete ordered DLO; and software with computational, physical,
and physics-simulation verification. Distinguish these four statements from the five
individual scientific novelty results and state the validation boundary in Statement IV.

### 24. Scientific and practical significance — 0:55

The theoretical significance is the coherent finite-dimensional representation,
length-feasible interpolation, geometry-based local mapping, and transition-level route
admissibility. The practical significance is a parameter-identification-free methodology
and research software. Reliability follows from mathematical construction, parameter
studies, repeated randomized experiments, physical verification of shape control,
independent simulation of GCR, and peer-reviewed dissemination. Keep the stated scope
explicit.

### 25. Principal scientific results — 0:40

Conclude with four integrated findings: the ordered finite-dimensional observed state;
large-deformation planning and control without cable-parameter identification;
transition-admissible global routing; and software-supported computational, physical,
and simulation verification. Together, these constitute mathematical models, effective
numerical methods, and problem-oriented software within specialty 1.2.2.

### 26. Publications and conferences — 0:45

The five complete citations are generated from the dissertation BibTeX records in a
compact author--title--venue format, with the candidate's name emphasized: four
works indexed by Scopus and one article in a journal included in the Russian Higher
Attestation Commission list. Distinguish the three journal articles from the two
conference-proceedings papers, then identify the three international conferences at
which the results were presented. The research was conducted within RSF project
No. 22-41-02006.

### 27. Questions — 0:15

Thank the committee for its attention and invite questions.
