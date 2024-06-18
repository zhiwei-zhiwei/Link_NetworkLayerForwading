## Link & Network Layer Forwarding

## Overview

This project involves implementing the forwarding behavior of a switch and a router. A switch forwards packets based on MAC addresses, and a router forwards packets based on IP addresses. The project is divided into three main parts:

1. **Getting Started**
2. **Implementing a Virtual Switch**
3. **Implementing a Virtual Router**

## Learning Outcomes

Upon completion, students will be able to:
- Construct a learning switch that optimally forwards packets based on link layer headers.
- Determine the matching route table entry for a given IP address.
- Develop a router that updates and forwards packets based on network layer headers.

## Prerequisites

### Software Requirements
- Mininet
- POX (Software-Defined Networking control platform)
- VirtualBox
- Java (>= 8)
- Python 2.7

### Installation Steps
1. **Run Mininet VM using VirtualBox**.
2. **Install required packages**:
    ```sh
    sudo apt-get update
    sudo apt-get install -y python-dev python-setuptools flex bison ant openjdk-8-jdk git screen
    ```
3. **Install ltprotocol**:
    ```sh
    cd ~
    git clone https://github.com/dound/ltprotocol.git
    cd ltprotocol
    sudo pip install twisted
    sudo python setup.py install
    ```
    If you encounter an error with setuptools, update it:
    ```sh
    sudo pip install --upgrade setuptools pip
    ```
4. **Checkout the appropriate version of POX**:
    ```sh
    cd ~/pox
    git checkout f95dd1
    ```
5. **Download the starter code**:
    ```sh
    cd ~
    wget https://pages.cs.wisc.edu/~mgliu/CS640/F22/labs/lab2/lab2.tgz
    tar xzvf lab2.tgz
    ```
6. **Symlink POX and configure the POX modules**:
    ```sh
    cd ~/lab2
    ln -s ~/pox
    sudo chmod +x config.sh && ./config.sh
    ```

## Part 1: Getting Started

### Sample Configuration
- The initial configuration consists of a single switch (s1) and three emulated hosts (h1, h2, h3).
- Each host runs an HTTP server.

### Running the Virtual Switch
1. **Start Mininet emulation**:
    ```sh
    cd ~/lab2/
    sudo python run_mininet.py topos/single_sw.topo -a
    ```
2. **Start the controller**:
    ```sh
    cd ~/lab2/
    sudo chmod +x run_pox.sh && ./run_pox.sh
    ```
3. **Restart Mininet emulation**:
    ```sh
    cd ~/lab2/
    sudo python ./run_mininet.py topos/single_sw.topo -a
    ```
4. **Build and start the virtual switch**:
    ```sh
    cd ~/lab2/
    ant
    java -jar VirtualNetwork.jar -v s1
    ```
5. **Ping test**:
    ```sh
    mininet> h1 ping -c 2 10.0.1.102
    ```

## Part 2: Implement Virtual Switch

### Task
- Implement a learning switch that forwards packets based on destination MAC addresses.
- Timeout learned MAC addresses after 15 seconds.

### Testing
- Test using provided topologies: `single_sw.topo`, `linear5_sw.topo`, `inclass_sw.topo`.

## Part 3: Implement Virtual Router

### Tasks
1. **Route Lookups**: Complete `lookup(...)` in `RouteTable` class.
2. **Checking Packets**: Complete `handlePacket(...)` in `Router` class.

### Forwarding Packets
- Update and forward IPv4 packets based on destination IP addresses.
- Use statically provided route table and ARP cache.

### Testing
- Test using provided topologies: `single_rt.topo`, `pair_rt.topo`, `triangle_rt.topo`, `linear5_rt.topo`.

## Submission Instructions
- Submit a single tar file of the `src` directory containing Java source files for your virtual switch and router.
- Command to create tar file:
    ```sh
    tar czvf username1_username2.tgz src
    ```
- Upload the tar file on the Lab2 tab on the course's Canvas page.

## Additional Information
- Refer to the provided documentation and examples for detailed steps and configuration settings.
