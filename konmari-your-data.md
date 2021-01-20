---
title: BIDS data
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

Academic research projects commonly has a truck factor of 1. We cannot fix this, but we can reduce the risk. 

---

## Data managenet

- Sanity
- Risk management
- Reusable data
- Easier for future colaboration

---

Aim of data organisation: when giving a new person access to the data, they can find all information they need.

---

- Frequent change logging
- Consistent file naming

---

## Project folder
[Real example README file](https://hackmd.io/eN8FT2amTWySqhR36iimgQ)

----

### Organisation
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
- Description of basic rules (i.e. create analysis in your own folder)

---

## `data/`
- Contain a README file and CHANGES log
    - Document means of labels, who worked on the project etc
- Contain source data, raw data, and derivatives
    - source data: data as how they were collected
    - raw data: organised but **unprocessed** data
    - derivatives: processed data derived from raw data

----

### Organise your source data into raw data
- data collected in analysis unfriendly format
    - e.g. DICOM for MRI data but software uses NIFTY format
- lots of things can go wrong during testing
    - only experimenter remeber what is useable what is not
    - and they eventually forgets
- get a clean copy for analysis for the ease of mind

----

### Suggestion on organising data
- The latter something happen, closer should it be to the top
- Consistent file names
- Add README file any where you feel it's needed

----

Scenario: two behavioural task, two sessions, one with ecg recording, one with two run in a session

---- 

Example

```
data/ ("top" level)
 ├── README
 ├── participants.tsv
 ├── sub-01/  # here's raw data
 │   ├── sub-01_ses-1_task-difficult_beh.tsv
 │   ├── sub-01_ses-1_task-difficult_recording-ecg_physio.smr
 │   ├── sub-01_ses-1_run-1_task-sheep_beh.tsv
 │   ├── sub-01_ses-1_run-2_task-sheep_beh.tsv
 │   ├── sub-01_ses-2_task-difficult_beh.tsv 
 │   ├── sub-01_ses-2_task-difficult_recording-ecg_physio.smr
 │   ├── sub-01_ses-2_run-1_task-sheep_beh.tsv
 │   └── sub-01_ses-2_run-2_task-sheep_beh.tsv
 ├── derivatives/ # accuracy, mean reaction time etc
 │    ├── README
 │    ├── task-difficult_summary.tsv 
 │    └── task-sheep_summary.tsv
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

## I don't have a lab manager to set the rules / monitor project

---

Don't worry. **Brain Imaging Data Structure** has figured that out. 
![](https://i.imgur.com/iwh7Cod.png)

---

- BIDS covers neuroimaging, behavioural, physiology, genetic, and **unspecified** data.
- Maintained by a community 
  (high truck factor == low risk)
- Run [BIDS Validator](https://bids-standard.github.io/bids-validator/) to see if RA organised the data properly.

----

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
├── CHANGES                         Change log. Please update after any modification.
├── dataset_description.json        Descriptions of this dataset.
├── LICENSE                         Plain text license related to distribution of the dataset.
├── participants.tsv                Simple details for subjects. Each line is a subject.
└── README                          This file.
```

----

### Physiology data
- BIDS converts data to raw text and/or other open source file format
- We use CED spike for physiology recording, closed-source file format
- Solution: 
    - save a BIDS competible copy 
    - name the original file in BIDS standard as derivative

----

### Existing past analysis
- Add to derivative with extra documentation 

----

### [ADIE data organisation aid](https://github.com/htwangtw/adie_ongoingthoughts/)

- Handle new incoming data (currently limited to a specific task and MRI data)
- Tested on different versions of Python
- Maintainable independent from the dataset by using synthatic data 

---

### Wrap up

- Decide the organisation system early on and stick to it
- README file explaining the at the top level
- Use BIDS if you don't have a (working) system in place

---

### Thank you! :sheep: 

Resources:
[BIDS specification](https://bids-specification.readthedocs.io/en/stable/)
[BIDS examples](https://github.com/bids-standard/bids-examples/)
[BIDS validator](https://bids-standard.github.io/bids-validator/)
[Heudiconv: DICOM to BIDS MRI converter](https://heudiconv.readthedocs.io/en/latest/)