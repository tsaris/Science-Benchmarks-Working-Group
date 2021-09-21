# Overview and objective: 
Encourage and support the curation of large-scale experimental and scientific datasets and the engineering of ML benchmarks operating on those datasets. The WG will engage with scientists, academics, national laboratories, such as synchrotrons, in securing, engineering, curating, and publishing datasets and machine learning benchmarks that operate on experimental scientific datasets. This will entail working across different domains of sciences, including material, life, environmental, and earth sciences, particle physics, and astronomy, to mention a few. We will include traditional observational and computer-generated data.

Although scientific data is widespread, curating, maintaining, and distributing large-scale, useful datasets for public consumption is a challenging process, covering various aspects of data (from FAIR principles to distribution to versioning). With large data products, various ML techniques have to be evaluated against different architectures and different datasets. Without these benchmarking efforts, the community has no clear pathway for utilizing these advanced models. We expect that the collection will have significant tutorial value as examples from one field, and one observational or computational experiment can be modified to advance other fields and experiments.

The working group’s goal is to assemble and distribute scientific data sets relevant to a scientific campaign in a systematic manner, and pose quantifiable targets (“science benchmark”). A benchmark involves (i) a data set, (ii) objective criteria to meet, and (iii) a reference implementation. The objective criteria depends on the scientific problem at hand. The metric should be well defined on the data but could come from a diverse set of measures (one or more of: accuracy targets, top-1 or 5% error, time to convergence, cross-validation rates, confusion matrices, type-1/type-2 error rates, inference times, surrogate accuracy, control stability measure, etc.).


# Meeting Schedule: 
Bi-weekly on Wednesay from 8:00-9:00AM Pacific.

# Mailing List:
[science@googlegroups.com](science@googlegroups.com)

# Working Group Resources:
[Google Drive](https://drive.google.com/drive/u/4/folders/19FK3PXa9DVIe9j7FawwihCb47F0V_nlC)

# Working Group Chair:
Geoffrey Fox ([gcfexchange@gmail.com](gcfexchange@gmail.com)) [CV](https://luddy.indiana.edu/contact/profile/?profile_id=203)

Tony Hey ([tony.hey@stfc.ac.uk](tony.hey@stfc.ac.uk)) [CV](https://www.scd.stfc.ac.uk/Pages/Tony-Hey.aspx)

Jeyan Thiyagalingam ([t.jeyan@stfc.ac.uk](t.jeyan@stfc.ac.uk)) [CV](https://www.scd.stfc.ac.uk/Pages/sciml-profile-jeyan.aspx)

# Benchmarks

| Benchmark  | Science | Task | Owner Institute | Specific Benchmark Targets |
| ------------- | ------------- | ------------- | ------------- | ------------- |
| CloudMask  | Climate | Segmentation | RAL | [link specifis cloudmask](#cloudmask-specific-benchmark-targets) |
| STEMDL  | Material | Classification | ORNL |  [link specifis stemdl](#stemdl-specific-benchmark-targets) |
| CANDLE-UNO  | Medicine | Classification | ANL | [link specifis candle-uno](#candle-uno-specific-benchmark-targets) |
| TEvolOp Forecasting  | Earthquake | Regression | Indiana |  [link specifis tevolop](#tevolop-specific-benchmark-targets) |


### CloudMask (Segmentation)

Estimation of sea surface temperature (SST) from space-borne sensors, such as satellites, is crucial for a number of applications in environmental sciences. One of the aspects that underpins the derivation of SST is cloud screening, which is a step that marks each and every pixel of thousands of satellite imageries as containing cloud or clear sky, historically performed using either thresholding or Bayesian methods.

This benchmark focuses on using a machine learning-based model for masking clouds, in the Sentinel-3 satellite, which carries the Sea and Land Surface Temperature Radiometer (SLSTR) instrument. More specifically, the benchmark operates on multispectral image data. The baseline implementation is a variation of the U-Net deep neural network. The benchmark includes two datasets of DS1-Cloud and DS2-Cloud, with sizes of 180GB and 4.9TB, respectively. Each dataset is made up of two parts: reflectance and brightness temperature. The reflectance is captured across six channels with the resolution of 2400 x 3000 pixels, and the brightness temperature is captured across three channels with the resolution of 1200 x 1500 pixels.

#### CloudMask Specific Benchmark Targets:
1. Scientific objective(s):
   * Formula: 
   * Score:
2. Data
   * Download:
   * Input Size:
   * Training samples:
   * Validation samples:
3. Baseline implementation
   * Model: 
   * Reference Code: 
   * Run Instructions: 
4. Hardware systems explored and performance:
   * Summit:
   * ThetaGPU:
   * RAL: 
5. Example improvements:
   * ...

### STEMDL (Classification)

State of the art scanning transmission electron microscopes (STEM) produce focused electron beams with atomic dimensions and allow to capture diffraction patterns arising from the interaction of incident electrons with nanoscale material volumes. Backing out the local atomic structure of said materials requires compute- and time-intensive analyses of these diffraction patterns (known as convergent beam electron diffraction, CBED). Traditional analyses of CBED requires iterative numerical solutions of partial differential equations and comparison with experimental data to refine the starting material configuration. This process is repeated anew for every newly acquired experimental CBED pattern and/or probed material. 

In this [benchmark](https://github.com/at-aaims/stemdl-benchmark), we used newly developed multi-GPU and multi-node electron scattering simulation codes [[1]](https://www.osti.gov/biblio/1631694-namsa) on the Summit supercomputer to generate CBED patterns from over 60,000 materials (solid-state materials), representing nearly every known crystal structure. A scaled-down version of this data [[2]](https://doi.ccs.ornl.gov/ui/doi/70) is used for one of the data challenges [[3]](https://smc-datachallenge.ornl.gov/challenges-2020/challenge-2-2020/) at SMC 2020 conference, and the overarching goals are to: (1) explore the suitability of machine learning algorithms in the advanced analysis of CBED and (2) produce a machine learning algorithm capable of overcoming intrinsic difficulties posed by scientific datasets. 

A [data](https://doi.ccs.ornl.gov/ui/doi/70) sample from this data set is given by a 3-d array formed by stacking various CBED patterns simulated from the same material at different distinct material projections (i.e. crystallographic orientations). Each CBED pattern is a 2-d array with float 32-bit image intensities. Associated with each data sample in the data set is a host of material attributes or properties which are, in principle, retrievable via analysis of this CBED stack. Of note are (1) 200 crystal space groups out of 230 unique mathematical discrete space groups and (2) local electron density which governs material’s property. 

This benchmark consists of 2 tasks: classification for crystal space groups and reconstruction for local electron density, the baseline implementation of which are provided in [[4]](https://link.springer.com/chapter/10.1007%2F978-3-030-63393-6_30) and [[5]](https://arxiv.org/abs/1909.11150).

#### STEMDL Specific Benchmark Targets:
1. Scientific objective(s):
   * Formula: F1 score on validation data
   * Score: 0.9 considered converged
2. Data
   * Download: https://doi.ccs.ornl.gov/ui/doi/70
   * Input Size: (128, 128, 3)
   * Training samples: 138.7K
   * Validation samples: 48.4
3. Baseline implementation
   * Model: ResNet-50
   * Reference Code: https://github.com/at-aaims/stemdl-benchmark
   * Run Instructions: https://github.com/at-aaims/stemdl-benchmark#quickstart
4. Hardware systems explored and performance:
   * Summit: 40min with ResNet50 on 60 V100 GPUs
   * ThetaGPU:
   * RAL: 
5. Example improvements:
   * Variation of ResNet pre-trained models



### CANDLE-UNO

CANDLE (Exascale Deep Learning and Simulation Enabled Precision Medicine for Cancer) project aims to implement deep learning architectures that are relevant to problems in cancer. These architectures address problems at three biological scales: cellular (Pilot1 P1), molecular (Pilot P2) and population (Pilot3).

Pilot1 (P1) benchmarks are formed out of problems and data at the cellular level. The high level goal of the problem behind the P1 benchmarks is to predict drug response based on molecular features of tumor cells and drug descriptors. Pilot2 (P2) benchmarks are formed out of problems and data at the molecular level. The high level goal of the problem behind the P2 benchmarks is molecular dynamic simulations of proteins involved in cancer, specifically the RAS protein. Pilot3 (P3) benchmarks are formed out of problems and data at the population level. The high level goal of the problem behind the P3 benchmarks is to predict cancer recurrence in patients based on patient related data.

Uno application from Pilot1 (P1):  The goal of Uno is to predict tumor response to single and paired drugs, based on molecular features of tumor cells across multiple data sources. Combined dose response data contains sources: [‘CCLE’ ‘CTRP’ ‘gCSI’ ‘GDSC’ ‘NCI60’ ‘SCL’ ‘SCLC’ ‘ALMANAC.FG’ ‘ALMANAC.FF’ ‘ALMANAC.1A’]. Uno implements a deep learning architecture with 21M parameters in TensorFlow framework in Python. The code is publicly available on [GitHub](https://github.com/ECP-CANDLE/Benchmarks/tree/develop/Pilot1/Uno). The script in this repository downloads all required datasets. The primary metric to evaluate this applications is throughput (samples per second).  More details on running Uno can be found [here](https://github.com/ECP-CANDLE/Benchmarks/blob/develop/Pilot1/Uno/README.AUC.md).

#### CANDLE-UNO Specific Benchmark Targets:
1. Scientific objective(s):
   * Formula: 
   * Score:
2. Data
   * Download:
   * Input Size:
   * Training samples:
   * Validation samples:
3. Baseline implementation
   * Model: 
   * Reference Code: 
   * Run Instructions: 
4. Hardware systems explored and performance:
   * Summit:
   * ThetaGPU:
   * RAL: 
5. Example improvements:
   * ...

### TEvolOp Earthquake Forecasting

Time series are seen in many scientific problems and many of them are geospatial -- functions of space and time and this benchmark illustrates this type. Some time series have a clear spatial structure that for example strongly relates nearby space points. The problem chosen is termed a spatial bag where there is spatial variation but it is not clearly linked to the geometric distance between spatial regions. In contrast, traffic-related time series have a strong spatial structure. We intend benchmarks that cover a broad range of problem types.

The earthquake data comes from USGS and we have chosen a 4 degrees of Latitude (32 to 36 N) and 6 degrees of Longitude (-120 to -114) region covering Southern California. The data runs from 1950 to the present day and is presented as events: magnitude, ground location, depth, and time. We have divided the data into time and space bins. The time interval is daily but in our reference models, we accumulate this into fortnightly data. Southern California is divided into a 40 by 60 grid of 0.1 by 0.1-degree “pixels” which corresponds roughly to squares with an 11 km side, The dataset also includes an assignment of pixels to known faults and a list of the largest earthquakes in that region from 1950 until today. We have chosen various samplings of the dataset to provide both input and predicted values. These include time ranges from a fortnight up to 4 years. Further, we calculate summed magnitudes and depths and counts of significant quakes (magnitude > 3.29). Other easily available quantities are powers of quake energy (using Energy ~ 101.5m where m is magnitude). Quantities are “Energy averaged” when there are multiple events in a single space-time bin except for simple event counts. 

Current reference models are a basic LSTM recurrent neural network and a modification of the original science transformer. Details can be found at [https://docs.google.com/presentation/d/1ykYnX0uvxPE-M-c-Tau8irU3IqYuvj8Ws8iUqd5RCxQ/edit?usp=sharing](https://docs.google.com/presentation/d/1ykYnX0uvxPE-M-c-Tau8irU3IqYuvj8Ws8iUqd5RCxQ/edit?usp=sharing), and [https://www.researchgate.net/publication/346012611_DRAFT_Deep_Learning_for_Spatial_Time_Series](https://www.researchgate.net/publication/346012611_DRAFT_Deep_Learning_for_Spatial_Time_Series)

#### TEvolOp Specific Benchmark Targets:
1. Scientific objective(s):
   * Formula: 
   * Score:
2. Data
   * Download:
   * Input Size:
   * Training samples:
   * Validation samples:
3. Baseline implementation
   * Model: 
   * Reference Code: 
   * Run Instructions: 
4. Hardware systems explored and performance:
   * Summit:
   * ThetaGPU:
   * RAL: 
5. Example improvements:
   * ...

# Reference Implementation: 
The reference implementation is primarily to demonstrate feasibility, show how the data is represented, help address any interpretation considerations, and potentially trigger initial ideas on how the benchmark can be improved.

# Respondents: 
At the present time, we expect respondents to submit the results of their run, and should provide justification in the form of documentation (e.g., a technical manuscript or source code with run instructions). We are exploring setting this up as a “pull request” based contribution mechanism.

<img width="717" alt="Screen Shot 2021-06-23 at 3 49 56 PM" src="https://user-images.githubusercontent.com/24704023/123159172-b08aa500-d43a-11eb-99f4-61c4193d5e69.png">
