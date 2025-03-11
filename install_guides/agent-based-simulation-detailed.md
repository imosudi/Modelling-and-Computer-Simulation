# 4. Agent-Based & AI-Powered Simulations

## 4.1 NetLogo

### Prerequisites:
* **OS**: Windows, macOS, Linux
* **Dependencies**: Java 8+
* **Minimum Requirements**: 2GB RAM, 1GB storage, Dual-core CPU
* **Optimum Requirements**: 8GB RAM, 2GB storage, Quad-core CPU

### Installation Steps:

1. Download NetLogo from the official website:
   ```
   https://ccl.northwestern.edu/netlogo/download.shtml
   ```

2. For Linux users, install Java if not already present:
   ```bash
   sudo apt update && sudo apt install -y default-jre
   ```

3. For macOS users, use Homebrew to install Java:
   ```bash
   brew install openjdk@11
   ```

4. Extract the downloaded archive and run NetLogo:
   ```bash
   # Linux/macOS
   cd ~/Downloads
   tar -xzf NetLogo-*.tgz
   cd NetLogo-*
   ./netlogo
   
   # Windows
   # Run the installer executable and follow the prompts
   ```

5. Verify installation by running a sample model:
   ```
   File > Models Library > Sample Models > Biology > Wolf Sheep Predation
   ```

### Key Features:
* Built-in Models Library with hundreds of simulations
* Agent-based modeling environment with intuitive programming language
* 2D and 3D visualization capabilities
* Extensive documentation and tutorials
* BehaviorSpace tool for parameter space exploration
* HubNet architecture for participatory simulations

### Common Use Cases:
* Ecological and biological systems modeling
* Social science and economic simulations
* Complex systems research
* Educational activities and demonstrations
* Urban planning and traffic flow analysis

### Example Model:
```netlogo
;; Simple Flocking Model
globals [
  max-align-turn   ; maximum degrees one bird can turn
  max-separate-turn ; maximum degrees one bird can turn
  max-cohere-turn  ; maximum degrees one bird can turn
]

breed [birds bird]

birds-own [
  flockmates        ; agentset of nearby birds
  nearest-neighbor  ; closest bird in flockmates
  speed             ; current speed
]

to setup
  clear-all
  set max-align-turn 5
  set max-separate-turn 1.5
  set max-cohere-turn 3
  
  create-birds population [
    set shape "bird"
    set color yellow
    set size 1.5
    set speed 0.5 + random-float 0.5
    setxy random-xcor random-ycor
    set flockmates no-turtles
  ]
  
  reset-ticks
end

to go
  ask birds [
    find-flockmates
    if any? flockmates [
      find-nearest-neighbor
      flock
    ]
    fd speed
  ]
  tick
end

to find-flockmates
  set flockmates other birds in-radius vision
end

to find-nearest-neighbor
  set nearest-neighbor min-one-of flockmates [distance myself]
end

to flock
  align
  cohere
  separate
end

to align
  let avg-heading atan sum [sin heading] of flockmates sum [cos heading] of flockmates
  turn-towards avg-heading max-align-turn
end

to cohere
  let cohere-target towards mean-point-of flockmates
  turn-towards cohere-target max-cohere-turn
end

to separate
  if any? flockmates in-radius minimum-separation [
    let separate-target towards max-one-of flockmates [distance myself]
    turn-away separate-target max-separate-turn
  ]
end

to turn-towards [target max-turn]
  turn-at-most (subtract-headings target heading) max-turn
end

to turn-away [target max-turn]
  turn-at-most (subtract-headings (target + 180) heading) max-turn
end

to turn-at-most [turn max-turn]
  ifelse abs turn > max-turn
    [ ifelse turn > 0
        [ rt max-turn ]
        [ lt max-turn ] ]
    [ rt turn ]
end
```

### Advanced Usage:
1. Extending NetLogo with Extensions:
   ```netlogo
   extensions [gis csv nw]
   
   to setup-with-gis
     gis:load-dataset "map.shp"
     gis:set-world-envelope gis:envelope-of map-dataset
   end
   ```

2. Exporting and analyzing simulation data:
   ```netlogo
   to export-results
     file-open "simulation-results.csv"
     file-print csv:to-row (list "tick" "population" "average-energy")
     file-close
   end
   ```

## 4.2 SUMO (Traffic Simulation)

### Prerequisites:
* **OS**: Linux, Windows (via WSL), macOS
* **Dependencies**: None (all included in installation)
* **Minimum Requirements**: 4GB RAM, 1GB storage, Dual-core CPU
* **Optimum Requirements**: 16GB RAM, 2GB storage, Quad-core CPU

### Installation Steps:

1. For Ubuntu/Debian, install SUMO using apt:
   ```bash
   sudo apt update && sudo apt install -y sumo sumo-tools sumo-doc
   ```

2. For Windows, download and install from the official website:
   ```
   https://sumo.dlr.de/docs/Downloads.php
   ```

3. For macOS, use Homebrew:
   ```bash
   brew tap dlr-ts/sumo
   brew install sumo
   ```

4. Set up environment variables:
   ```bash
   # Linux/macOS
   echo 'export SUMO_HOME="/usr/share/sumo"' >> ~/.bashrc
   source ~/.bashrc
   
   # Windows
   setx SUMO_HOME "C:\Program Files (x86)\Eclipse\Sumo"
   ```

5. Run SUMO GUI to verify installation:
   ```bash
   sumo-gui
   ```

6. Test with a basic simulation:
   ```bash
   cd $SUMO_HOME/docs/tutorial
   sumo-gui -c data/hello.sumocfg
   ```

### Key Features:
* Microscopic traffic simulation for urban environments
* Supports large-scale networks with millions of vehicles
* Includes tools for network import and editing
* Interfaces with popular programming languages (Python, Java)
* Real-time visualization and 3D rendering capabilities
* Emission and noise modeling
* Traffic light control optimization

### Common Use Cases:
* Urban traffic planning and optimization
* Public transportation system design
* Emission and environmental impact studies
* Autonomous vehicle testing
* Traffic management strategy evaluation
* Large-scale evacuation simulations

### Example Simulation:
1. Create a basic network (save as `my_net.net.xml`):
   ```xml
   <net version="1.9" junctionCornerDetail="5" limitTurnSpeed="5.50" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="http://sumo.dlr.de/xsd/net_file.xsd">
       <location netOffset="0.00,0.00" convBoundary="0.00,0.00,1000.00,0.00" origBoundary="-10000000000.00,-10000000000.00,10000000000.00,10000000000.00" projParameter="!"/>
       <edge id="E0" from="J0" to="J1" priority="-1">
           <lane id="E0_0" index="0" speed="13.89" length="1000.00" shape="0.00,-1.60 1000.00,-1.60"/>
       </edge>
       <junction id="J0" type="dead_end" x="0.00" y="0.00" incLanes="" intLanes="" shape="0.00,0.00 0.00,-3.20"/>
       <junction id="J1" type="dead_end" x="1000.00" y="0.00" incLanes="E0_0" intLanes="" shape="1000.00,-3.20 1000.00,0.00"/>
   </net>
   ```

2. Create routes (save as `my_routes.rou.xml`):
   ```xml
   <routes xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="http://sumo.dlr.de/xsd/routes_file.xsd">
       <vType id="car" accel="2.6" decel="4.5" sigma="0.5" length="5" minGap="2.5" maxSpeed="50" color="1,0,0"/>
       <route id="route0" edges="E0"/>
       <vehicle id="veh0" type="car" route="route0" depart="0"/>
       <vehicle id="veh1" type="car" route="route0" depart="2"/>
       <vehicle id="veh2" type="car" route="route0" depart="4"/>
       <vehicle id="veh3" type="car" route="route0" depart="6"/>
   </routes>
   ```

3. Create configuration (save as `my_sim.sumocfg`):
   ```xml
   <configuration xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="http://sumo.dlr.de/xsd/sumoConfiguration.xsd">
       <input>
           <net-file value="my_net.net.xml"/>
           <route-files value="my_routes.rou.xml"/>
       </input>
       <time>
           <begin value="0"/>
           <end value="100"/>
       </time>
   </configuration>
   ```

4. Run the simulation:
   ```bash
   sumo-gui -c my_sim.sumocfg
   ```

### Python Integration with TraCI:
```python
# Example Python script for SUMO control via TraCI
import traci
import time

# Start the simulation
sumo_binary = "sumo-gui"
sumo_cmd = [sumo_binary, "-c", "my_sim.sumocfg"]
traci.start(sumo_cmd)

# Simulation loop
step = 0
while step < 1000:
    traci.simulationStep()
    
    # Get vehicle IDs
    vehicle_ids = traci.vehicle.getIDList()
    
    # Process each vehicle
    for veh_id in vehicle_ids:
        # Get vehicle position
        x, y = traci.vehicle.getPosition(veh_id)
        
        # Get vehicle speed
        speed = traci.vehicle.getSpeed(veh_id)
        
        # Change vehicle color based on speed
        normalized_speed = min(speed / 13.89, 1.0)  # Normalize by max speed
        r = 1.0 - normalized_speed
        g = normalized_speed
        b = 0.0
        traci.vehicle.setColor(veh_id, (int(r*255), int(g*255), int(b*255), 255))
    
    step += 1
    time.sleep(0.05)  # Slow down simulation for visualization

# Close TraCI connection
traci.close()
```

## 4.3 AnyLogic

### Prerequisites:
* **OS**: Windows, macOS, Linux
* **Dependencies**: Java 11+
* **Minimum Requirements**: 8GB RAM, 4GB storage, Quad-core CPU
* **Optimum Requirements**: 32GB RAM, 10GB storage, Octa-core CPU with dedicated GPU

### Installation Steps:

1. Download AnyLogic Personal Learning Edition from the official website:
   ```
   https://www.anylogic.com/downloads/
   ```

2. Install Java Development Kit if not already present:
   ```bash
   # Ubuntu/Debian
   sudo apt update && sudo apt install -y openjdk-11-jdk
   
   # macOS
   brew install openjdk@11
   
   # Windows
   # Download and install from https://adoptopenjdk.net/
   ```

3. Run the installer and follow the prompts:
   ```bash
   # Linux
   cd ~/Downloads
   chmod +x AnyLogic-*-Linux.bin
   ./AnyLogic-*-Linux.bin
   
   # macOS/Windows
   # Double-click the installer and follow the prompts
   ```

4. Verify installation by creating a new model:
   ```
   File > New > Agent Based Model
   ```

### Key Features:
* Multiple modeling paradigms: agent-based, system dynamics, discrete-event
* Rich Java-based modeling environment
* Extensive libraries for specific domains (pedestrian, rail, fluid, etc.)
* 3D visualization and animation capabilities
* Statistical analysis and experiment frameworks
* Cloud execution for large-scale simulations
* GIS integration for spatial modeling

### Common Use Cases:
* Supply chain optimization
* Manufacturing process improvement
* Healthcare systems analysis
* Pedestrian flow and evacuation planning
* Warehouse and logistics operations
* Transportation systems modeling
* Business process optimization

### Example Model:
```java
// Simple Customer Agent Model in AnyLogic
public class Customer extends Agent {
    // Parameters
    public double serviceTime;
    public double patience;
    
    // Variables
    public double waitingTime;
    public boolean isServed;
    
    // Statechart states
    public StatechartElement Waiting;
    public StatechartElement BeingServed;
    public StatechartElement Leaving;
    
    // Initialize the customer
    @Override
    public void onCreate() {
        waitingTime = 0;
        isServed = false;
        patience = triangular(2, 5, 15);  // Random patience between 2-15 minutes
        serviceTime = triangular(3, 7, 12);  // Random service time
    }
    
    // Custom behavior when waiting
    public void updateWaiting() {
        waitingTime += 1/60.0;  // Add one second in hours
        if (waitingTime > patience) {
            // Customer runs out of patience
            send("leave_queue", this);
        }
    }
    
    // Event when service is complete
    public void serviceComplete() {
        isServed = true;
        send("service_finished", this);
    }
}
```

### Advanced Features:
1. Database Integration:
   ```java
   // Connect to a database
   Database db = connectToDB(DATABASE_URL, USERNAME, PASSWORD);
   
   // Execute query
   ResultSet rs = db.executeQuery("SELECT * FROM customer_data");
   
   // Process results
   while (rs.next()) {
       int id = rs.getInt("id");
       String name = rs.getString("name");
       // Use the data in simulation
       Customer customer = new Customer();
       customer.setId(id);
       customer.setName(name);
       add_customer(customer);
   }
   ```

2. Custom Visualization with Charts:
   ```java
   // Create time plot
   TimePlot waitingTimePlot = new TimePlot(this);
   waitingTimePlot.addDataSet("Average Waiting Time", Color.BLUE, 2);
   
   // Update the plot during simulation
   waitingTimePlot.addDataPoint("Average Waiting Time", time(), calculateAverageWaitingTime());
   ```

## 4.4 Repast Simphony

### Prerequisites:
* **OS**: Windows, macOS, Linux
* **Dependencies**: Java 8+, Eclipse IDE (recommended)
* **Minimum Requirements**: 4GB RAM, 2GB storage, Dual-core CPU
* **Optimum Requirements**: 16GB RAM, 5GB storage, Quad-core CPU

### Installation Steps:

1. Download Repast Simphony from the official website:
   ```
   https://repast.github.io/download.html
   ```

2. Install Java Development Kit if not already present:
   ```bash
   sudo apt update && sudo apt install -y openjdk-8-jdk
   ```

3. For the complete installation with IDE:
   ```bash
   # Download the installer and run
   chmod +x repast_simphony_installer-*.jar
   java -jar repast_simphony_installer-*.jar
   ```

4. Follow installation wizard (select "Install Repast Simphony with Eclipse")

5. Launch Repast Simphony:
   ```bash
   cd repast_simphony/eclipse
   ./repast
   ```

### Key Features:
* Pure Java-based agent modeling platform
* Flexible agent scheduling
* Built-in data collection and visualization tools
* GIS integration for spatial analysis
* ReLogo domain-specific language for easy modeling
* Distributed computing capabilities
* Batch run manager for parameter exploration

### Common Use Cases:
* Social network analysis
* Ecological modeling
* Economic and market simulations
* Epidemiological studies
* Urban dynamics modeling
* Policy analysis and evaluation
* Military and defense simulations

### Example Model:
```java
// Simple Zombie Infection Model in Repast Simphony
package zombieModel;

import repast.simphony.context.Context;
import repast.simphony.engine.environment.RunEnvironment;
import repast.simphony.engine.schedule.ScheduledMethod;
import repast.simphony.parameter.Parameters;
import repast.simphony.random.RandomHelper;
import repast.simphony.space.continuous.ContinuousSpace;
import repast.simphony.space.continuous.NdPoint;
import repast.simphony.space.grid.Grid;
import repast.simphony.util.ContextUtils;

public class Human {
    private ContinuousSpace<Object> space;
    private Grid<Object> grid;
    private boolean infected = false;
    private int infectionTime = 0;
    private int timeToTurnIntoZombie;

    public Human(ContinuousSpace<Object> space, Grid<Object> grid) {
        this.space = space;
        this.grid = grid;
        
        // Get parameter from simulation
        Parameters params = RunEnvironment.getInstance().getParameters();
        timeToTurnIntoZombie = (Integer)params.getValue("zombieTransformationTime");
    }
    
    @ScheduledMethod(start = 1, interval = 1)
    public void step() {
        // Move the human
        NdPoint myPoint = space.getLocation(this);
        double x = myPoint.getX() + RandomHelper.nextDoubleFromTo(-1, 1);
        double y = myPoint.getY() + RandomHelper.nextDoubleFromTo(-1, 1);
        space.moveByDisplacement(this, x, y);
        
        // Update grid position after moving in continuous space
        myPoint = space.getLocation(this);
        grid.moveTo(this, (int)myPoint.getX(), (int)myPoint.getY());
        
        // If infected, check if it's time to turn into zombie
        if (infected) {
            infectionTime++;
            if (infectionTime >= timeToTurnIntoZombie) {
                turnIntoZombie();
            }
        }
    }
    
    public void getInfected() {
        this.infected = true;
    }
    
    private void turnIntoZombie() {
        // Get the context
        Context<Object> context = ContextUtils.getContext(this);
        
        // Create a new zombie at this location
        NdPoint myPoint = space.getLocation(this);
        Zombie zombie = new Zombie(space, grid);
        context.add(zombie);
        
        // Move the zombie to this human's location
        space.moveTo(zombie, myPoint.getX(), myPoint.getY());
        grid.moveTo(zombie, (int)myPoint.getX(), (int)myPoint.getY());
        
        // Remove the human
        context.remove(this);
    }
}
```

### Advanced Usage:
1. Using ReLogo for simplified modeling:
   ```groovy
   // ReLogo example
   to setup
     clear-all
     create-humans 100 [
       setxy random-xcor random-ycor
       set color blue
     ]
     create-zombies 5 [
       setxy random-xcor random-ycor
       set color red
     ]
   end
   
   to go
     ask humans [
       move
       if any? zombies-here [
         get-infected
       ]
     ]
     ask zombies [
       move
       infect-nearby-humans
     ]
     tick
   end
   ```

2. Setting up Batch Runs for Parameter Sweeping:
   ```java
   // In BatchRunner.java
   @Parameter(displayName = "Initial Number of Humans", usageName = "numHumans")
   public int numHumans = 100;
   
   @Parameter(displayName = "Initial Number of Zombies", usageName = "numZombies")
   public int numZombies = 5;
   
   @Parameter(displayName = "Infection Probability", usageName = "infectionProb")
   public double infectionProb = 0.5;
   
   @ParameterSweep({"numHumans", "numZombies"})
   public Set<Integer> populationSweep = Set.of(50, 100, 200);
   
   @ParameterSweep({"infectionProb"})
   public Set<Double> probSweep = Set.of(0.1, 0.5, 0.9);
   ```

## 4.5 MASON (Multi-Agent Simulator Of Neighborhoods)

### Prerequisites:
* **OS**: Windows, macOS, Linux
* **Dependencies**: Java 8+
* **Minimum Requirements**: 2GB RAM, 1GB storage, Dual-core CPU
* **Optimum Requirements**: 8GB RAM, 2GB storage, Quad-core CPU

### Installation Steps:

1. Download MASON from the official website:
   ```
   https://cs.gmu.edu/~eclab/projects/mason/
   ```

2. Install Java Development Kit:
   ```bash
   sudo apt update && sudo apt install -y openjdk-8-jdk
   ```

3. Extract the MASON archive:
   ```bash
   unzip mason*.zip -d mason
   ```

4. Add MASON to your Java classpath:
   ```bash
   export CLASSPATH=$CLASSPATH:~/mason/mason.jar:~/mason/lib/*
   ```

5. Run a demo:
   ```bash
   java sim.app.heatbugs.HeatBugsWithUI
   ```

### Key Features:
* Fast, portable Java-based simulation core
* Support for both 2D and 3D visualization
* Built-in charting capabilities
* Serialization of entire simulation state
* Very lightweight with minimal dependencies
* OpenGL-based 3D visualization