# Transition Planning Workflow

## Before Running

Always use the ROS Humble environment and deactivate Conda before building or running ROS packages.

Example:

```bash
conda deactivate
cd ~/ws_humble
source /opt/ros/humble/setup.bash
source install/setup.bash
```

## Workflow

### 1. Launch RViz and the central planning scene

```bash
ros2 launch master_the_tension_transition_plan central_planning_bringup.launch.py
```

Notes:

- default hardware mode is `mock_components`
- if needed, you can still pass `ros2_control_hardware_type:=isaac`

### 2. Load the online DLO model as piecewise linear markers

Use:

```bash
ros2 launch master_the_tension_transition_plan load_dlo.launch.py
```

### 3. Launch the planner

Use:

```bash
ros2 launch master_the_tension_transition_plan pick_place_demo_dual.launch.py clip_ids:="[6, 7, 8]" exe:=dual_mtc_routing alter_finger_left:=false clip_added_from_blender:=false attach_pull_cable:=true attach_transport_cable:=true
```

When planning for objects added from Blender, set:

```bash
clip_added_from_blender:=true
```

### 4. Load obstacles and clip fixtures

For the plane setup with obstacles:

```bash
ros2 launch master_the_tension_transition_plan load_scene.launch.py \
scene_file:=/home/tp2/ws_humble/scene/trans/trans_env_adapt_z.scene \
mesh_file:=/home/tp2/ws_humble/scene/trans/mesh/qb_board_plane_with_obs_2.stl \
clip_file:=/home/tp2/ws_humble/scene/trans/target_shape_plane_7_clip_qb.scene \
use_qb_board_coordinate:=true \
add_clip_hats:=true
```

For the BMW shape loaded from Blender:

```bash
ros2 launch master_the_tension_transition_plan load_scene.launch.py \
scene_file:=/home/tp2/ws_humble/scene/trans/trans_env_blender_plane.scene \
mesh_file:=/home/tp2/ws_humble/scene/trans/mesh/qb_board_bmw_with_clip_high.stl \
clip_file:=/home/tp2/ws_humble/scene/trans/target_shape_bmw_clip_high_qb.scene \
use_qb_board_coordinate:=true \
add_clip_hats:=false
```

Notes:

- set `use_qb_board_coordinate:=false` when using `_world.scene`
- the launch file defaults use `~/ws_humble/...`, but the explicit examples above keep the original absolute paths for clarity
