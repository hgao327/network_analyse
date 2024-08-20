# a project to analyse network latency developed CRISPpp - Windows Ebpf / Linux Ebpf

<img width="790" alt="Screenshot 2024-06-07 at 2 36 17 PM" src="https://github.com/user-attachments/assets/486f3f43-4da3-4887-9238-70c137c6b46c">

The significance of this system lies in its ability to accurately identify and address network performance bottlenecks within data centers or large fleets. By promptly detecting and resolving these issues, the system enhances service efficiency, optimizes resource allocation, and minimizes service disruptions, thereby significantly improving user experience and reducing operational costs. Through real-time monitoring and advanced analytics, not only does it improve network efficiency and reduce service interruptions, but it also helps save on operational costs and ensures the best service experience for users. Additionally, the scalability of the system means it can adapt to the growing demands of the infrastructure, supporting the long-term growth of the business.

![image](https://github.com/user-attachments/assets/9be745ad-6728-4052-844a-7d9e1412299a)

### 1. **Dynamic Module Loading**

#### ebpfsvc
- **Service Components**: The `ebpfsvc` directory likely contains core functionalities related to the eBPF service. Depending on actual needs, these services can be started or stopped on demand, especially during periods of low usage or when system resources are strained.

#### libs
- **Library Files**: The `libs` directory contains libraries that may be shared across multiple components. Specific libraries can be dynamically loaded or unloaded based on the type of eBPF programs being executed, to reduce memory usage.

#### tools
- **Toolset**: The `tools` directory may contain auxiliary programs and utilities. These tools generally do not need to be loaded into memory permanently and can be dynamically loaded as needed.

### 2. **On-Demand Service Start-Up**

#### ebpfcore
- **Core Functionality**: The `ebpfcore` directory may contain the core logic for handling eBPF programs. This module can be designed to start on demand, only loading into memory when eBPF programs need to be executed.

#### netebpfext
- **Network Extensions**: The `netebpfext` directory may involve extensions for network functionalities. Depending on network load and actual needs, this part of the functionality can be optionally enabled or disabled to optimize network performance and resource usage.

### 3. **Configurable Components**

#### installer
- **Installation Scripts/Programs**: The `installer` directory contains scripts or programs related to installation. This part is typically only used during installation or updates, thus does not need to reside in memory constantly.

#### manifests/Kubernetes
- **Kubernetes Support**: This directory provides support for Kubernetes integration. If the deployment environment does not involve Kubernetes, consider not loading this module.

### 4. **Optimized Startup and Execution Strategies**

- **Lazy Loading**: For components that are not immediately needed, implement a lazy loading strategy, which involves not loading them until they are actually required.
- **Resource Monitoring**: Monitor system resource usage in real-time and dynamically adjust module loading strategies based on resource utilization rates.

By implementing these strategies, unnecessary resource consumption can be effectively reduced, and the system's response speed and operational efficiency can be enhanced. These strategies should be adjusted and optimized based on the actual deployment and usage scenarios.

# USAGE
## ebpf config for ubuntu
```
sudo apt install make clang llvm libelf1 libelf-dev zlib1g-dev bpfcc-tools linux-headers-$(uname -r)
```
if you cant not get vmlinux.h, you can generate it with command below
```
bpftool btf dump file /sys/kernel/btf/vmlinux format c > vmlinux.h
```
## complie
```
./complie.sh
```
## run the test demo
```
./bin/server
./bin/client
```
## run the ebpf part
```
./bin/tcp_analyse_service
./bin/tcp_analyse
```

## run the ebpf part with PID
```
./bin/tcp_analyse_service -p $(PID from test service demo)
./bin/tcp_analyse -p $(PID from test client demo)
```

# result
![image](https://github.com/user-attachments/assets/187811d7-12b8-4182-b002-9be188115309)
<img width="841" alt="Screenshot 2024-08-19 at 9 22 30 PM" src="https://github.com/user-attachments/assets/0d1a4f5a-8c33-412e-9d2f-248905dcf680">

