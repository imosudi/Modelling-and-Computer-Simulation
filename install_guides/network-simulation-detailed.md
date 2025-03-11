# 3. Network & Communication System Simulation

## 3.1 NS-3 (Network Simulator 3)

### Prerequisites:
* **OS**: Linux (Ubuntu recommended), macOS (limited support)
* **Dependencies**: gcc, g++, cmake, Python3
* **Minimum Requirements**: 4GB RAM, 5GB storage, Quad-core CPU
* **Optimum Requirements**: 16GB RAM, 10GB storage, Octa-core CPU

### Installation Steps:

1. Open a terminal and install dependencies:
   ```bash
   sudo apt update && sudo apt install -y gcc g++ python3 cmake git
   ```

2. Clone NS-3 repository:
   ```bash
   git clone https://gitlab.com/nsnam/ns-3-dev.git
   ```

3. Compile and build NS-3:
   ```bash
   cd ns-3-dev
   ./ns3 configure --enable-examples
   ./ns3 build
   ```

4. Verify installation by running a simple example:
   ```bash
   ./ns3 run first
   ```

### Key Features:
* Discrete-event network simulator for Internet systems
* Support for a wide range of protocols (TCP/IP, WiFi, LTE, etc.)
* Comprehensive documentation and tutorials
* Active community and regular updates
* Visualization capabilities through NetAnim

### Common Use Cases:
* Protocol development and testing
* Performance evaluation of wireless networks
* Large-scale network behavior analysis
* Academic research and education

### Example Simulation:
```bash
# Create a simple wireless network simulation
cat > simple-wireless.cc << EOF
#include "ns3/core-module.h"
#include "ns3/network-module.h"
#include "ns3/mobility-module.h"
#include "ns3/wifi-module.h"
#include "ns3/internet-module.h"
#include "ns3/applications-module.h"

using namespace ns3;

int main() {
  NodeContainer nodes;
  nodes.Create(3);
  
  WifiHelper wifi;
  wifi.SetStandard(WIFI_STANDARD_80211n);
  
  YansWifiChannelHelper channel = YansWifiChannelHelper::Default();
  YansWifiPhyHelper phy;
  phy.SetChannel(channel.Create());
  
  WifiMacHelper mac;
  NetDeviceContainer devices = wifi.Install(phy, mac, nodes);
  
  InternetStackHelper internet;
  internet.Install(nodes);
  
  Simulator::Run();
  Simulator::Destroy();
  return 0;
}
EOF

# Compile and run the example
./ns3 run scratch/simple-wireless
```

## 3.2 Mininet (SDN Simulation)

### Prerequisites:
* **OS**: Linux (Ubuntu recommended)
* **Dependencies**: None (included in package)
* **Minimum Requirements**: 2GB RAM, 1GB storage, Dual-core CPU
* **Optimum Requirements**: 8GB RAM, 5GB storage, Quad-core CPU

### Installation Steps:

1. Install Mininet on Ubuntu:
   ```bash
   sudo apt update && sudo apt install -y mininet
   ```

2. Test Mininet with:
   ```bash
   sudo mn --test pingall
   ```

3. Install additional components for SDN:
   ```bash
   sudo apt install -y mininet openvswitch-testcontroller
   sudo cp /usr/bin/ovs-testcontroller /usr/bin/ovs-controller
   ```

4. Install Mininet development tools (optional):
   ```bash
   git clone https://github.com/mininet/mininet
   cd mininet
   sudo ./util/install.sh -a
   ```

### Key Features:
* Creation of realistic virtual networks with SDN capabilities
* Integration with real hardware and software switches
* Support for OpenFlow and other SDN protocols
* Interactive command-line interface for network manipulation
* Python API for custom topology creation and experiments

### Common Use Cases:
* Software Defined Networking (SDN) research and development
* Network protocol testing
* Data center network simulation
* Academic teaching and learning

### Example Topology:
```python
# Save this file as custom_topo.py
from mininet.topo import Topo
from mininet.net import Mininet
from mininet.cli import CLI
from mininet.log import setLogLevel
from mininet.node import OVSController

class CustomTopo(Topo):
    def build(self):
        # Add switches
        s1 = self.addSwitch('s1')
        s2 = self.addSwitch('s2')
        s3 = self.addSwitch('s3')
        
        # Add hosts
        h1 = self.addHost('h1', ip='10.0.0.1/24')
        h2 = self.addHost('h2', ip='10.0.0.2/24')
        h3 = self.addHost('h3', ip='10.0.0.3/24')
        h4 = self.addHost('h4', ip='10.0.0.4/24')
        
        # Connect hosts to switches
        self.addLink(h1, s1)
        self.addLink(h2, s1)
        self.addLink(h3, s3)
        self.addLink(h4, s3)
        
        # Connect switches in a line
        self.addLink(s1, s2)
        self.addLink(s2, s3)

def runNetwork():
    topo = CustomTopo()
    net = Mininet(topo=topo, controller=OVSController)
    net.start()
    CLI(net)
    net.stop()

if __name__ == '__main__':
    setLogLevel('info')
    runNetwork()
```

To run the custom topology:
```bash
sudo python custom_topo.py
```

## 3.2 Mininet (SDN Simulation)

Mininet creates a realistic virtual network, running real kernel, switch and application code, on a single machine. It's particularly useful for software-defined networking (SDN) development, testing, and research.

### Prerequisites:
* **OS**: Linux (Ubuntu recommended)
* **Dependencies**: Python3, Open vSwitch, OpenvSwitch-Switch
* **Minimum Requirements**: 2GB RAM, 1GB storage, Dual-core CPU
* **Optimum Requirements**: 8GB RAM, 5GB storage, Quad-core CPU

### Installation Steps:

1. Install dependencies:
```bash
sudo apt update && sudo apt install -y python3 python3-pip
sudo apt install -y openvswitch-switch openvswitch-testcontroller
```

2. Install Mininet (basic installation):
```bash
sudo apt update && sudo apt install -y mininet
```

3. For the full installation with all features (recommended):
```bash
git clone https://github.com/mininet/mininet
cd mininet
git checkout -b mininet-2.3.0 2.3.0
util/install.sh -a
```

4. Test Mininet with:
```bash
sudo mn --test pingall
```

### Common Topologies:

1. Single switch topology:
```bash
sudo mn --topo single,3
```

2. Linear topology with 4 switches:
```bash
sudo mn --topo linear,4
```

3. Tree topology with depth 2, fanout 2:
```bash
sudo mn --topo tree,depth=2,fanout=2
```

4. Custom topology (create a Python script):
```python
from mininet.topo import Topo
from mininet.net import Mininet
from mininet.node import CPULimitedHost
from mininet.link import TCLink
from mininet.util import dumpNodeConnections
from mininet.log import setLogLevel

class MyTopo(Topo):
    def build(self):
        # Add hosts and switches
        h1 = self.addHost('h1')
        h2 = self.addHost('h2')
        s1 = self.addSwitch('s1')
        
        # Add links
        self.addLink(h1, s1, bw=10, delay='5ms')
        self.addLink(h2, s1, bw=10, delay='5ms')

topos = { 'mytopo': ( lambda: MyTopo() ) }
```

### SDN Controller Integration:

1. Run with default controller:
```bash
sudo mn --controller=default
```

2. Run with remote controller:
```bash
sudo mn --controller=remote,ip=127.0.0.1,port=6653
```

3. Run with specific OpenFlow version:
```bash
sudo mn --switch ovs,protocols=OpenFlow13
```

### Network Performance Testing:

1. Bandwidth test between hosts:
```bash
mininet> h1 iperf -s &
mininet> h2 iperf -c h1
```

2. Latency test:
```bash
mininet> h1 ping h2 -c 10
```

3. TCP performance with different parameters:
```bash
mininet> h1 iperf -s &
mininet> h2 iperf -c h1 -t 30 -i 1
```



## 3.3 OMNeT++ (Modular Network Simulator)

### Prerequisites:
* **OS**: Linux, Windows, macOS
* **Dependencies**: C++ compiler, Qt libraries
* **Minimum Requirements**: 4GB RAM, 2GB storage, Dual-core CPU
* **Optimum Requirements**: 16GB RAM, 5GB storage, Quad-core CPU

### Installation Steps:

1. Download OMNeT++ from the official website:
   ```
   https://omnetpp.org/download/
   ```

2. Install dependencies on Ubuntu:
   ```bash
   sudo apt update && sudo apt install -y build-essential gcc g++ bison flex perl \
   qt5-default tcl-dev tk-dev libxml2-dev zlib1g-dev default-jre doxygen graphviz libwebkitgtk-1.0
   ```

3. Extract and configure:
   ```bash
   tar -xvzf omnetpp-6.0-src-linux.tgz
   cd omnetpp-6.0
   source setenv
   ./configure
   ```

4. Build OMNeT++:
   ```bash
   make -j$(nproc)
   ```

5. Start the IDE:
   ```bash
   omnetpp
   ```

### Key Features:
* Component-based architecture with reusable modules
* Extensive simulation library (INET Framework)
* Powerful visualization and statistical tools
* Support for parallel simulation execution
* Integration with Eclipse IDE

### Common Use Cases:
* Wired and wireless networking research
* Sensor network simulation
* Protocol development and validation
* IoT network modeling

### Example Network:
```c++
// Simple network definition
network SimpleNetwork {
    parameters:
        int numHosts = 10;
    submodules:
        router: Router {
            gates:
                port[numHosts];
        }
        host[numHosts]: Host {
            gates:
                port;
        }
    connections:
        for i=0..numHosts-1 {
            router.port[i] <--> Channel <--> host[i].port;
        }
}
```

## 3.4 GNS3 (Graphical Network Simulator)

### Prerequisites:
* **OS**: Windows, macOS, Linux (Ubuntu recommended)
* **Dependencies**: Python, Qt, VirtualBox or VMware
* **Minimum Requirements**: 8GB RAM, 20GB storage, Quad-core CPU
* **Optimum Requirements**: 32GB RAM, 100GB+ storage, Octa-core CPU with virtualization support

### Installation Steps:

1. Install dependencies:
   ```bash
   sudo apt update && sudo apt install -y python3-pip python3-dev cpp gcc make cmake \
   libelf-dev qemu qemu-kvm qemu-utils libvirt-clients libvirt-daemon-system
   ```

2. Add GNS3 repository:
   ```bash
   sudo add-apt-repository ppa:gns3/ppa
   ```

3. Install GNS3:
   ```bash
   sudo apt update && sudo apt install -y gns3-gui gns3-server
   ```

4. Add current user to required groups:
   ```bash
   sudo usermod -aG ubridge,libvirt,kvm,wireshark $(whoami)
   ```

5. Reboot and start GNS3:
   ```bash
   gns3
   ```

### Key Features:
* Simulation of complex networks with actual router/switch images
* Integration with virtual machines and Docker containers
* Support for Cisco, Juniper, and many other vendors' devices
* Capture and analysis of network traffic with Wireshark
* Design and test networks before physical deployment

### Common Use Cases:
* Network certification preparation (CCNA, CCNP, etc.)
* Enterprise network design and testing
* Security testing and penetration testing
* Protocol troubleshooting

### Basic Configuration:
1. Set up a Cisco router topology:
   - Add a Cisco IOS router from the device panel
   - Configure the router interfaces:
   ```
   Router# configure terminal
   Router(config)# interface FastEthernet0/0
   Router(config-if)# ip address 192.168.1.1 255.255.255.0
   Router(config-if)# no shutdown
   Router(config-if)# exit
   Router(config)# end
   Router# write memory
   ```

2. Configure connectivity:
   - Connect routers using the link tool
   - Verify connectivity using ping and traceroute commands
   - Capture traffic using the Wireshark integration

## 3.5 CORE (Common Open Research Emulator)

### Prerequisites:
* **OS**: Linux (Ubuntu recommended)
* **Dependencies**: Python, TK/TCL
* **Minimum Requirements**: 4GB RAM, 2GB storage, Dual-core CPU
* **Optimum Requirements**: 16GB RAM, 10GB storage, Quad-core CPU

### Installation Steps:

1. Install dependencies:
   ```bash
   sudo apt update && sudo apt install -y python3-pip build-essential git autoconf automake pkg-config make \
   libtool libxml2-dev libprotobuf-dev python3-protobuf libpcap-dev python3-tk python3-setuptools
   ```

2. Clone CORE repository:
   ```bash
   git clone https://github.com/coreemu/core.git
   ```

3. Build and install CORE:
   ```bash
   cd core
   ./bootstrap.sh
   ./configure
   make
   sudo make install
   ```

4. Start CORE GUI:
   ```bash
   core-gui
   ```

### Key Features:
* Network emulation with live-running kernel processes
* Distributed emulation capabilities across multiple servers
* Support for routing protocols (OSPF, BGP, etc.)
* Integration with physical networks
* Lightweight virtualization through Linux namespaces

### Common Use Cases:
* Mobile ad-hoc network research
* Tactical network planning and simulation
* Protocol development and testing
* Cyber security exercises and training

### Example Scenario:
1. Create a simple MANET (Mobile Ad-hoc Network):
   - Drag multiple wireless node icons to the canvas
   - Configure mobility using the mobility tool
   - Set wireless range and parameters
   - Run the emulation to see dynamic routing in action

2. Routing Protocol Test:
   ```bash
   # On a specific node in the emulation
   vtysh -c "configure terminal" -c "router ospf" -c "network 10.0.0.0/24 area 0"
   ```
