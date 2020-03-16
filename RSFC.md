---
title: resting state functional connectivity
tags: Presentation
slideOptions:
  transition: 'fade'
---

# Trends in resting-state functional connectivity

Hao-Ting Wang
CISC Seminar Series
01/10/2019

---

Lots of Python-based tool promotion, no one paid me to do this.

---

## The golden age of open access dataset

----

## Just to name a few...

 - Autism Brain Imaging Dataset Exchange (ABIDE)
 - Human connectome project
 - UK Biobank
 - Healthy brain network
 - MyConnectome
 - The PRIMatE Data Exchange (PRIME-DE)

----

![](https://i.imgur.com/Jk3ZQYN.png =75%x)
[(Ridgway et al., 2006)](https://jeb.biologists.org/content/209/18/3621)


----

These initiatives all collected resting-state fMRI data.


---

## Road map
* What is resting-state functional connectivity?
* Common analysis approaches
* Notes on preprocessing
* Resources for analysis

---

## What is resting-state functional connectivity?

* The temporal correlation/**statistical dependency** between the time series of different brain regions.

----


* FC does not incorporate any knowledge or assumptions about the structure and mechanisms of the brain.

* Today I will cover functional connectivity calculated from correlation.

Note:
    More precisely - static functional connectivity.

----

![](https://i.imgur.com/LoMfw0X.png)
[(Courtsey to Pierre Bellec)](https://github.com/neurohackademy/2019_materials)

----

![](https://i.imgur.com/2NjdRUu.png)
[(Courtsey to Pierre Bellec)](https://github.com/neurohackademy/2019_materials)


----

![](https://i.imgur.com/aFGSzCg.png)
[(Courtsey to Pierre Bellec)](https://github.com/neurohackademy/2019_materials)

---

## Other types of connectivity measures
[See definition from Roebroeck et al., 2011](http://proceedings.mlr.press/v12/roebroeck11/roebroeck11.pdf)
* Anatomical (structural) connectivity
The  *physical* presence of an axonal projection from one brain area to another. 
* Effective  connectivity
Measures of *directed influence and causality* within the networks constrained by further assumptions
    
Note:
    See Friston, 1994 for the first proposal of functional connectivity

----

### Structural, functional, and effective connectivity

![](https://i.imgur.com/yPxPagD.png =75%x)
[(Rubinov & Sporns, 2010)](https://sph.umd.edu/sites/default/files/files/Rubinov_Sporns_2009.pdf)

Note:
    Macaque cortex
    See Rubinov & Sporns, 2010 for a neuroimaging focused review for  connectivity measures and network modelling

----

![](https://i.imgur.com/B7eeNH2.png =40%x)
[(Smith et al., 2019)](https://doi.org/10.1523/JNEUROSCI.2912-18.2019)

Note:
    Two higher-level clusters involving DMN grey matter network obtained using hierarchical clustering. a Left, structural DMN 1; right, DMN (Fox et al., 2009). b, structural DMN 2 was paired with executive, the GMN resembling the executive control RSN, to create a cluster comparable to the limbic precuneus functional network (right, adapted from Margulies et al., 2009). The two structural clusters in a and b made up the entire DMN and its negatively correlated network (top right).

---

### Rest vs Task

![](https://i.imgur.com/21zf9oD.png)

[(Smith et al., 2009)](https://doi.org/10.1073/pnas.0905267106)


Note:
    The resting-state encompasses a wide repertoire of cognitive states due to its uncontrolled nature.
    RSN - resting-state networks derived from ICA
    BM - BrainMap networks derived from ICA (meta-analysis network from activation based study)
    BrainMap is a large database of fMRI and PET brain activation studies

---

## Why study functional connectivity at rest?
* Basic organisation of the functional brain
* Freedom on the psychological question
* If collecting data, very little time required on set up
* Potentials as clinical/cognitive biomarker


---

## Common analysis approaches

* Seed-based approach
* Decomposition
* Clustering
* Other emerging approaches

---

## Seed-based functional connectivity

* seed voxels or regions of interest selected *a priori*
  *I am interested in the connectivity of PCC in the whole brain*

----

### First-level: functional connectivity map
![](https://i.imgur.com/LoMfw0X.png)
[(Courtsey to Pierre Bellec)](https://github.com/neurohackademy/2019_materials)

----

### Second-level: group-level statistics with GLM

* Group-level functional connectivity map (one-sample t-test)
  *Does the association between the seed and the whole brain exist on average?*
* Compare across groups
  *Given the correlation between the seed region and the whole-brain, seek the difference between the average map between group A and B*
  
* Add other group-level regressors (i.e. psychological measures)
  *Given the correlation between the seed region and the whole-brain, seek the correlation pattern associated with the regressors*

* Any analysis you can do with GLM...

Note:
    [FSL FEAT user guide](https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FEAT/UserGuide)

----

### Seed-based approach summary

* Simple and easily interpretable
* Freedom with the psychological measure as second-level regressors
* Heavily dictated by seed selection
* Only reveal one specific functional system at a time

---

## Decomposition

----

### ICA and PCA
![](https://i.imgur.com/JCUYGiv.png)

Note:
    https://mne.tools/0.15/manual/preprocessing/ica.html
    

----

### Seed-based approach revisit: dual regression

ICA derived network to replace seed-based

![](https://i.imgur.com/AA6l004.png =65%x)

[Paper (Nickerson et al. 2017)](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5346569/)



Note:
    Original poster [(Beckmann et al., 2009)](https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/DualRegression?action=AttachFile&do=get&target=CB09.pdf), Dual regression allows researchers to investigate individual and group differences in the structure of these networks, as well as to identify subject-specific networks based on networks identified at the group level.

---

## Clustering

![](https://i.imgur.com/YxMeH9Y.png)

Note:
[Source](https://arxiv.org/pdf/1812.11477.pdf)

----

* Common in the study of brain organisation
* Understand the clustering approach when selecting atlas for analysis

----

Online interactive tutorial
[Bootstrap Aggregation of Stable Clusters (BASC)](https://github.com/SIMEXP/tutorials-basc)

----

Yeo-Kieran 7 networks(2011) 
![](https://i.imgur.com/kyis9LU.png  =70%x)

----

Schaefer et al. (2017)
![](https://i.imgur.com/KbB9Hcb.jpg  =60%x)

----

Multi-session hierarchical Bayesian model (MS-HBM)
Kong et al. (2018)
![](https://i.imgur.com/rks8nNC.png =70%x)


----

Craddock et al. (2011)

![](https://i.imgur.com/HtZxPqh.png)

Note:
PCC functional connectivity using different atlas
![](https://i.imgur.com/yQTm0Ew.png =30%x)


---

## Gradient?

![](https://i.imgur.com/KuOp6aD.png =70%x)

[Margulies et al. (2015)](https://www.pnas.org/content/113/44/12574)

----

## Hippocampus gradient
![](https://i.imgur.com/KBQfAHx.png =80%x)

[Vos de Wael et al. (2018)](https://www.pnas.org/content/115/40/10154)

----


## Healthy control vs ASD
![](https://i.imgur.com/t1p9qqW.png)

[Hong et al. 2018](https://www.nature.com/articles/s41467-019-08944-1)


---

## Dynamic FC in resting state


![](https://i.imgur.com/yTaUFsW.jpg =60%x)
[Vidaurre et al, 2017](https://www.pnas.org/content/114/48/12827)

---

## Notes on preprocessing


---

## Motion in resting state

![](https://i.imgur.com/OCHTUtJ.png)
Group 1: less motion; group 10: a lot of motion

[Van Dijk et al 2012](https://doi.org/10.1016/j.neuroimage.2011.07.044)

Note:
    Readings:
    [Ciric et al (2017)](https://doi.org/10.1016/j.neuroimage.2017.03.020)
    [Caballero-Gaudes et al (2017)](https://doi.org/10.1016/j.neuroimage.2016.12.018)
    [Lindquist et al. (2019)](https://doi.org/10.1002/hbm.24528)

---

## General preprocessing steps

* Slice-time correction
* Head motion correction
* Skull stripping
* (Registration to standard space)

----

* Noise reduction
    * Nuisance regression (aCompcor, ICA-FIX, ICA-AROMA)
    * Band-pass filtering (0.01–0.1 Hz)

* Controversial
    * Global signal regression
    * Volume censoring (scrubbing) 

Note:
    Denoise methods comparison: [Parkes et al., 2018](https://www.sciencedirect.com/science/article/pii/S1053811917310972)


---

## Global signal regression

![](https://i.imgur.com/QjYLPvQ.png)


Note:
    [Murphy et al (2009)](http://nwkpsych.rutgers.edu/~jose/courses/578_mem_learn/2012/readings/Murphy_2009.pdf)

---

## Volume censoring (scrubbing)

![](https://i.imgur.com/KTPs5ny.png)
Remove volumes with severe motion.

Note:
    Power et al (2012, 2013, 2014, 2015)
    [C-PAC documentation on noise handling](https://fcp-indi.github.io/docs/user/nuisance.html)

---

### Volume or Surface space?

![](https://emmarobinson01.files.wordpress.com/2015/10/whysurface.png)

----

![](https://cdn.elifesciences.org/articles/32992/elife-32992-fig2-v2.jpg =70%x)

[Bijsterbosch et al (2018)](https://elifesciences.org/articles/32992)

Note:
[Tucholka 2012 Volume vs Surface](https://hal.archives-ouvertes.fr/hal-00723437v3/document)

[Emma Robinson's blog on Bijsterbosch et al (2018)](https://emmarobinson01.com/2017/10/31/are-variations-in-functional-connectivity-strength-driven-by-variations-in-spatial-topography/)


---

### My genuine advice

* Read up the latest literature and follow published preprocessing protocol.
* Use software with detailed documentation on every step to learn about preprocessing.
* Do one preprocessing with GSR and the other without GSR.

* Advance: Consider surface-based analysis 

----

### But I am not interested in preprocessing...

Consider [fmriprep](https://fmriprep.readthedocs.io/en/stable/index.html)


----

![](https://i.imgur.com/n4F9v8c.png=60%x)

---

## Resources and tutorials

----

### Toolboxes

Good for learning details of preprocessing.
* CONN (preprocessing/seed-based/graph-based measure; SPM-based)
* CPAC (preprocessing/seed-based/graph-based measure; Python wrapper of many softwares)

For lazy people (good documentation)
* fmriprep (one-liner preprocessing)

Note:
Human connectome project preprocessing pipeline
https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3720813/

----

* FSLNet (Network Modelling)
* FSL - MELODIC (ICA)
* BrainSpace (Connectomic gradient)

----

### Group-level atlas
* Yeo-Krienen 7/17 networks
* Schaefer parcellations
* Craddock atlas 
* Glasser atlas (multimodal)

### Parcellation tools
* Nilearn brain parcellation tools

---

### Tutorials

[Jeanette Mumford's Youtube channel](https://www.youtube.com/channel/UCZ7gF0zm35FwrFpDND6DWeA)
She still answers questions on Tumblr and Facebook group

[Andrew Jahn](https://www.andysbrainblog.com/)
Cover most of the main stream softwares with great Youtube videos.


---

## Thanks!

H.Wang@bsms.ac.uk
Link to the slides and notes: 
https://hackmd.io/@haotingwang/BkgXygbwS