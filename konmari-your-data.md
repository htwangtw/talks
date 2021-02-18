---
title: Data management
tags: Presentation
description: View the slide with "Slide Mode".
---

# Spark joy -- Life-Changing Magic of Tidying Up (Your Data)

<!-- Put the link to this slide here so people can follow -->
slide: https://hackmd.io/p/e4vuB8kCRuSv1irvpPtJwA

---

## Truck factor
The minimal number of people that have to be hit by a truck (or leave) to put a project in trouble.

----

Academic research projects commonly have a truck factor of 1. We cannot fix this, but we can reduce the risk when the truck is coming.

---

## Data management

- Risk management
- Easier for future access
- Back-up system

----

Aim of data organisation: when giving a new person access to the data, they can find all information they need.

----

- Frequent change logging
- Consistent file naming
- Metadata (description of variables)

---

## Example: research data and analysis
[Real example README file](https://hackmd.io/eN8FT2amTWySqhR36iimgQ)

---

## Anatomy of a data analysis project
```
my_project/
 ├── <name>_analysis/  analysis folder
 ├── data/             dataset; read-only once data aquired
 ├── docs/             Paperwork (ethics, consent form  etc.)
 ├── README            This file
 └── CHANGES           Changes related to this project
```
All folders should have their own README.

----

### Suggested content in `README`
- The organisation tree
- Description of basic rules (i.e. create analysis in your folder)

---

## `data/`
- Contain a README file and CHANGES log
    - Document means of labels, who worked on the project etc
- Contain source data, raw data, and derivatives
    - source data: data as to how they were collected
    - raw data: organised but **unprocessed** data
    - derivatives: processed data derived from raw data

----

### Organise your source data into raw data
- data collected in analysis unfriendly format
    - e.g. DICOM for MRI data but software uses NIFTI format
- lots of things can go wrong during testing
    - only experimenter(s) remember what is useable what is not
    - and they eventually forget
- get a clean copy for analysis for the ease of mind

-----

### Suggestion on organising data
- The latter something happens, closer should it be to the top
- Consistent file names
- Add README file anywhere you feel it's needed

---

## Scenario

* Two behavioural tasks
* Two sessions
    * one with ecg recording (session 1)
    * one with two run in a session (session 1 and 2)

----

### Inside `data/`
```
data/ ("top" level)
 ├── README
 ├── participants.tsv
 ├── task-sheep_description.txt
 ├── task-difficult_description.txt
 ├── sub-01/  # here's raw data
 │   ├── sub-01_ses-1_task-difficult_beh.tsv
 │   ├── sub-01_ses-1_task-difficult_recording-ecg_physio.smr
 │   ├── sub-01_ses-1_run-1_task-sheep_beh.tsv
 │   ├── sub-01_ses-1_run-2_task-sheep_beh.tsv
 │   ├── sub-01_ses-2_run-1_task-sheep_beh.tsv
 │   └── sub-01_ses-2_run-2_task-sheep_beh.tsv
 ├── derivatives/ # accuracy, mean reaction time etc
 │    ├── README
 │    ├── task-difficult_summary.tsv 
 │    └── task-sheep_summary.tsv
```

----

```
 └── code/
      ├── README
      ├── task-difficult/
      │    ├── data/   # here's source data
      │    ├── README
      │    ├── experiment_trials.tsv
      │    └── run_task.py
      └── task-sheep/
           ├── data/  # here's source data
           ├── README
           └── beep_beep_im_a_sheep.py
```

---

## I don't have time to set the rules/monitor project

----

**Brain Imaging Data Structure** has figured that out. 
![](https://i.imgur.com/iwh7Cod.png)
[BIDS specification]

----

- BIDS covers neuroimaging, behavioural, physiology, genetic, and **unspecified** data.
- Maintained by a community 
  (high truck factor == low risk)
- Run [BIDS Validator] to see if data fit the standard properly.

---

## Case study: ADIE data to BIDS
```
./
├── code/                           Code for datacollection, compiling raw data (sub-*), generating derivatives.
├── derivatives/                    Dereivatives of raw data (sub-*). 
├── phenotype/                      Assessment and questionnaire data. 
├── sourcedata/                     Collected data with own README. 
├── sub-*/[ses-<label>/]            BIDS raw data. Subject with multiple session will have an extra level. 
│   ├── anat/                       Anatomical scans (T1w, T2w).
│   ├── func/                       functional scans (tasks).
│   ├── dwi/                        Diffusion weighted imaging.
│   └── beh/                        Behavioural lab data.
├── CHANGES                         Changelog. Please update after any modification.
├── dataset_description.json        Descriptions of this dataset.
├── LICENSE                         Plain text license related to distribution of the dataset.
├── participants.tsv                Simple details for subjects. Each line is a subject.
└── README                          This file.
```

----

### Physiology data
- BIDS converts data to raw text and/or other open-source file format
- We use CED spike for physiology recording, closed-source file format
- Solution: 
    - save a BIDS compatible copy 
    - name the original file in BIDS standard as derivative

----

### Existing past analysis
- Add to the derivative with extra documentation 

----

### [ADIE data organisation aid](https://github.com/htwangtw/adie_ongoingthoughts/)

- Handle new incoming data (currently limited to a specific task and MRI data)
- Tested on different versions of Python
- Maintainable independent from the dataset by using synthetic data 

---

## Other incentives of using BIDS

----

### BIDS compatible tools

- Stable:
    - fMRIprep (minimal preprocessing tool)
    - C-PAC (maximal preprocessing tool)
    - MRIQC

See [Poldrack_2017] to understand why use minimal preprocessing tool.

----

### BIDS compatible tools

- Emerging:
    - EEGLAB-BIDS
    - dMRIprep (DWI)
    - fMRwhy (real-time neuralfeedback; SPM/MATLAB)

----

### Manegment perspective
- First-pass quality check (missing/corrupted files)
- Semantics of the projects (e.g. what is a session)

----

### New specifications in BIDS 1.5
- PET
- Genetic Descriptor

---

## Wrap up - checklist

- Do not touch the source/raw data. Back it up somewhere reasonable and keep a read-only copy.
- Have a plan BEFORE you start collecting it.
- Document everything. 


----

- Create the data you want to see in the word. 
- Before you start creating some crazy new schema, storage format or naming protocol, have a quick google or ask your colleagues. (i.e. BIDS)

Reference: [The Turing Way - Research Data Management]

---

## Thank you! :sheep: 

See link to slides for all the references.

[BIDS specification]: (https://bids-specification.readthedocs.io/en/stable/)

[BIDS examples]: (https://github.com/bids-standard/bids-examples/)

[BIDS validator]: (https://bids-standard.github.io/bids-validator/)

[Heudiconv: DICOM to BIDS converter]:(https://heudiconv.readthedocs.io/en/latest/)

[Poldrack_2017]: (https://doi.org/10.1038/nrn.2016.167)

[The Turing Way - Research Data Management]:(https://the-turing-way.netlify.app/reproducible-research/rdm.html)