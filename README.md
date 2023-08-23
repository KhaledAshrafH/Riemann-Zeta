# Riemann-Zeta

This repository contains an MPI program written in C that calculates the Riemann zeta function and evaluates its performance using MPI collective communication functions. The program approximates the value of ζ(3) with a given value of `s` (3 - Apéry's constant). It calculates the runtime, speedup, and efficiency for different numbers of processes.

## Riemann Zeta Function

The Riemann zeta function is defined as:
```
ζ(s) = 1^(-s) + 2^(-s) + 3^(-s) + ...
```

In this program, we calculate the Riemann zeta function for `s = 3 - Apéry's constant`. The goal is to approximate the value of `ζ(3)` and compare it with the expected result.

## Program Structure

The program is structured as follows:

1. **Initialization**: The main function initializes the MPI environment and retrieves the rank and number of processes.

2. **Input Prompt**: Process 0 (master) prompts the user for the number of iterations. This value determines the accuracy of the approximation.

3. **Workload Distribution**: Process 0 calculates the number of iterations per process based on the total number of iterations and distributes this information to all processes using the `MPI_Bcast` function.

4. **Partial Sum Calculation**: Each process calculates its part of the sum by iterating over a specific range of values. The iteration range for each process is determined based on its rank and the number of iterations per process.

5. **Sum Reduction**: The partial sums calculated by each process are reduced using the `MPI_Reduce` function to obtain the final sum. The reduction operation is a summation of all partial sums.

6. **Performance Evaluation**: Process 0 calculates the runtime, speedup, and efficiency of the parallel computation. The serial time is measured as the time taken to calculate the sum without using parallelization. The parallel time is measured as the time taken to calculate the sum using MPI parallelization. The speedup is calculated as the ratio of serial time to parallel time, and the efficiency is calculated as the speedup divided by the number of processes.

7. **Output**: The program prints the calculated sum, error (difference between the expected result and the calculated sum), serial time, parallel time, speedup, and efficiency. The results are also written to the `file.txt` file.

## MPI Functions Used

The program utilizes the following MPI functions:

- `MPI_Init`: Initializes the MPI environment.
- `MPI_Comm_size`: Retrieves the number of processes.
- `MPI_Comm_rank`: Retrieves the rank of the current process.
- `MPI_Bcast`: Broadcasts data from the master process to all other processes.
- `MPI_Reduce`: Performs a reduction operation on data across all processes.
- `MPI_Finalize`: Finalizes the MPI environment.

## Files

The repository contains the following files:

- `main.c`: The main C program that calculates the Riemann zeta function using MPI.
- `file.txt`: A text file used for storing the program's output.

## Dependencies

To compile and run the program, you need to have a working installation of MPI (Message Passing Interface) on your system.

## Usage

Follow the steps below to compile and run the program:

1. Ensure that you have MPI installed on your system.

2. Compile the program using an MPI compiler. For example:
   ```
   mpicc main.c -o riemann_zeta_mpi
   ```

3. Run the program with the desired number of processes. For example, to run with 4 processes:
   ```
   mpirun -np 4 ./riemann_zeta_mpi
   ```

4. The program will calculate the Riemann zeta function, print the results, and write them to the `file.txt` file.

## Output

The program will output the following information for each combination of the number of processes (`p`) and the number of iterations (`n`):

- The calculated sum of the Riemann zeta function.
- The error, which is the difference between the expected result and the calculated sum.
- The serial time, which is the time taken to calculate the sum without using parallelization.
- The parallel time, which is the time taken to calculate the sum using MPI parallelization.
- The speedup, which is the ratio of serial time to parallel time.
- The efficiency, which is the speedup divided by the number of processes.

The results will be appended to the `file.txt` file.

## Notes

- The program uses MPI collective communication functions `MPI_Bcast` and `MPI_Reduce` as specified in the requirements.
- The program assumes that the user enters a positive integer as the number of iterations (`n`).
- The accuracy of the approximation increases with a higher number of iterations.
- The program measures the runtime using the `MPI_Wtime` function, which provides wall-clock time.

## Contributing

Contributions are welcome! If you find any issues or have suggestions for improvement, please open an issue or submit a pull request.


## Authors

- [Khaled Ashraf Hanafy Mahmoud - 20190186](https://github.com/KhaledAshrafH).
- [Ahmed Sayed Hassan Youssef - 20190034](https://github.com/AhmedSayed117).
- [Samah Moustafa Hussien Mahmoud - 20190248](https://github.com/Samah-20190248).

## License

This program is licensed under the [MIT License](LICENSE.md).
