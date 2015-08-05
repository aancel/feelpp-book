Using a backend {#TutorialBackend}
===============

<!-- toc -->

# Introduction

After the discretization process, one may have to solve a (non) linear
system. Feel++ interfaces with PETSc/SLEPc and Eigen3.  Consider this
system
$$A x = b $$

We call `Backend` an object that manages the solution strategy to
solve it. Some explanation are available \ref Solver and \ref
Preconditioner.


Feel++ provides a default backend that is mostly hidden to the final
user.  In many examples, you do not have to take care of the
backend. You change the backend behavior via the command line or
config files.  For example

```cpp
./feelpp_doc_mybackend --backend.pc-type=id
```

will use the identity matrix as a right preconditionner for the default backend.
The size of the preconditionner will be defined from the size of the A matrix.

If you try to solve a different system $$A_1 y= c$$ (in size) with the
same backend or the default without rebuilding it, it will fail.

```cpp
backend(_rebuild=true)->solve(_matrix=A1,_rhs=c,_sol=y);
```

Each of that options can be retrieved via the `\c --help-lib` argument in the command line.

## Non default Backend

You may need to manage more than one backend in an application: you
have different systems to solve and you want to keep some already
computed objects such as preconditioners.

- The default backend is in fact an unnamed backend: in order to
distinguish between backend you have to name them. for example   
   
  ***marker_opt***


- After that, you create the backend object:   

 ***marker_obj***

  Be careful, the backend's name has to match the name you gave at the options step.

- Then, you load meshes, creates spaces etc. At solve time, or you solve with the default backend:   

 ***marker_default***
 
 One of the important backend option is to be able to monitor the residuals and iteration count
```sh
./feelpp_tut_mybackend --pc-type=id --ksp-monitor=true --myBackend.ksp-monitor=true
```

- Finally you can create a named backend:   

*** marker_hm ***



The whole code example :   

## Code
!CODEFILE "code/09-mybackend.cpp" 
## Config file
!CODEFILE "code/09-mybackend.cfg"