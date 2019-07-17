# Transient Wall Module
This module was developed by [ATA Engineering](http://www.ata-e.com) as an 
add-on to the Loci/CHEM computational fluid dynamics (CFD) solver. The module 
can be used to extend the **viscousWall** boundary condition to allow it to 
specify a time varying boundary condition. It is intended to be used with 
transient flow simulations that use either an adiabatic, isothermal, or 
isoflux boundary condition for the wall.

# Dependencies
This module depends on both Loci and CHEM being installed. Loci is an open
source framework developed at Mississippi State University (MSU) by Dr. Ed 
Luke. The framework provides a rule-based programming model and can take 
advantage of massively parallel high performance computing systems. CHEM is a 
full featured open source CFD code with finite-rate chemistry built on the Loci 
framework. CHEM is export controlled under the International Traffic In Arms 
Regulations (ITAR). Both Loci and CHEM can be obtained from the 
[SimSys Software Forum](http://www.simcenter.msstate.edu) hosted by MSU. This
module also requires a compiler with C++11 support.

# Installation Instructions
First Loci and CHEM should be installed. The **LOCI_BASE** environment
variable should be set to point to the Loci installation directory. The 
**CHEM_BASE** environment variable should be set to point to the CHEM 
installation directory. The installation process follows the standard 
make, make install procedure.

```bash
make
make install
```

# Usage
First the module must be loaded at the top of the **vars** file. 
Any **viscousWall** boundaries conditions may be tagged with the 
**transient** tag. The **adiabatic**, **Twall**, or **qwall** options can be
used to specify the name of a file which contains the time varying wall data.

```
loadModule: transientWall

boundary_conditions: <BC_1=viscousWall(transient, Twall="wall.dat"), ...>
```

In the above example, the **wall.dat** file would look something like below. The
first line is the number of time points to follow. The following lines list
the time, wall temperature, and wall velocity for the boundary. For an isoflux
wall the heat flux is specified instead of the wall temperature. For an 
adiabatic wall, only the velocity is specified. In all cases, the data should
be input in SI units.

```
3
0 400 0 0 0
0.1 500 0 0 0
0.2 600 10 0 0
```
