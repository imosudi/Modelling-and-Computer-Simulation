# 2. Discrete-Event & System Modelling

## 2.1 SimPy (Python Discrete-Event Simulation Library)

### Overview
SimPy is an open-source, process-based discrete-event simulation framework built on standard Python. It allows you to model complex systems with active components (like customers, vehicles, or agents) using processes. SimPy provides shared resources, environment monitoring, and real-time event execution capabilities.

### Key Features
- Process-oriented simulation modeling
- Resource management (queues, capacity constraints)
- Monitoring and statistics collection
- Event-based simulation control
- Support for various simulation approaches (process interaction, event scheduling)
- Seamless integration with other Python libraries (NumPy, Pandas, Matplotlib)

### Prerequisites
- **Operating Systems**: Windows 7/10/11, macOS 10.13+, Linux distributions (Ubuntu, Debian, CentOS, etc.)
- **Dependencies**: Python 3.6 or higher
- **Minimum Requirements**:
  - 2GB RAM
  - 1GB storage
  - Dual-core CPU (1.6 GHz or faster)
  - Basic GPU capabilities for visualization
- **Optimum Requirements**:
  - 8GB RAM
  - 2GB storage
  - Quad-core CPU (2.5 GHz or faster)
  - Dedicated graphics card for complex visualizations

### Installation Steps
1. Install Python from the official website https://www.python.org
   - For Windows: Download the installer and check "Add Python to PATH"
   - For macOS: Use the installer or install via Homebrew with `brew install python`
   - For Linux: Use package manager (e.g., `sudo apt-get install python3`)

2. Open a terminal (Command Prompt, Terminal, or similar) and install SimPy:
   ```
   pip install simpy
   ```
   
   For potential dependency issues, use:
   ```
   pip install simpy --user
   ```

3. Verify installation by running a test script:
   ```python
   import simpy
   env = simpy.Environment()
   print("SimPy version:", simpy.__version__)
   print("SimPy installed successfully!")
   ```

4. Install optional but recommended companion packages:
   ```
   pip install numpy pandas matplotlib
   ```

### Documentation and Resources
- Official Documentation: https://simpy.readthedocs.io/
- GitHub Repository: https://github.com/team-simpy/simpy
- Community Forum: https://groups.google.com/forum/#!forum/python-simpy

## 2.2 AnyLogic PLE (Personal Learning Edition)

### Overview
AnyLogic Personal Learning Edition (PLE) is a free simulation tool for academic and educational purposes. It supports multiple modeling methods, including agent-based, discrete-event, and system dynamics approaches, allowing for hybrid simulations that combine different modeling paradigms.

### Key Features
- Multi-method modeling capabilities (agent-based, discrete-event, system dynamics)
- Graphical modeling environment with drag-and-drop interface
- Customizable agent behaviors and state charts
- Built-in statistical analysis tools
- 2D and 3D animation capabilities
- GIS integration for spatial modeling
- Industry-specific libraries (transportation, pedestrian dynamics, etc.)
- Java API for extending functionality

### Prerequisites
- **Operating Systems**:
  - Windows 10/11 (64-bit)
  - macOS 10.14+ (Mojave or newer)
  - Linux (Ubuntu 18.04+ or equivalent)
- **Dependencies**:
  - Java 8 or higher (JRE/JDK)
  - Internet connection for license activation
  - Administrator privileges for installation
- **Minimum Requirements**:
  - 4GB RAM
  - 2GB storage
  - Dual-core CPU (2.0 GHz or faster)
  - 1280×800 screen resolution
  - OpenGL-compatible graphics
- **Optimum Requirements**:
  - 16GB RAM
  - 4GB storage (SSD recommended)
  - Quad-core CPU (3.0 GHz or faster)
  - 1920×1080 screen resolution or higher
  - Dedicated graphics card with 2GB+ VRAM

### Installation Steps
1. Visit the official AnyLogic download page: https://www.anylogic.com/downloads/
   
2. Register for a free account and download the **Personal Learning Edition (PLE)** appropriate for your operating system.

3. Before installation:
   - Windows: Ensure .NET Framework 4.5+ is installed
   - macOS: Allow installation of apps from identified developers in Security settings
   - Linux: Install required dependencies (may vary by distribution)

4. Run the installer:
   - Windows: Execute the downloaded .exe file with administrator privileges
   - macOS: Mount the .dmg file and drag AnyLogic to Applications
   - Linux: Extract the archive and run the installation script

5. During installation:
   - Accept the license agreement
   - Choose the installation directory
   - Select components to install (examples, documentation, etc.)
   - Create desktop shortcuts if desired

6. After installation:
   - Launch AnyLogic
   - Complete the registration process if prompted
   - Activate your PLE license

7. Verify installation by creating a new model:
   - Click "File" > "New" > "Model"
   - Add a simple element to the canvas
   - Run simulation to confirm functionality

### Limitations of PLE Version
- Maximum of 100 agents per simulation
- Limited export capabilities
- No commercial use allowed
- Cloud execution restrictions
- No database connectivity features
- Watermark on exported results and presentations

### Documentation and Resources
- Getting Started Guide: https://anylogic.help/
- Video Tutorials: https://www.anylogic.com/resources/educational-videos/
- Example Models: Available in the software under "Help" > "Example Models"
- User Manual: Accessible through the software or online documentation portal
- Community Forum: https://forum.anylogic.com/
