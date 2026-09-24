Use this as your README.md
# Parallel Matrix Multiplication Performance Analysis

## Executive Summary

This repository contains the experimental implementation and performance study of a
4000 × 4000 matrix multiplication workload using four different parallel computing
approaches:

1. Sequential CPU execution
2. OpenMP shared-memory parallelism
3. MPI distributed-memory parallelism
4. CUDA GPU acceleration

All implementations perform the same matrix multiplication workload and verify the
correctness of the output using C[0][0] = 4000.00.

### Performance Summary

The sequential implementation required 348.02 seconds. OpenMP using 8 threads
completed the execution in 132.46 seconds, while MPI using 4 nodes completed it in
92.98 seconds. CUDA GPU execution completed the total phase in approximately
0.165 seconds.

---

## Table of Contents

1. [Project Objectives](#1-project-objectives)
2. [Computing Architecture](#2-computing-architecture)
3. [System and Hardware Specifications](#3-system-and-hardware-specifications)
4. [Experimental Procedure](#4-experimental-procedure)
5. [Experimental Results and Screenshots](#5-experimental-results-and-screenshots)
6. [Performance Comparison](#6-performance-comparison)
7. [Visualizations](#7-visualizations)
8. [Technical Analysis](#8-technical-analysis)
9. [Conclusion](#9-conclusion)
10. [Repository Structure](#10-repository-structure)

---

## 1. Project Objectives

The main objectives of this Parallel Computing laboratory experiment are:

1. Implement matrix multiplication for 4000 × 4000 matrices using:
   - Sequential C
   - OpenMP
   - MPI
   - CUDA

2. Verify the correctness of the calculated matrix by checking:
   `C[0][0] = 4000.00`

3. Measure execution time and calculate the speedup obtained using different
   parallel computing approaches.

4. Compare shared-memory, distributed-memory, and GPU-based parallel execution.

---

## 2. Computing Architecture

### Sequential CPU

A single CPU thread performs the complete matrix multiplication.

### OpenMP

Multiple CPU threads execute portions of the matrix multiplication simultaneously
using shared system memory.

### MPI

The workload is distributed between multiple nodes using message passing.

### CUDA

Matrix multiplication is executed on the NVIDIA GPU using a large number of
parallel threads.

---

## 3. System and Hardware Specifications

| Parameter | Sequential | OpenMP | MPI | CUDA |
|---|---|---|---|---|
| Execution Environment | WSL2 Ubuntu 22.04 | WSL2 Ubuntu 22.04 | 4 Ubuntu VMs | NVIDIA GPU |
| Compute Units | 1 CPU Core | 8 CPU Threads | 4 Nodes | NVIDIA GPU |
| Memory Architecture | Single RAM | Shared RAM | Distributed Memory | GPU VRAM |
| Matrix Size | 4000 × 4000 | 4000 × 4000 | 4000 × 4000 | 4000 × 4000 |
| Expected C[0][0] | 4000.00 | 4000.00 | 4000.00 | 4000.00 |

---

## 4. Experimental Procedure

### Part A: Sequential Matrix Multiplication

1. Initialize matrices A and B with 1.0 values.
2. Initialize matrix C with 0.0.
3. Perform matrix multiplication using nested loops.
4. Record the execution time.

```bash
gcc -O2 src/matrix_sequential.c -o src/matrix_sequential
./src/matrix_sequential
Part B: OpenMP Parallelism
Set the number of OpenMP threads to 8.
Parallelize the outer matrix loop.
Execute the program and record the execution time.
gcc -O2 -fopenmp src/matrix_openmp.c -o src/matrix_openmp
export OMP_NUM_THREADS=8
./src/matrix_openmp
Part C: MPI Distributed Computing
Configure the master and worker nodes.
Establish communication between the nodes.
Distribute portions of the matrix using MPI.
Collect the partial results.
mpicc -O2 src/matrix_mpi.c -o src/matrix_mpi
mpirun -np 4 --hostfile hosts ./src/matrix_mpi
Part D: CUDA GPU Computing
Allocate host and GPU memory.
Transfer the matrices to GPU memory.
Execute the matrix multiplication kernel.
Transfer the resulting matrix back to the host.
nvcc -O2 src/matrix_cuda.cu -o src/matrix_cuda
./src/matrix_cuda
5. Experimental Results and Screenshots
Sequential Execution

The sequential implementation completed the matrix multiplication in approximately
348.02 seconds.

Figure 1: Sequential matrix multiplication execution.

OpenMP Execution

The OpenMP implementation used 8 threads and completed the execution in
approximately 132.46 seconds.

Figure 2: OpenMP matrix multiplication execution.

OpenMP Verification

Figure 3: Verification of the OpenMP result.

CPU Resource Monitoring

The htop utility was used to observe CPU activity during parallel execution.

Figure 4: CPU resource utilization during OpenMP execution.

6. Performance Comparison
Computing Method	Execution Time	Speedup	Result
Sequential	348.023990 s	1.00×	4000.00
OpenMP	132.457362 s	2.63×	4000.00
MPI	92.979510 s	3.74×	4000.00
CUDA Kernel	0.146443 s	2376.51×	4000.00
CUDA Total Phase	0.165004 s	2109.18×	4000.00
7. Visualizations
Execution Time Comparison

Figure 5: Execution time comparison of the different computing approaches.

Speedup Comparison

Figure 6: Speedup comparison with respect to the sequential implementation.

Performance Dashboard

Figure 7: Overall performance comparison.

8. Technical Analysis
Sequential Execution

The sequential implementation performs matrix multiplication using a single CPU
thread. Matrix multiplication has O(N³) computational complexity, resulting in a
large execution time for a 4000 × 4000 matrix.

OpenMP

OpenMP divides the workload among multiple CPU threads. Using 8 threads improves
execution time compared with the sequential implementation, although memory
bandwidth and shared-resource contention limit the achievable speedup.

MPI

MPI distributes the computation between multiple nodes. Each node processes a
portion of the matrix, and the results are combined using message passing.

CUDA

CUDA uses the GPU's massively parallel architecture to execute many matrix
operations concurrently. This significantly reduces the execution time for the
given matrix multiplication workload.

9. Conclusion

The experiment demonstrates the performance differences between sequential,
shared-memory, distributed-memory, and GPU-based computing.

The measured execution times were:

Sequential: 348.02 seconds
OpenMP: 132.46 seconds
MPI: 92.98 seconds
CUDA Total Phase: 0.165 seconds

The experiment shows how parallel computing techniques can reduce execution time
for computationally intensive matrix multiplication.

10. Repository Structure
Parallel_Computing/
│
├── README.md
├── LAB_REPORT.md
│
├── images/
│   ├── 1_sequential_execution.jpeg
│   ├── 2_openmp_execution.jpeg
│   ├── 3_openmp_verification.jpeg
│   ├── 4_htop_resource_monitor.jpeg
│   ├── 5_sequential_verification.jpeg
│   ├── execution_time_comparison.png
│   ├── speedup_comparison.png
│   └── overall_performance_dashboard.png
│
└── src/
    ├── matrix_sequential.c
    ├── matrix_openmp.c
    ├── matrix_mpi.c
    └── matrix_cuda.cu

Laboratory experiment conducted as part of the Parallel and Grid Computing course.


### Now, what you actually need to do in GitHub

Since you already created your **`Parallel_Computing`** repository:

1. Open your repository.
2. Click **`README.md`**.
3. Click the **pencil/edit icon**.
4. Select the existing README text.
5. Delete it.
6. Copy the README above.
7. Paste it there.
8. Scroll down.
9. Click **Commit changes**.

**Don't upload `README.md` from your friend's folder.** Use the README that GitHub already created in **your** repository and replace its contents with the version above.

Also, the image names in the README must match the actual files you upload into your `images` folder; otherwise GitHub will show broken images. The original README uses those image paths explicitly. :contentReference[oaicite:2]{index=2}

If you want, **send me a screenshot of your empty `Parallel_Computing` repository now**, and I'll tell you exactly **which button to click first**.
