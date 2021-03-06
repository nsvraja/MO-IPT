﻿                      An LA-SiGMA Software Distribution
                                MO-IPT package 
              Version 0.9 (Revision Placeholder) - May 2014
        Copyright 2014 Jawaharlal Nehru Centre for Advanced Scientific Research

                                
                This package contains code and sample data for generating
                Green's functions and self-energies of multi-orbital strongly
                correlated electron systems within dynamical mean field theory.
                The impurity solver is multi-orbital iterated perturbation
		theory. Detailed installation and operation instructions and
		other files may be found in the docs subdirectory. The code
		employs parallelization through message passing interface.
		For the latest version and other resources visit [blank,
		needs to be filled].
 
     ---------------------------------------------------------------------
                                       Description

     MO-IPT stands for multi-orbital iterated perturbation theory. The present code
implements the MO-IPT solver as described in Dasari et al [paper reference] within
the dynamical mean field theory (DMFT) framework and may be used to obtain single-
-particle spectra and self-energies for strongly correlated model Hamiltonians as
well as real materials with multiple orbital degrees of freedom. The code is implemented
for zero as well as finite temperatures. The impurity solver uses the second-order
self-energy in an ansatz motivated by the continued fraction expansion of the self-
-energy. The ansatz has certain free parameters that are chosen to satisfy high
frequency and the atomic limits. Since the ansatz reproduces low frequency Fermi liquid
behaviour and the band limit by construction, the MO-IPT is expected to be a reasonable
interpolating approximation. Naturally, the MO-IPT cannot be expected to be accurate
close to phase transitions, etc, where exact methods such as QMC and NRG would be
far more accurate. For extensive benchmarking of the method with continuous time
Monte Carlo and other methods, please see Dasari et al [paper reference]. One of the main
limitations of the code is that the Hund's coupling is presently implemented only as
a density-density interaction. The main merits of the MO-IPT is that it is fast,
numerically inexpensive, can deal with many orbitals, and provides real frequency
results at zero and finite temperature. The main motivation of our implementation
is to carry out first principles calculations of strongly correlated materials, so
the integration with band structure results (from e.g WIEN2K) is also implemented
in this set of codes.

The basic single-orbital IPT code was developed by N.S.Vidhyadhiraja (nsvraja@gmail.com).
The multi-orbital extension and MPI wrapper for k-summation were done by Nagamalleswararao
Dasari (nagamalleswararao.d@gmail.com). The optimization and benchmarks were carried out
by Dasari, Peng () and Wasim (wasimr.mondal@gmail.com) with the assistance of Mark
Jarrell (jarrellphysics@gmail.com), Juana Moreno (moreno@phys.lsu.edu) and N.S.Vidhyadhiraja. 

Detailed operating instructions, testing procedure and physics description of the test data
can be found in doc/manual.pdf. Sketchy details of the prerequisites, setup and operation
are given in docs/instructions.txt and a more detailed  manual is docs/manual.pdf.

    ---------------------------------------------------------------------

                                      Prerequisites
                  
MO-IPT has been tested on the following system:
                
(1) Ubuntu on Intel Xeon Hex-core E5645 (2.4GHz) with 12GB RAM
Linux 3.2.0-23-generic 36 -Ubuntu SMP Tue Apr 10 20:39:51 UTC 2012 x8664 x8664 x8664 GNU/Linux

DISTRIB ID=Ubuntu
DISTRIB RELEASE = 12.04
DISTRIB CODENAME=precise

Compiler information : mpif90 for MPICH version 3.0.3; ifort version 13.0.0
                
(2) Mageia on Intel Core i7-4765T (2GHz) with 8GB RAM
Linux 3.10.28-desktop-1.mga3 #1 SMP Sat Feb 1 16:15:10 UTC 2014 x86_64 x86_64 x86_64 GNU/Linux

Distributor ID: Mageia
Description:    Mageia 3
Release:        3
Codename:       thornicroft

Compiler information : mpif90 for MPICH2 version 1.2.1; ifort version 14.0.1


                

MO-IPT requires an MPI implementation e.g through MPICH2 or openmpi.
               
     ---------------------------------------------------------------------
     
                            Steps - Initial Setup and Simple Run 

These steps are for setup, and for running the code.
The sample commands are for a user with home directory
"/home/username" and who has unpacked the MO-IPT distribution
into directory MO-IPT, so that the path to the readme file
would be /home/username/MO-IPT/docs/README.
              

         
                 [ ] Install Prerequisites (MPI) 
                     Download the MO-IPT package.
                     Unpack using the following commands:
                      
                     tar -xzvf MO-IPT.tar.gz

		     Presumably you have already done this, otherwise you wouldn't be seeing this! 

              
                [ ]  Build the executable.
                     Commands:
                     
                     % cd /home/username/MO-IPT/src
                     % make  # This should result in an executable named MO-IPT.run
		     % cd ..

	       [ ]  For running the code with the sample data, we recommend using the script run.sh
	            
		    % chmod 744 run.sh
		    % ./run.sh

                    Users should refer to the example description given in the manual (docs/manual.pdf). 

       ---------------------------------------------------------------------

                            Operation

The MO-IPT package is used for finding the Green's functions and self-energies
of multi-orbital strongly correlated electron systems. The execution is through
command line as mentioned above. The input and output files and parameters are
mentioned in docs/manual.pdf. 

We recommend that users should save the output appearing on stdout (display).
This may be done for example by "mpirun -np $nprocs MO-IPT.run > screen.out"
or "mpirun -np $nprocs MO-IPT.run | tee screen.out". The screen output is 
very valuable for diagnostics. If pre-existing data is used to initialise a
run, then those files will be overwritten on completion. Convergence along
with DMFT loop numbers appears on the screen. Users can tune the tolerance for
convergence in the main.f program.
