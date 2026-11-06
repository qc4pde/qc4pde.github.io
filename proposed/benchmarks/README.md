
# QC4PDE: Benchmarks & Stewardship 

## Co-Chairs

* t.b.d., [contact]

* t.b.d., [contact]


## Purpose

The Benchmarks & Stewardship committee exists to define the benchmarks of relevance to the consortium. Its activities may include: 

* maintaining a *list of benchmark cases* in increasing levels of difficulty: *textbook* cases compare fundamentals, *stretch goals* pursue applications of scientific and industrial interest in phased and estimated projects, and *grand challenges* present out-year potentials

* establishing preferred *standards for publication*, including use of arXiv, open source code, and FAIR data

* establishing preferred *standards for comparability* of results (e.g. L2 fidelity) and the metadata around results (e.g. quantum machine calibration)

* maintaining a *catalog of results* which adhere to the preferred standards, linked to in its native location

* conducting *comparative studies* of cataloged results, publishing frameworks and findings, and projecting pathways to utility, informing future benchmark use cases


## Benchmark Formulation 

Benchmarks can be established along several axis: 

- *fidelity* relative to classical reference

- *size* of problem, in comparable units or as percentage of some defined problem

- *resources* required, including both quantum and classical, as well as interconnects and other operational considerations

- and finally, *wall-time performance*, as the consortium concedes any comparisons with a classical reference at this stage in the evolution of quantum computing for PDEs, yet encourages the collection and comparison of such data 


## Sample Benchmark Cases

**WORK IN PROGRESS**


* textbook 
    + CFD - compressible, linearized, low qubit/gate cases 
        - {2,3}-D Hele-Shaw
        - {1,2,3}-D supersonic diverging nozzle
        - 1D Sod shock tube
        - 2D lid-driven cavity
        - {1,2,3}-D viscous Burgers: sine IC
        - {2,3}-D irrotational flow {cylinder,airfoil}
        - {2,3}-D inviscid flow in {channel w bump, pipe w constriction}
        - {2,3}-D invicid flow over {airfoil}
        - {2,3}-D laminar flow in {channel,pipe}
        - {2,3}-D laminar flow over {airfoil}
        - 0D flame kinetics
    + [bio domain]
    + [other domain]

* stretch goals (w steps & estimation, roadmap alignment) 
    + CFD
        - 2D->3D: textbook cases but with higher resource needs
        - structural mechanics

* grand challenges
    + NASA 2030, large grids, high QC resource needs, (w advantage)
