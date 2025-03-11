# 5. 3D & Digital Twin Simulation

## 5.1 Gazebo (Robotics & AI Simulation)

### Overview
Gazebo is an advanced open-source 3D robotics simulator that enables accurate simulation of robots in complex indoor and outdoor environments. It features a robust physics engine, high-quality graphics, and programmatic and graphical interfaces for developing and testing robotics algorithms.

### Prerequisites
* **Operating Systems**: 
  - **Recommended**: Ubuntu 20.04 LTS or 22.04 LTS
  - **Supported**: Debian, Fedora, Arch Linux, and other Linux distributions
  - **Limited Support**: macOS (via Docker or source build)
  - **Experimental**: Windows (via WSL2)
* **Dependencies**: 
  - ROS (Robot Operating System) integration optional but recommended
  - OpenGL-compatible graphics drivers
  - CMake, Git, and build essentials
* **Minimum System Requirements**: 
  - **RAM**: 4GB
  - **Storage**: 10GB free disk space
  - **Processor**: Quad-core CPU at 2.0GHz+
  - **Graphics**: OpenGL 3.3+ compatible GPU with 1GB VRAM
* **Optimum System Requirements**: 
  - **RAM**: 16GB+
  - **Storage**: 20GB+ SSD storage
  - **Processor**: Octa-core CPU at 3.0GHz+
  - **Graphics**: Dedicated GPU with 4GB+ VRAM, CUDA or OpenCL support for physics acceleration

### Installation Methods

#### Method 1: Standard Package Installation (Ubuntu)

```bash
# Update package lists
sudo apt update

# Install Gazebo
sudo apt install gazebo

# For the latest stable version (Gazebo 11 as of this writing)
sudo apt install gazebo11

# Additional development packages
sudo apt install libgazebo11-dev
```

#### Method 2: Installation with ROS Integration

```bash
# For ROS Noetic (Ubuntu 20.04)
sudo apt install ros-noetic-gazebo-ros-pkgs ros-noetic-gazebo-ros-control

# For ROS Foxy (Ubuntu 20.04) or Humble (Ubuntu 22.04)
sudo apt install ros-foxy-gazebo-ros-pkgs
# or
sudo apt install ros-humble-gazebo-ros-pkgs
```

#### Method 3: Docker Installation (Cross-Platform)

```bash
# Pull the Gazebo Docker image
docker pull osrf/gazebo:latest

# Run Gazebo in a container with GUI support
docker run -it --privileged \
  --env="DISPLAY=$DISPLAY" \
  --env="QT_X11_NO_MITSHM=1" \
  --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" \
  osrf/gazebo:latest gazebo
```

#### Method 4: Source Installation (Advanced Users)

```bash
# Install dependencies
sudo apt install build-essential cmake git libboost-all-dev \
  libtinyxml-dev libxml2-dev libqt5core5a libqt5gui5 libqt5widgets5 \
  libprotobuf-dev protobuf-compiler libprotoc-dev libfreeimage-dev \
  libcurl4-openssl-dev libtinyxml2-dev libgts-dev libignition-math6-dev

# Clone the repository
git clone https://github.com/osrf/gazebo.git

# Build Gazebo
cd gazebo
mkdir build && cd build
cmake ..
make -j$(nproc)
sudo make install
```

### Verification and First Launch

After installation, verify Gazebo works correctly:

```bash
# Launch Gazebo with an empty world
gazebo

# Or with a specific world file
gazebo worlds/pioneer2dx.world
```

### Core Features

#### Physics Simulation
- **Multiple Physics Engines**: ODE (default), Bullet, Simbody, DART
- **Rigid Body Dynamics**: Accurate simulation of joints, contacts, and friction
- **Sensor Simulation**: Cameras, LiDAR, IMU, depth sensors, GPS, etc.
- **Real-time Performance**: Optimized for real-time robotics simulation

#### Graphics and Visualization
- **OGRE Graphics Engine**: High-quality rendering of complex environments
- **Material System**: PBR (Physically Based Rendering) materials support
- **Dynamic Lighting**: Shadows, ambient occlusion, and lighting effects
- **Camera Views**: Multiple viewpoints and camera controls

#### Modeling and Environment Creation
- **Model Database**: Large collection of pre-built robot and environment models
- **Model Editor**: GUI tools for creating and modifying models
- **SDF Format**: Simulation Description Format for defining robots and environments
- **URDF Support**: Universal Robot Description Format compatibility
- **World Editor**: Tools for building complex simulation environments

#### Programming and Integration
- **C++ API**: Comprehensive API for programmatic control
- **Python Bindings**: Python interface for scripting and control
- **ROS Integration**: Seamless connection to Robot Operating System
- **Plugin Architecture**: Extensible system for custom functionality
- **TCP/IP Transport**: Network interface for distributed simulation

### Advanced Usage

#### Keyboard Shortcuts
- **Space**: Play/pause simulation
- **Ctrl+R**: Reset world
- **Ctrl+S**: Save world
- **Tab**: Cycle through models
- **~**: Show/hide console
- **Left-click + Drag**: Rotate camera
- **Shift + Left-click + Drag**: Pan camera
- **Scroll Wheel**: Zoom camera

#### Custom World Creation

```xml
<?xml version="1.0" ?>
<sdf version="1.6">
  <world name="custom_world">
    <include>
      <uri>model://sun</uri>
    </include>
    <include>
      <uri>model://ground_plane</uri>
    </include>
    <!-- Add a simple robot -->
    <include>
      <uri>model://pioneer2dx</uri>
      <pose>0 0 0.5 0 0 0</pose>
    </include>
    <!-- Add custom objects -->
    <model name="box">
      <pose>2 0 0.5 0 0 0</pose>
      <link name="link">
        <collision name="collision">
          <geometry>
            <box>
              <size>1 1 1</size>
            </box>
          </geometry>
        </collision>
        <visual name="visual">
          <geometry>
            <box>
              <size>1 1 1</size>
            </box>
          </geometry>
        </visual>
      </link>
    </model>
  </world>
</sdf>
```

Save this to a file named `custom_world.world` and launch with:

```bash
gazebo custom_world.world
```

#### Basic Plugin Development in C++

```cpp
#include <gazebo/gazebo.hh>
#include <gazebo/physics/physics.hh>

namespace gazebo {
  class HelloWorldPlugin : public WorldPlugin {
    public: 
      void Load(physics::WorldPtr _world, sdf::ElementPtr _sdf) {
        // Plugin initialization code
        printf("Hello World from Gazebo plugin!\n");
        
        // Access simulation time
        common::Time sim_time = _world->SimTime();
        printf("Simulation time: %f\n", sim_time.Double());
        
        // Create an update event connection
        this->updateConnection = event::Events::ConnectWorldUpdateBegin(
          std::bind(&HelloWorldPlugin::OnUpdate, this, std::placeholders::_1));
      }
      
      void OnUpdate(const common::UpdateInfo & _info) {
        // Code to run on every simulation step
      }
      
    private:
      event::ConnectionPtr updateConnection;
  };
  
  // Register this plugin with the simulator
  GZ_REGISTER_WORLD_PLUGIN(HelloWorldPlugin)
}
```

#### ROS Integration Example

```python
#!/usr/bin/env python3

import rospy
from geometry_msgs.msg import Twist
from sensor_msgs.msg import LaserScan

class GazeboRobotController:
    def __init__(self):
        rospy.init_node('gazebo_robot_controller')
        
        # Subscribe to laser scan data
        self.laser_sub = rospy.Subscriber('/scan', LaserScan, self.laser_callback)
        
        # Publisher to control robot
        self.cmd_vel_pub = rospy.Publisher('/cmd_vel', Twist, queue_size=10)
        
        self.rate = rospy.Rate(10)  # 10 Hz
        self.twist = Twist()
        
    def laser_callback(self, data):
        # Simple obstacle avoidance behavior
        if min(data.ranges[270:450]) < 1.0:  # If obstacle in front
            # Turn left
            self.twist.linear.x = 0.1
            self.twist.angular.z = 0.5
        else:
            # Move forward
            self.twist.linear.x = 0.5
            self.twist.angular.z = 0.0
    
    def run(self):
        while not rospy.is_shutdown():
            # Publish velocity commands
            self.cmd_vel_pub.publish(self.twist)
            self.rate.sleep()

if __name__ == '__main__':
    try:
        controller = GazeboRobotController()
        controller.run()
    except rospy.ROSInterruptException:
        pass
```

### Common Use Cases and Applications

#### Robotics Research and Development
- **Algorithm Testing**: Develop and test navigation, manipulation, and perception algorithms
- **Hardware Validation**: Validate robot designs before physical prototyping
- **Sensor Simulation**: Test sensor configurations and fusion algorithms
- **Control Systems**: Develop and tune control systems for robotic platforms

#### Industrial Digital Twins
- **Production Line Simulation**: Model and optimize manufacturing processes
- **Layout Planning**: Test facility layouts and material flow
- **Process Optimization**: Identify bottlenecks and optimize workflows
- **Training**: Train operators on virtual replicas of real systems

#### Autonomous Vehicles
- **Scenario Testing**: Create complex traffic and environmental scenarios
- **Sensor Configuration**: Optimize placement and selection of sensors
- **Decision System Validation**: Test autonomous decision-making systems
- **Edge Case Coverage**: Simulate rare but critical scenarios

#### Education and Training
- **Robotics Courses**: Hands-on learning without physical hardware
- **Competition Preparation**: Practice for robotics competitions
- **Visualization**: Demonstrate robotics concepts and algorithms
- **Remote Learning**: Enable robotics education without physical access to labs

### Performance Optimization Tips

1. **Graphics Settings**: Reduce rendering quality for better simulation performance
   ```bash
   # Launch Gazebo with reduced graphics settings
   GAZEBO_GRAPHICS=0 gazebo
   ```

2. **Physics Engine Selection**: Choose the appropriate physics engine for your needs
   ```bash
   # Launch with the DART physics engine
   gazebo --physics=dart
   ```

3. **Real-time Factor**: Adjust simulation speed for faster-than-realtime simulation
   ```bash
   # Set real-time factor via command line
   gazebo -u --physics=ode -e bullet
   ```

4. **Model Complexity**: Simplify collision meshes and visual geometries
5. **Simulation Step Size**: Adjust step size for trade-off between accuracy and speed
6. **Multithreading**: Enable physics engine parallel execution where supported

### Troubleshooting Common Issues

#### Issue: Gazebo crashes on startup
**Solution**: Check graphics drivers and try with reduced graphics settings:
```bash
LIBGL_ALWAYS_SOFTWARE=1 gazebo
```

#### Issue: Models appear black or with incorrect textures
**Solution**: This is often related to graphics driver issues. Try updating your graphics drivers or use:
```bash
# Force OpenGL 3 rendering
MESA_GL_VERSION_OVERRIDE=3.3 gazebo
```

#### Issue: Slow simulation performance
**Solution**: Reduce physics simulation complexity or adjust real-time factor:
```bash
# Set real-time factor to run faster than real-time
gazebo -u
```

#### Issue: "Error in REST request" messages
**Solution**: This is often related to model database connectivity. If you don't need online models:
```bash
# Disable online model database
GAZEBO_MODEL_DATABASE_URI="" gazebo
```

### Community Resources

- **Official Website**: [http://gazebosim.org/](http://gazebosim.org/)
- **Documentation**: [http://gazebosim.org/tutorials](http://gazebosim.org/tutorials)
- **Source Code**: [https://github.com/osrf/gazebo](https://github.com/osrf/gazebo)
- **Community Forum**: [https://community.gazebosim.org/](https://community.gazebosim.org/)
- **Model Database**: [https://app.gazebosim.org/fuel](https://app.gazebosim.org/fuel)
- **Issue Tracker**: [https://github.com/osrf/gazebo/issues](https://github.com/osrf/gazebo/issues)

### Future Development: Moving to Ignition/Gazebo

Gazebo development is transitioning to Ignition Gazebo (also known as Gazebo with a different version numbering scheme). Consider exploring Ignition Gazebo for future projects:

```bash
# Install Ignition Gazebo (Ubuntu 20.04+)
sudo apt install ignition-gazebo

# Run Ignition Gazebo
ign gazebo
```

## 5.2 Other Notable 3D Simulation Tools

### Blender Physics Simulation
Open-source 3D creation suite with powerful physics simulation capabilities.

**Key Features**:
- Rigid and soft body dynamics
- Fluid and smoke simulation
- Cloth and hair physics
- Python scripting API
- Cross-platform (Windows, macOS, Linux)

### Unity3D
Game engine with extensive simulation capabilities, increasingly used for digital twins.

**Key Features**:
- High-quality rendering
- Physics simulation via PhysX
- C# scripting
- Asset store with pre-built models
- AR/VR support

### NVIDIA Omniverse
Collaborative platform for creating and operating industrial digital twins.

**Key Features**:
- Real-time ray tracing
- Physics simulation via PhysX
- USD-based workflows
- AI integration
- Multi-application connectors

### OpenFOAM
Open-source CFD (Computational Fluid Dynamics) software.

**Key Features**:
- Extensive fluid dynamics solver
- Parallel computing support
- Custom solver development
- Pre- and post-processing utilities
- Active community development
