# Network & Communication System Simulation

## Table of Contents
- [3.1 NS-3 (Network Simulator 3)](#31-ns-3-network-simulator-3)
- [3.2 Mininet (SDN Simulation)](#32-mininet-sdn-simulation)
- [3.3 GNS3 (Graphical Network Simulator)](#33-gns3-graphical-network-simulator)
- [3.4 OMNeT++ (Objective Modular Network Testbed)](#34-omnet-objective-modular-network-testbed)
- [3.5 Common Simulation Scenarios](#35-common-simulation-scenarios)

## 3.1 NS-3 (Network Simulator 3)

NS-3 is a discrete-event network simulator primarily used for research and educational purposes. It provides substantial support for simulation of TCP, routing, and multicast protocols over wired and wireless networks.

### Prerequisites:
* **OS**: Linux (Ubuntu recommended), macOS (limited support), Windows (via WSL)
* **Dependencies**: gcc, g++, cmake, Python3, python3-dev, python3-pip
* **Minimum Requirements**: 4GB RAM, 5GB storage, Quad-core CPU
* **Optimum Requirements**: 16GB RAM, 10GB storage, Octa-core CPU

### Installation Steps:

1. Open a terminal and install dependencies:

```bash
sudo apt update && sudo apt install -y gcc g++ python3 python3-dev python3-pip cmake git libxml2-dev libsqlite3-dev
```

2. Clone NS-3 repository:

```bash
git clone https://gitlab.com/nsnam/ns-3-dev.git
```

3. Compile and build NS-3:

```bash
cd ns-3-dev
./ns3 configure --enable-examples --enable-tests
./ns3 build
```

4. Verify installation:

```bash
./ns3 run hello-simulator
```

### Configuration Options:

* Enable specific modules:
```bash
./ns3 configure --enable-examples --enable-modules='core,network,internet,applications'
```

* Enable debugging:
```bash
./ns3 configure --build-profile=debug
```

* Enable optimizations:
```bash
./ns3 configure --build-profile=optimized
```

### Running Simulations:

1. Basic simulation execution:
```bash
./ns3 run "scratch/myfirst.cc"
```

2. With command-line arguments:
```bash
./ns3 run "scratch/myfirst.cc --PrintHelp"
```

3. Running with example programs:
```bash
./ns3 run "tcp-variants-comparison --duration=30 --tracing=true"
```

### Troubleshooting:

* Missing dependencies: 
```bash
sudo apt install python3-setuptools python3-pygraphviz python3-pygccxml
```

* Visualization support:
```bash
sudo apt install python3-matplotlib python3-tk ipython3
```

* Build errors:
```bash
./ns3 clean
./ns3 configure --enable-examples
./ns3 build
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

## 3.3 GNS3 (Graphical Network Simulator)

GNS3 allows the emulation of complex networks by combining virtual and real devices. It's widely used for network certification training and testing network configurations.

### Prerequisites:
* **OS**: Windows, Linux, macOS
* **Dependencies**: VirtualBox or VMware
* **Minimum Requirements**: 4GB RAM, 10GB storage, Quad-core CPU
* **Optimum Requirements**: 16GB RAM, 50GB storage, Octa-core CPU with virtualization support

### Installation Steps:

1. For Ubuntu:
```bash
sudo add-apt-repository ppa:gns3/ppa
sudo apt update
sudo apt install -y gns3-gui gns3-server
```

2. Install virtualization support:
```bash
sudo apt install -y virtualbox
```

3. For Cisco emulation, install Dynamips:
```bash
sudo apt install -y dynamips
```

### Key Features:
* Emulation of Cisco IOS, Juniper, and other network devices
* Integration with virtual machines
* Support for Wireshark packet capture
* Drag-and-drop network design interface
* Support for custom appliances

### Troubleshooting:
* GNS3 VM connectivity issues:
```bash
sudo systemctl restart libvirtd
```

* Permission problems:
```bash
sudo usermod -aG libvirt,kvm,wireshark,ubridge $USER
```

## 3.4 OMNeT++ (Objective Modular Network Testbed)

OMNeT++ is an extensible, modular, component-based C++ simulation library and framework primarily for building network simulators.

### Prerequisites:
* **OS**: Linux, Windows, macOS
* **Dependencies**: C++ compiler, Qt, make
* **Minimum Requirements**: 4GB RAM, 5GB storage, Dual-core CPU
* **Optimum Requirements**: 8GB RAM, 10GB storage, Quad-core CPU

### Installation Steps for Ubuntu:

1. Install dependencies:
```bash
sudo apt update && sudo apt install -y build-essential gcc g++ bison flex zlib1g-dev libxml2-dev qtbase5-dev qtchooser qt5-qmake qtbase5-dev-tools libqt5opengl5-dev libwebkit2gtk-4.0-dev xvfb doxygen graphviz
```

2. Download OMNeT++ (check website for latest version):
```bash
wget https://github.com/omnetpp/omnetpp/releases/download/omnetpp-6.0.1/omnetpp-6.0.1-linux-x86_64.tgz
tar xvfz omnetpp-6.0.1-linux-x86_64.tgz
cd omnetpp-6.0.1
```

3. Configure and build:
```bash
source setenv
./configure
make -j$(nproc)
```

4. Start the IDE:
```bash
omnetpp
```

### Sample Simulation:
1. Create a new OMNeT++ project
2. Add the following network definition (.ned file):
```
network SimpleNetwork {
    parameters:
        int numNodes = default(5);
    submodules:
        node[numNodes]: SimpleNode;
    connections:
        for i=0..numNodes-2 {
            node[i].out --> node[i+1].in;
            node[i].in <-- node[i+1].out;
        }
}
```

### Framework Extensions:
* INET Framework: Internet protocols simulation
* VEINS: Vehicular network simulation
* SimuLTE: LTE networks simulation
* OverSim: Peer-to-peer and overlay networks

## 3.5 Common Simulation Scenarios

### TCP/IP Protocol Stack:
```bash
# NS-3 example for TCP simulation
./ns3 run "tcp-variants-comparison --tcpVariant=TcpNewReno --duration=100"
```

### Wireless Networks:
```bash
# NS-3 WiFi example
./ns3 run "wifi-simple-adhoc --distance=50"
```

### SDN Controllers:
```bash
# Mininet with custom controller
sudo mn --controller=remote,ip=127.0.0.1,port=6653 --topo tree,3
```

### Performance Analysis:
```bash
# Extract performance metrics in NS-3
./ns3 run "bulksend --tracing=true --prefix=data"
```

### IoT Network Simulation:
```bash
# LoRaWAN simulation in NS-3
git clone https://github.com/signetlabdei/lorawan
cd lorawan
./ns3 configure --enable-examples
./ns3 build
./ns3 run "lorawan-network-example"
```
