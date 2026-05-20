# Master the Tension

This is the repository is for reseach article "Master the Tension: Force-Driven Assembly of Deformable Linear Objects with Environmental Contacts".

This repository contains the two layers
- Planning layer, including Transition Planning, covered by [planning packages](https://github.com/KejiaChen/master_the_tension_transition_plan) and custom [MoveIt 2 Task Constructor package](https://github.com/KejiaChen/moveit_task_constructor)
- Contol layer, including Transport Control and Adaptive Fixing, covered by [control framework for Franka Panda robot](https://github.com/KejiaChen/master_the_tension_mios)


## Planning

### System Requirement
Tested on Ubuntu 22.04 with ROS2 humble.

### Installation
1. Install MoveIt2 humble following [MoveIt2 Documentation](https://moveit.picknik.ai/humble/doc/tutorials/getting_started/getting_started.html)

2. Add custom packages for master the tenstion and build again
```bash
cd ~/ws_moveit2/src
git clone git@github.com:KejiaChen/master_the_tension_transition_plan.git
git clone 
colcon build
```

### Planning Workflow
Follow [this workflow](transition_planning.md) to plan daul-arm collision-free trajectories to transit a DLO segment from one fixture to another.

The planned joint trajectory will be saved locally to 


## Control 
This section includes scirpts to drive the two Franka Panda Robot in the real world to finishe the manipulation task. 
It is built on top of the [mios](https://github.com/KejiaChen/master_the_tension_mios) framework. The workflow incldues 
- transpot control, which maintains a certain tenion on the grasepd DLO while following planned trajectory, 
- and adaptive fixing, which modules stretching and pushing force to achieve a cautious and efficient attachment to the fixture.

### System Requirement
Tested on workstations with Ubuntu 20.04.

### Installtion
```bash
cd <mios_path>
. install.sh
```
Detail

### Workflow
The assembly experiment will be exectued by running ```dual_arm_assembly.py```. It will control two Franka arms to run repeatedly 
- transpot control, by executing the `MoveTrajectoryCartForceFeedback` skill
- adaptive fixing, by executing the `TaxFixClipTelepresence` skill

## Copyright
Copyright (c) 2025 Technical University Munich.

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
