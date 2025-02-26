[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)
# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: LI, Ruoxuan
### Student ID: 20761765
### Email: rliba@connect.ust.hk

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of the measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

    > The tool used for testing CPU and memory performance is sysbench, which provides simple and straightforward testing instructions for both CPU and memory. For CPU testing, the input instruction is: "_sysbench --histogram=on --threads=2 CPU run_". To test the multi-threads capacity of the CPU, the value for "_--threads_" is set to 2 to evaluate the multi-core capacity. And "_--histogram_" is set to on for an intuitive layout.
    >
    > The instruction for testing memory is "_sysbench --threads=1 --memory-block-size=1k memory run_". In this case, to avoid the influence of different CPUs, parameter "_--threads_" is set to 1 and "_--memory-block-size_" is set to 1k to reduce the burden of the CPUs.
    >
    > The results are shown below. The CPU testing results are mainly about the latency evaluated from multiple perspectives. As for the results of memory tests, they are much simpler since they are all about the speed of data transfer.

2. (1 mark) Run your measurement tool on general-purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance | Memory performance |
    | ----------- | --------------- | ------------------ |
    | `t2.micro` |  ![image](https://github.com/user-attachments/assets/7634d0ff-cb0c-4ddc-b962-0abf7dcd6da4)  |![image](https://github.com/user-attachments/assets/198515ee-505e-4007-add0-f050c153d797)  |
    | `t2.medium`  |  ![image](https://github.com/user-attachments/assets/107eb278-a3b0-4954-81bb-c5b8d77513ce) |![image](https://github.com/user-attachments/assets/59c35cfd-c6a8-4b36-9a7f-a8547ea4821d)|
    | `c5d.large` |![image](https://github.com/user-attachments/assets/7357fd1f-4fc6-4e72-b11f-e08b6d3b7d80)  |![image](https://github.com/user-attachments/assets/1a348d3d-ede9-459a-b0b0-d598775be99c)|

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` |                |          |
    | `m5.large` - `m5.large`   |                |          |
    | `c5n.large` - `c5n.large` |                |          |
    | `t3.medium` - `c5n.large` |                |          |
    | `m5.large` - `c5n.large`  |                |          |
    | `m5.large` - `t3.medium`  |                |          |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      |                |          |
    | N. Virginia - N. Virginia |                |          |
    | Oregon - Oregon           |                |          |
 
    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.
