# a project to analyse network latency developed CRISPpp - Windows Ebpf / Linux Ebpf

<img width="790" alt="Screenshot 2024-06-07 at 2 36 17 PM" src="https://github.com/user-attachments/assets/486f3f43-4da3-4887-9238-70c137c6b46c">


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
