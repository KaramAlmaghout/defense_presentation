# Speaker notes — 21:30 target

These notes correspond to the 26 main slides in main.pdf. The seven backup
slides are untimed. The planned delivery is 21 minutes 30 seconds, leaving
3 minutes 30 seconds in a 25-minute slot for pauses and interruptions.

Do not read equations or tables line by line. On a method slide, explain the
physical meaning of the notation. On a result slide, state the protocol first,
then the quantitative finding and its limitation.

| # | Slide | Target | Cumulative |
|---:|---|---:|---:|
| 1 | Title | 0:25 | 0:25 |
| 2 | Relevance and applications | 0:50 | 1:15 |
| 3 | Existing approaches and gap | 0:55 | 2:10 |
| 4 | Goal and objectives | 0:55 | 3:05 |
| 5 | Research structure | 0:50 | 3:55 |
| 6 | Provisions presented for defense | 1:00 | 4:55 |
| 7 | Ordered state and VFPs | 0:55 | 5:50 |
| 8 | Complete mass--spring model | 0:55 | 6:45 |
| 9 | Intermediary-shape planning | 0:55 | 7:40 |
| 10 | Diminishing-rigidity Jacobian | 0:55 | 8:35 |
| 11 | Constrained dual-arm control | 0:55 | 9:30 |
| 12 | Simulation design | 0:45 | 10:15 |
| 13 | Simulation results for \(N\) | 0:50 | 11:05 |
| 14 | ALI step-size study | 0:50 | 11:55 |
| 15 | Physical setup | 0:40 | 12:35 |
| 16 | Physical U/L/S/M results | 0:55 | 13:30 |
| 17 | Opposite-concavity results | 0:55 | 14:25 |
| 18 | GCR problem formulation | 0:50 | 15:15 |
| 19 | GCR numerical method | 0:55 | 16:10 |
| 20 | Complete-motion validation | 0:55 | 17:05 |
| 21 | Representative computed routes | 0:35 | 17:40 |
| 22 | GCR benchmark results | 1:00 | 18:40 |
| 23 | MuJoCo execution | 0:55 | 19:35 |
| 24 | Main scientific results | 1:00 | 20:35 |
| 25 | Publications and implementation | 0:40 | 21:15 |
| 26 | Closing | 0:15 | 21:30 |

## Slide-by-slide talk track

### 1. Title — 0:25

Introduce the dissertation title, specialty, candidate, and scientific
supervisor. State that the work addresses two connected problems: large planar
shape change and routing of a complete cable among obstacles.

### 2. Relevance and applications — 0:50

Define a deformable linear object before using DLO. Use the two applications to
motivate the work. Explain the three difficulties: the state is distributed,
material parameters vary, and safe gripper paths do not guarantee safe cable
motion. Finish with the research question shown on the slide.

### 3. Existing approaches and the research gap — 0:55

Compare model-free, model-based, and data-driven control. Their limitations are
respectively local range, parameter identification, and dependence on training
data. For routing, emphasize that valid endpoint shapes can still be connected
by an invalid swept motion. The dissertation addresses these limitations as one
connected sequence of models and numerical methods.

### 4. Goal, object, subject, and objectives — 0:55

State the formal goal. Distinguish the object—planar dual-arm manipulation—from
the subject—the developed models and numerical methods. Use the five objectives
as the roadmap and avoid implementation detail here.

### 5. Research structure — 0:50

Read the matrix vertically, as in the supplied defense template. For each
research branch identify the problem, prior limitation, dissertation result,
and verification. Chapter 2 provides perception and the evaluation model;
Chapter 3 develops and physically evaluates shape control; Chapter 4 develops
and computationally evaluates global routing.

### 6. Provisions presented for defense — 1:00

State the four provisions concisely: ordered image-based reconstruction;
large-deformation control using ALI and the diminishing-rigidity Jacobian;
global routing with swept-transition validation; and software-supported
verification. The rest of the presentation follows this order.

### 7. Ordered DLO state and Virtual Feature Points — 0:55

Expand Virtual Feature Points and RGB. The cable itself has no markers; one
gripper is marked only to fix the traversal origin. Explain segmentation,
thinning, and circular-mask traversal. The output is an ordered set of
approximately equidistant points used in the physical controller.

### 8. Mass--spring DLO model — 0:55

This is the complete DLO simulation model, not only a stretching equation.
Linear springs preserve length, torsion springs represent bending, and damping
suppresses relative oscillation. Point to the complete force balance and the
two energies. Mention backward Euler and the conjugate-gradient solve. State
that this is an evaluation model, not a controller input or separate novelty.

### 9. Intermediary-shape planning — 0:55

Expand LI, ILI, and ALI. LI can terminate without a feasible path. ILI restores
segment length but cannot reverse concavity. ALI translates the most displaced
reference point, interpolates segment angles, and reconstructs in both
directions with fixed length. The two signed recurrences are the key.

### 10. Diminishing-rigidity Jacobian — 0:55

Use the dissertation’s exact name. Define stretched distance \(D\), current
distance \(d\), and influence \(\mu\). A taut cable section transmits
end-effector motion strongly; slack reduces the influence. Each point is
assigned to the nearest end-effector and the point Jacobians are assembled.
This is a geometric slack approximation, not a measured stiffness law.

### 11. Constrained dual-arm shape control — 0:55

At each ALI stage, use the current observed point state and the next reference
profile. Update the Jacobian, calculate bounded end-effector motion, observe
the new cable geometry, and repeat. The online controller needs geometry and
robot poses, not identified cable stiffness or damping.

### 12. Shape-control simulation design — 0:45

Show the U, L, S, and M transformation families. Two cable models and four
values of \(N\) produce 32 tasks. Define the strict condition
\(e_{\mathrm{mean}}<0.01L\). The iteration cap is \(20K\), where \(K\) is the
number of ALI profiles—not 20,000 iterations.

### 13. Simulation results for point count \(N\) — 0:50

The top row shows the original simulated final-shape figures. All 32 tasks
completed. Distinguish completion from strict convergence: one \(N=10\) run,
two \(N=12\) runs, and three \(N=14\) runs reached the iteration cap before the
strict condition. Do not say all 32 converged.

### 14. ALI step-size study — 0:50

Use the original error and iteration plots. The tested range is 1–100 mm.
The dissertation reports 10–50 mm as the effective operating range. Above
50 mm, larger changes between reference profiles increased errors and failures.
Present this as a tested range, not a universal optimum.

### 15. Physical experimental setup — 0:40

Identify the two KUKA LBR iiwa robots, top-view Intel RealSense D435, and the
350 mm by 9 mm cable. The physical state uses ten VFPs. These are planar,
obstacle-free shape-control experiments.

### 16. U/L/S/M physical results — 0:55

The top row contains the real final overlays. Compare matched simulation and
physical values using the exact dissertation table. Physical mean errors are
11.7, 10.9, 10.6, and 5.2 mm for U, L, S, and M. All four physical targets were
reproduced.

### 17. Opposite-concavity experiments — 0:55

The images show real initial, intermediary, and target profiles. ALI passes
through a stretched configuration rather than remaining trapped in the
original concavity. Report mean errors 12.4, 9.0, 8.1, and 4.5 mm. Qualify the
claim as all four tested physical transformations.

### 18. Global Cable Routing problem formulation — 0:50

Expand Global Cable Routing. A configuration is the complete ordered cable
chain in \(2N\)-dimensional space, not a gripper pose. Static admissibility
checks workspace, full cable segments, and length bounds. A route also requires
valid ordered motion between every pair of neighboring configurations.

### 19. Global Cable Routing numerical method — 0:55

Explain the three source figures: guided sampling, Artificial Potential Field
bias, and projected relaxation. Then summarize the two-tree search and
shortcutting. APF only biases candidate generation; bidirectional tree search
provides global exploration.

### 20. Complete-motion validation — 0:55

Contrast the accepted and rejected transitions. For each cable segment, test
the convex swept polygon. Also preserve endpoint-axis consistency so robot
assignments cannot flip, and apply optional end-effector constraints. This is a
geometric transition test, not a dynamic cable simulation.

### 21. Representative computed routes — 0:35

Use the four scenarios to show that the method handles different geometric
structures: open motion, a narrow gate, a trap, and an L-corridor. Each figure
shows the start, goal, and shortcut-refined ordered sequence.

### 22. GCR benchmark results — 1:00

Start with the protocol: ten scenarios, 1,000 independent random seeds per
scenario, single-threaded C++. Every one of the 10,000 tested runs returned a
path satisfying the stated static and transition predicates. Mean time ranged
from 0.008 to 1.306 seconds. Shortcutting reduced 13–25 raw configurations to
3–9. This is empirical evidence for the tested cases, not a completeness proof.

### 23. MuJoCo execution — 0:55

Expand root-mean-square error before using RMSE. Two UR10 manipulators execute
the planned endpoint waypoints for a 0.27 m cable. Across ten scenarios, RMSE
is 1.60–4.66 mm and maximum point error is 2.31–7.81 mm. End with the boundary:
this is physics-based simulation; no physical GCR experiment is claimed.

### 24. Main scientific results — 1:00

Read the table by objective, not by column. Connect each result to its evidence
and established scope. Emphasize the progression from perception to
large-deformation control and then global routing. Close with the explicit
future-work items rather than extending the demonstrated claims to 3D,
occlusion, frictional contact, or physical routing.

### 25. Publications and implementation — 0:40

State the publication count and indexing. Do not read every title aloud.
Identify the implemented VFP/control, MATLAB, C++, and MuJoCo software, and
mention Russian Science Foundation support.

### 26. Closing — 0:15

Thank the committee and invite questions. Leave this slide visible.

## Backup guide

| ID | Slide | Use when asked about |
|---:|---|---|
| A1 | Abbreviations | DLO, RGB, VFPs, LI, ILI, ALI, GCR, APF, or RMSE |
| A2 | Mass--spring forces | length, bending, damping, or integration |
| A3 | ALI construction | \(\sigma\), \(K\), \(\lambda\), or the two recurrences |
| A4 | Physical error histories | convergence during U/L/S/M experiments |
| A5 | GCR admissibility | static constraints, clearance, or predicate \(\Gamma\) |
| A6 | Complete GCR benchmark | fastest time, iterations, or all seven metrics |
| A7 | Opposite-concavity finals | final overlays for the four physical cases |
