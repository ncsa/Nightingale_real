
Programming Environment
===============================

The GNU compilers (GCC) version 8.4.1 are in the default user environment. Version 12.2.0 is also available — load this version with the command:
::
module load gcc/12.2.0


Compiler Commands
-------------------

Serial
~~~~~~~~~~~
To build (compile and link) a serial program in Fortran, C, and C++ enter:

.. table:: Compiling Serial Code With GCC
+--------------------------+
| **GCC**                  |
+==========================+
| ``gfortran myprog.f``    |
|                          |
| ``gfortran myprog.f90``  |
|                          |
| ``gcc      myprog.c``    |
|                          |
| ``g++      myprog.cc``   |
+--------------------------+


MPI
~~~~~~~

To build (compile and link) a MPI program in Fortran, C, and C++:

.. table::Compiling With OpenMPI
+---------------------+-------------------------------+-------------------------------------+
| MPI Implementation  | modulefile for MPI/Compiler   | Build Commands                      |
+=====================+===============================+=====================================+
| Open MPI            | openmpi/4.1.4-gcc             | ``Fortran 77:  mpif77 myprog.f``    |
|                     |                               |                                     |
|                     |                               | ``Fortran 90:  mpif90 myprog.f90``  |
|                     |                               |                                     |
|                     |                               | ``C:           mpicc myprog.c``     |
|                     |                               |                                     |
|                     |                               | ``C++:         mpicxx myprog.cc``   |
+---------------------+-------------------------------+-------------------------------------+

OpenMP
~~~~~~~~
To build an OpenMP program, use the -fopenmp / -qopenmp option:

.. table::Compiling OpenMP Code
+---------------------------------------------+
|        **GCC**                              |
+=============================================+
| ``gfortran -fopenmp myprog.f``              |
|                                             |
| ``gfortran -fopenmp myprog.f90``            |
|                                             |
| ``gcc      -fopenmp myprog.c``              |
|                                             |
| ``g++      -fopenmp myprog.cc``             |
+---------------------------------------------+


Hybrid MPI/OpenMP
~~~~~~~~~~~~~~~~~~~~~
To build an MPI/OpenMP hybrid program, use the -fopenmp / -qopenmp option with the MPI compiling commands:

.. table::Compiling Hybrid MPI/OpenMP Code
+---------------------------------------------+
|  **GCC**                                    |
+=============================================+
|   OpenMPI                                   |
+---------------------------------------------+
| ``mpif77 -fopenmp myprog.f``                |
|                                             |
| ``mpif90 -fopenmp myprog.f90``              |
|                                             |
| ``mpicc  -fopenmp myprog.c``                |
|                                             |
| ``mpicxx -fopenmp myprog.cc``               |
+---------------------------------------------+

CUDA
~~~~~~
NVIDIA GPUs are available as part of the Nightingale compute cluster. CUDA is a parallel computing platform and programming model from NVIDIA for use on the GPUs. These GPUs support CUDA compute capability 2.0.

Load the CUDA Toolkit into your environment using the following module command:
::
``module load cuda/11.4.2``


+
