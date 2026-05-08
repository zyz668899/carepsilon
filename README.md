# carepsilon

## Overview
carepsilon is a ROS2-based multi-agent planning and simulation stack for autonomous driving in interactive environments. It includes behavior planning, prediction, simulation, route planning, and vehicle modeling modules, plus integrated launch files for running end-to-end demos.

## Repository Layout
- app/planning_integrated: launch files and integration entry points
- aux_tools: terminal control tool for agent behaviors
- core: planners, prediction, simulators, maps, and vehicle models
- util: planner implementations (AI agent, EUDM, SSC)
- misc/toolchain: assets and tooling

## Requirements
- Ubuntu 22.04
- ROS2 Humble
- System packages:
  - libgoogle-glog-dev libdw-dev libopenblas-dev gfortran
- Python packages:
  - empy pygame

Optional (used by some planners and configs):
- OOQP (QP solver)
- Protobuf (parameter config)

## Build
Assume a standard ROS2 workspace structure.

```bash
source /opt/ros/humble/setup.bash
mkdir -p ~/ws/src
cd ~/ws/src
git clone https://github.com/zyz668899/carepsilon.git
cd ..
colcon build
source install/setup.bash
```

## Run
Run commands from the repository root unless noted.

1. Start RViz:
```bash
cd core/phy_simulator/rviz
ros2 run rviz2 rviz2 --display-config phy_simulator_planning.rviz
```

2. Start planning nodes:
```bash
ros2 launch planning_integrated test_ssc_with_eudm_ros_launch.py
```

3. Start AI agent node:
```bash
ros2 launch ai_agent_planner onlane_ai_agent_launch.py
```

4. Start the simulator (launch last):
```bash
ros2 launch phy_simulator phy_simulator_planning_launch.py
```

5. Start the behavior control UI:
```bash
cd aux_tools/src
python3 terminal_server.py
```

Controls: select an agent in the UI and use W/A/S/D to change its behavior.

## Notes
- If you see missing packages, install the dependencies listed above and rebuild.
- If RViz fails to load, confirm the ROS2 environment is sourced and the display config path is correct.
