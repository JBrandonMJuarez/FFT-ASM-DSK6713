# FFT-ASM-DSK6713
FFT algorithm implemented in assembly language for the TMS320C6713 DSP

The radix-2 FFT algorithm by frequency decimation is coded in assembly language in the Code Composer Studio IDE and implemented on the DSK6713 development board to analyze its behavior and performance during execution.

## Coding and implementation
Based on the FFT and bit reversi algorithms, they are coded in C for the DSK6713.
* FFT

      DIF_FFT Algorithm
      Variables
        w[N] = {WN_n}
        N
        a[N] = {a_n}
      Start
        NumOfProblems <- 1
        ProblemSize <- N
        Repeat while (ProblemSize > 1) do
          HalfSize <- ProblemSize / 2
          Repeat for K = 0 to NumOfProblems - 1 do
            JFirst <- K * ProblemSize
            JLast <- JFirst + HalfSize - 1
            Jtwiddle <- 2 * (N - (N / NumOfProblems))
            Repeat for J = JFirst to JLast do
                W <- w[Jtwiddle]
                Temp <- a[J]
                a[J] <- Temp + a[J + HalfSize]
                a[J + HalfSize] <- W * (Temp - a[J + HalfSize])
                Jtwiddle <- Jtwiddle + 1
            End For
          End For
          NumOfProblems <- 2 * NumOfProblems
          ProblemSize <- HalfSize
        End While
      End.
* Bit reversal

      Bit_Reversal Algorithm
        Variables
        a[N]
        R[N]
        powrev[k]
      Start
        powrev[0] <- n/2
        Repeat for i = 1 to k-1 do
          powrev[i] <- powrev[i-1] / 2
        End For
        Repeat for m = 0 to n-1 do
          j <- 0
          mm <- m
          Repeat for p = 0 to k-1 do
            j <- j + [mm] * powrev[p]
            mm <- mm / 2
          End For
          R[m] <- a[j]
        End For
      End.

With MATLAB scripts, it is possible to obtain precalculated values for $W_n$ and perform some tests to compare the results.
