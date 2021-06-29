## Overview and objective: 
The working group’s goal is to assemble and distribute scientific data sets relevant to a scientific campaign in a systematic manner, and pose quantifiable targets (“science benchmark”). A benchmark involves (i) a data set, (ii) objective criteria to meet, and (iii) a reference implementation. The objective criteria depends on the scientific problem at hand. The metric should be well defined on the data but could come from a diverse set of measures (one or more of: accuracy targets, top-1 or 5% error, time to convergence, cross-validation rates, confusion matrices, type-1/type-2 error rates, inference times, surrogate accuracy, control stability measure, etc.).

## Benchmarks
1) <h3>CloudMask</h3>
2) <h3>STEMDL</h3>

State of the art scanning transmission electron microscopes (STEM) produce focused electron beams with atomic dimensions and allow to capture diffraction patterns arising from the interaction of incident electrons with nanoscale material volumes. Backing out the local atomic structure of said materials requires compute- and time-intensive analyses of these diffraction patterns (known as convergent beam electron diffraction, CBED). Traditional analyses of CBED requires iterative numerical solutions of partial differential equations and comparison with experimental data to refine the starting material configuration. This process is repeated anew for every newly acquired experimental CBED pattern and/or probed material. 

In this [benchmark](https://github.com/at-aaims/stemdl-benchmark), we used newly developed multi-GPU and multi-node electron scattering simulation codes [[1]](https://www.osti.gov/biblio/1631694-namsa) on the Summit supercomputer to generate CBED patterns from over 60,000 materials (solid-state materials), representing nearly every known crystal structure. A scaled-down version of this data [[2]](https://doi.ccs.ornl.gov/ui/doi/70) is used for one of the data challenges [[3]](https://smc-datachallenge.ornl.gov/challenges-2020/challenge-2-2020/) at SMC 2020 conference, and the overarching goals are to: (1) explore the suitability of machine learning algorithms in the advanced analysis of CBED and (2) produce a machine learning algorithm capable of overcoming intrinsic difficulties posed by scientific datasets. 

A [data](https://doi.ccs.ornl.gov/ui/doi/70) sample from this data set is given by a 3-d array formed by stacking various CBED patterns simulated from the same material at different distinct material projections (i.e. crystallographic orientations). Each CBED pattern is a 2-d array with float 32-bit image intensities. Associated with each data sample in the data set is a host of material attributes or properties which are, in principle, retrievable via analysis of this CBED stack. Of note are (1) 200 crystal space groups out of 230 unique mathematical discrete space groups and (2) local electron density which governs material’s property. 

This benchmark consists of 2 tasks: classification for crystal space groups and reconstruction for local electron density, the baseline implementation of which are provided in [[4]](https://link.springer.com/chapter/10.1007%2F978-3-030-63393-6_30) and [[5]](https://arxiv.org/abs/1909.11150).

3) <h3>CANDLE-UNO</h3> 

## Reference Implementation: 
The reference implementation is primarily to demonstrate feasibility, show how the data is represented, help address any interpretation considerations, and potentially trigger initial ideas on how the benchmark can be improved.

## Respondents: 
At the present time, we expect respondents to submit the results of their run, and should provide justification in the form of documentation (e.g., a technical manuscript or source code with run instructions). We are exploring setting this up as a “pull request” based contribution mechanism.

<img width="717" alt="Screen Shot 2021-06-23 at 3 49 56 PM" src="https://user-images.githubusercontent.com/24704023/123159172-b08aa500-d43a-11eb-99f4-61c4193d5e69.png">

