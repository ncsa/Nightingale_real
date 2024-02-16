
Programming Environment
===============================

GNU Compiler Collection (GCC) `version 8.4.1 <https://gcc.gnu.org/gcc-8/>`_ is in the default user environment. `Version 12.2.0 <https://gcc.gnu.org/gcc-12/>`_ is also available; load version 12.2.0 with the command: 

.. code-block::

   module load gcc/12.2.0


Compiler Commands
-------------------

Serial
~~~~~~~~~~~
To build (compile and link) a serial program in Fortran, C, and C++ enter:

.. table:: Compiling Serial Code With GCC
   
   +---------------------+---------------------------+
   | GCC                 |  Build Commands           |
   +=====================+===========================+
   | Fortran 77          | ``gfortran myprog.f``     |
   +---------------------+---------------------------+
   | Fortran 90          | ``gfortran myprog.f900``  |
   +---------------------+---------------------------+
   | C                   | ``gcc myprog.c``          |
   +---------------------+---------------------------+
   | C++                 | ``g++ myprog.cc``         |
   +---------------------+---------------------------+



MPI
~~~~~~~
*(coming soon)*

To build (compile and link) a MPI program in Fortran, C, and C++:

.. table:: Compiling With OpenMPI

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
To build an OpenMP program, use the ``-fopenmp`` option:

.. table:: Compiling OpenMP Code

   +---------------------+-----------------------------------+
   | GCC                 |  Build Commands                   |
   +=====================+===================================+
   | Fortran 77          | ``gfortran -fopenmp myprog.f``    |
   +---------------------+-----------------------------------+
   | Fortran 90          | ``gfortran -fopenmp myprog.f900`` |
   +---------------------+-----------------------------------+
   | C                   | ``gcc -fopenmp myprog.c``         |
   +---------------------+-----------------------------------+
   | C++                 | ``g++ -fopenmp myprog.cc``        |
   +---------------------+-----------------------------------+



Hybrid MPI/OpenMP
~~~~~~~~~~~~~~~~~~~~~
*(coming soon)*

To build an MPI/OpenMP hybrid program, use the ``-fopenmp`` option with the MPI compiling commands:

.. table:: Compiling Hybrid MPI/OpenMP Code

   +---------------------+-------------------------------+----------------------------------------------+
   | MPI Implementation  | modulefile for MPI/Compiler   | Build Commands                               |
   +=====================+===============================+==============================================+
   | Open MPI            | openmpi/4.1.4-gcc             | ``Fortran 77:  mpif77 -fopenmp myprog.f``    |
   |                     |                               |                                              |
   |                     |                               | ``Fortran 90:  mpif90 -fopenmp myprog.f90``  |
   |                     |                               |                                              |
   |                     |                               | ``C:           mpicc -fopenmp myprog.c``     |
   |                     |                               |                                              |
   |                     |                               | ``C++:         mpicxx -fopenmp myprog.cc``   |
   +---------------------+-------------------------------+----------------------------------------------+


CUDA
~~~~~~
NVIDIA GPUs are available as part of the Nightingale compute cluster. `CUDA <https://developer.nvidia.com/cuda-toolkit-archive>`_ is a parallel computing platform and programming model from NVIDIA for use on the GPUs. These GPUs support CUDA compute capability 2.0.

Load the CUDA Toolkit into your environment using the following module command: 

.. code-block:: 

   module load cuda/11.4.2

