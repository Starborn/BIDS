# The BIDS Tool Ecosystem -- A Plain-Language Guide and Tutorial Map

**What every neuroimaging and neurophysiology analysis tool does, why it does it, and how to run it without Docker**



[View the interactive ecosystem map](https://starborn.github.io/BIDS)

SEARCH THIS PAGE FOR 'MODULE SEQUENCE' TO SEE THE PLAN
**[Jump to module sequence](#module-sequence-mri-focus-phase-1)**

Module 07 (Functional Connectivity) Learning is built 
07  Functional Connectivity    -- [Interactive module](https://starborn.github.io/BIDS/module-07-connectivity.html) [LIVE]


Version 0.2 -- May 2026
[W3C AIKR CG](https://www.w3.org/community/aikr/)


**Project home**: [github.com/Starborn/BIDS](https://github.com/Starborn/BIDS)
**OHBM Hackathon 2026**: [Issue #24](https://github.com/ohbm/hackathon2026/issues/24)

---

## Key Resources

| Resource | URL | What it is |
|---|---|---|
| BIDS Homepage | [bids.neuroimaging.io](https://bids.neuroimaging.io/) | Central portal for the standard |
| BIDS Specification (v1.11.1) | [bids-specification.readthedocs.io](https://bids-specification.readthedocs.io/en/stable/) | The definitive spec document |
| Awesome BIDS | [bids-standard.github.io/awesome-bids](https://bids-standard.github.io/awesome-bids/) | Community-curated catalogue of all tools |
| BIDS Starter Kit | [bids-standard.github.io/bids-starter-kit](https://bids-standard.github.io/bids-starter-kit/) | Getting started guide |
| BIDS Apps | [bids.neuroimaging.io/tools/bids-apps.html](https://bids.neuroimaging.io/tools/bids-apps.html) | Containerized analysis pipelines |
| BIDS Converters | [bids.neuroimaging.io/tools/converters.html](https://bids.neuroimaging.io/tools/converters.html) | Data format converters |
| BIDS Validator | [bids-standard.github.io/bids-validator](https://bids-standard.github.io/bids-validator/) | Browser-based dataset validator |
| OpenNeuro | [openneuro.org](https://openneuro.org/) | 1000+ open BIDS datasets |
| BIDS Extension Proposals | [bids.neuroimaging.io/get_involved.html](https://bids.neuroimaging.io/get_involved.html) | Proposed extensions |
| BIDS Specification (GitHub) | [github.com/bids-standard/bids-specification](https://github.com/bids-standard/bids-specification) | Spec source code |
| BIDS Website (GitHub) | [github.com/bids-standard/bids-website](https://github.com/bids-standard/bids-website) | Website source code |
| Awesome BIDS (GitHub) | [github.com/bids-standard/awesome-bids](https://github.com/bids-standard/awesome-bids) | Tool catalogue source |


---

## About this project

The [Brain Imaging Data Structure (BIDS)](https://bids.neuroimaging.io/) is a standard way to organize brain imaging and neurophysiology data so that software tools can automatically find and process it. Over the past decade, an ecosystem of 60+ tools has grown around this standard, covering 13 data modalities. The problem is that the ecosystem's own documentation is nearly impenetrable -- the official [BIDS Apps page](https://bids.neuroimaging.io/tools/bids-apps.html) shows Docker build status badges rather than explaining what each tool actually does.

This document aims to provide  *please help to build it:

1. A plain-language explanation of every BIDS-supported modality and the tools that serve it
2. For MRI tools (the most mature modality) -- what scientific question each tool answers, what math it uses, and what goes in and comes out
3. An assessment of whether each function can run in a browser without Docker
4. An architectural blueprint for "BIDS Academy" -- a browser-based learning environment where each analysis function comes with a tutorial covering the science, the math, and the code

**Scope note**: The detailed tool-by-tool breakdowns (Layers 3-8 below) currently focus on MRI-based tools. The architecture is designed to accommodate all 13 BIDS modalities in subsequent phases.


---

## The Full BIDS Modality Landscape

The [BIDS Specification v1.11.1](https://bids-specification.readthedocs.io/en/stable/) supports **13 data modalities**. Each has its own chapter in the spec, its own converter tools, and (for most) its own analysis pipelines.

### Overview of All Modalities

| # | Modality | Spec chapter | Signal type | Primary converters | Primary analysis tools | Maturity |
|---|---|---|---|---|---|---|
| 1 | **MRI** (Magnetic Resonance Imaging) | [Spec](https://bids-specification.readthedocs.io/en/stable/modality-specific-files/magnetic-resonance-imaging-data.html) | Radio frequency / magnetic fields | [dcm2niix](https://github.com/rordenlab/dcm2niix), [HeuDiConv](https://github.com/nipy/heudiconv), [BIDScoin](https://bidscoin.readthedocs.io/), [ezBIDS](https://brainlife.io/docs/using_ezBIDS/) | [fMRIPrep](https://fmriprep.org/), [MRIQC](https://mriqc.readthedocs.io/), [FreeSurfer](https://surfer.nmr.mgh.harvard.edu/), [SPM](https://www.fil.ion.ucl.ac.uk/spm/), [MRtrix3](https://www.mrtrix.org/), [nilearn](https://nilearn.github.io/) | Mature |
| 2 | **MEG** (Magnetoencephalography) | [Spec](https://bids-specification.readthedocs.io/en/stable/modality-specific-files/magnetoencephalography.html) | Magnetic fields from neural currents | [MNE-BIDS](https://mne.tools/mne-bids/), [FieldTrip](https://www.fieldtriptoolbox.org/example/bids/), [Biscuit](https://macquarie-meg-research.github.io/Biscuit/) | [MNE-Python](https://mne.tools/), [FieldTrip](https://www.fieldtriptoolbox.org/) | Mature |
| 3 | **EEG** (Electroencephalography) | [Spec](https://bids-specification.readthedocs.io/en/stable/modality-specific-files/electroencephalography.html) | Electrical potentials from scalp | [MNE-BIDS](https://mne.tools/mne-bids/), [EEGLAB](https://eeglab.org/tutorials/04_Import/BIDS.html), [FieldTrip](https://www.fieldtriptoolbox.org/example/bids/), [sovabids](https://sovabids.readthedocs.io/) | [MNE-Python](https://mne.tools/), [EEGLAB](https://eeglab.org/), [FieldTrip](https://www.fieldtriptoolbox.org/) | Mature |
| 4 | **iEEG** (Intracranial EEG) | [Spec](https://bids-specification.readthedocs.io/en/stable/modality-specific-files/intracranial-electroencephalography.html) | Electrical potentials from implanted electrodes | [MNE-BIDS](https://mne.tools/mne-bids/), [EEG2BIDS](https://github.com/aces/EEG2BIDS) | [MNE-Python](https://mne.tools/) | Mature |
| 5 | **PET** (Positron Emission Tomography) | [Spec](https://bids-specification.readthedocs.io/en/stable/modality-specific-files/positron-emission-tomography.html) | Gamma rays from radiotracer decay | Modality-specific DICOM converters | [PETSurfer](https://surfer.nmr.mgh.harvard.edu/fswiki/PetSurfer), kinetic modeling tools | Established |
| 6 | **fNIRS** (functional Near-Infrared Spectroscopy) | [Spec](https://bids-specification.readthedocs.io/en/stable/modality-specific-files/near-infrared-spectroscopy.html) | Near-infrared light absorption | [MNE-BIDS](https://mne.tools/mne-bids/) | [MNE-NIRS](https://mne.tools/mne-nirs/) | Established |
| 7 | **Microscopy** | [Spec](https://bids-specification.readthedocs.io/en/stable/modality-specific-files/microscopy.html) | Light / electron beams | Modality-specific | Image analysis tools | Newer |
| 8 | **MRS** (Magnetic Resonance Spectroscopy) | [Spec](https://bids-specification.readthedocs.io/en/stable/modality-specific-files/magnetic-resonance-spectroscopy.html) | Chemical concentration spectra | [spec2nii](https://github.com/wtclarke/spec2nii) | [FSL-MRS](https://open.win.ox.ac.uk/pages/fsl/fsl_mrs/), [Osprey](https://schorschinho.github.io/osprey/) | Newer |
| 9 | **Motion** | [Spec](https://bids-specification.readthedocs.io/en/stable/modality-specific-files/motion.html) | Position / orientation sensors | Modality-specific | Biomechanics tools | Newer |
| 10 | **EMG** (Electromyography) | [Spec](https://bids-specification.readthedocs.io/en/stable/modality-specific-files/electromyography.html) | Electrical signals from muscles | [MNE-BIDS](https://mne.tools/mne-bids/) | [MNE-Python](https://mne.tools/) | Newest |
| 11 | **Physiological recordings** | [Spec](https://bids-specification.readthedocs.io/en/stable/modality-specific-files/physiological-recordings.html) | Heart rate, respiration, skin conductance | [phys2bids](https://phys2bids.readthedocs.io/), [bidsphysio](https://github.com/cbinyu/bidsphysio) | Signal processing libraries | Established |
| 12 | **Behavioral experiments** | [Spec](https://bids-specification.readthedocs.io/en/stable/modality-specific-files/behavioral-experiments.html) | Stimulus timing, responses | [psychopy-bids](https://github.com/psych-ds/psychopy-bids) | Statistical analysis | Established |
| 13 | **Genetic Descriptor** | [Spec](https://bids-specification.readthedocs.io/en/stable/modality-specific-files/genetic-descriptor.html) | Genomic/genetic data | N/A (metadata standard) | Bioinformatics tools | Established |

**BIDS Extension Proposals (BEPs) in progress** include Non-Invasive Brain Stimulation (NIBS), provenance tracking, computational models, and more. See [bids.neuroimaging.io/get_involved.html](https://bids.neuroimaging.io/get_involved.html) for the current list.


---

## What Each Modality Measures and Why

### 1. MRI (Magnetic Resonance Imaging)

**What it measures**: Hydrogen atoms in water and fat respond to strong magnetic fields and radio pulses. Different tissue types (gray matter, white matter, CSF, blood) produce different signal intensities, creating detailed 3D images of brain structure.

**Sub-modalities in BIDS**:
- **Structural MRI (T1w, T2w, FLAIR)** -- High-resolution anatomical images for measuring brain structure, cortical thickness, and tissue volumes
- **Functional MRI (BOLD)** -- Blood-oxygen-level-dependent signal reflecting neural activity over time (4D: 3D space + time)
- **Diffusion MRI (DWI)** -- Water diffusion directionality revealing white matter tract architecture
- **Perfusion MRI (ASL)** -- Arterial spin labeling measuring blood flow without contrast agents
- **Quantitative MRI (qMRI)** -- Mapping physical tissue properties (T1, T2, proton density)
- **Fieldmaps** -- Calibration data for correcting magnetic field distortions

**Tool ecosystem**: The most mature in BIDS -- 20+ converters, 15+ BIDS Apps, dozens of analysis libraries. See detailed breakdowns in Layers 3-8 below.

### 2. MEG (Magnetoencephalography)

**What it measures**: Extremely weak magnetic fields (femtotesla scale) generated by synchronized neural currents, detected by superconducting sensors (SQUIDs) in a magnetically shielded room. Millisecond temporal resolution with centimeter spatial resolution.

**Key analysis operations**: Source localization (beamforming, minimum-norm estimation), time-frequency analysis, connectivity (coherence, phase-locking value), event-related fields.

**Primary tools**: [MNE-Python](https://mne.tools/) provides the full analysis stack. [FieldTrip](https://www.fieldtriptoolbox.org/) (MATLAB) is the other major option. Both are well-documented and widely used.

**Browser-runnable?**: YES -- MNE-Python is pure Python/NumPy, works in Colab.

### 3. EEG (Electroencephalography)

**What it measures**: Electrical voltage fluctuations at the scalp surface from postsynaptic potentials in cortical neurons. Millisecond temporal resolution, limited spatial resolution due to volume conduction through skull.

**Key analysis operations**: Filtering, artifact rejection (ICA), event-related potentials (ERPs), time-frequency decomposition (wavelets, FFT), source localization, microstate analysis, connectivity.

**Primary tools**: [MNE-Python](https://mne.tools/), [EEGLAB](https://eeglab.org/) (MATLAB), [FieldTrip](https://www.fieldtriptoolbox.org/) (MATLAB). The Python ecosystem (MNE) is fully browser-runnable.

**Browser-runnable?**: YES -- MNE-Python works in Colab. EEGLAB requires MATLAB.

### 4. iEEG (Intracranial EEG)

**What it measures**: Electrical signals recorded directly from brain tissue via surgically implanted electrodes. Covers stereo-EEG (depth electrodes), electrocorticography (surface grids), and deep brain stimulation recordings. Exceptional spatial and temporal resolution, but invasive (typically recorded during epilepsy surgery).

**Key analysis operations**: High-frequency oscillation detection, seizure onset zone mapping, cortical stimulation mapping, broadband gamma analysis.

**Primary tools**: [MNE-Python](https://mne.tools/) with iEEG-specific modules.

**Browser-runnable?**: YES.

### 5. PET (Positron Emission Tomography)

**What it measures**: Distribution of radioactive tracers injected into the bloodstream. Different tracers bind to different molecular targets (dopamine receptors, amyloid plaques, glucose metabolism), enabling measurement of specific neurochemical processes.

**Key analysis operations**: Kinetic modeling (compartment models), standardized uptake value (SUV) computation, partial volume correction, coregistration with MRI.

**The math**: Compartment models describe tracer kinetics -- the rate of tracer moving between blood plasma, free tissue, and specifically bound compartments, described by differential equations with rate constants K1, k2, k3, k4.

**Browser-runnable?**: Kinetic modeling is standard differential equation solving (scipy.integrate). YES for analysis; PET-specific preprocessing tools are heavier.

### 6. fNIRS (functional Near-Infrared Spectroscopy)

**What it measures**: Changes in oxygenated and deoxygenated hemoglobin concentration by shining near-infrared light through the skull. Similar principle to fMRI (hemodynamic response) but portable, cheaper, and wearable. Lower spatial resolution than fMRI.

**Key analysis operations**: Modified Beer-Lambert Law conversion (optical density to hemoglobin concentration), short-channel regression (removing scalp signal), GLM analysis similar to fMRI.

**Primary tools**: [MNE-NIRS](https://mne.tools/mne-nirs/) (Python extension of MNE).

**Browser-runnable?**: YES -- pure Python.

### 7. Microscopy

**What it measures**: Cellular and sub-cellular brain structure from tissue samples. Covers optical microscopy (brightfield, fluorescence, confocal, two-photon), electron microscopy (SEM, TEM), and micro-CT. Typically ex vivo (post-mortem tissue) but can be in vivo for some techniques.

**Key analysis operations**: Image registration, cell counting, fiber tracking at microscopic scale, 3D reconstruction from serial sections.

**Browser-runnable?**: Image processing operations (filtering, segmentation) are doable in Python. Large-scale 3D reconstruction requires significant compute.

### 8. MRS (Magnetic Resonance Spectroscopy)

**What it measures**: Chemical concentrations of metabolites in brain tissue (N-acetylaspartate, creatine, choline, GABA, glutamate, etc.) by analyzing the frequency spectrum of the MR signal rather than creating spatial images.

**Key analysis operations**: Spectral fitting (modeling the observed spectrum as a linear combination of known metabolite basis spectra), water referencing, tissue correction.

**Primary tools**: [FSL-MRS](https://open.win.ox.ac.uk/pages/fsl/fsl_mrs/) (Python), [Osprey](https://schorschinho.github.io/osprey/) (MATLAB). [spec2nii](https://github.com/wtclarke/spec2nii) for conversion.

**Browser-runnable?**: Spectral fitting is scipy.optimize. YES for the core analysis.

### 9. Motion

**What it measures**: Body and limb position/orientation over time from motion capture systems (optical markers, inertial measurement units). Used in motor control research, gait analysis, and multimodal studies combining movement with brain recordings.

**Browser-runnable?**: YES -- time series analysis, biomechanical computations are standard NumPy/SciPy.

### 10. EMG (Electromyography)

**What it measures**: Electrical activity from skeletal muscles. Surface EMG uses skin electrodes; intramuscular EMG uses needle electrodes. Used in motor control, rehabilitation, and brain-muscle coupling research.

**Primary tools**: [MNE-Python](https://mne.tools/) for signal processing. Similar analysis pipeline to EEG (filtering, rectification, time-frequency analysis).

**Browser-runnable?**: YES.

### 11. Physiological Recordings

**What it measures**: Body signals recorded alongside brain imaging -- cardiac (ECG/pulse oximetry), respiratory (belt/nasal cannula), electrodermal activity (skin conductance). Used primarily as nuisance regressors in fMRI analysis or for autonomic nervous system research.

**Primary tools**: [phys2bids](https://phys2bids.readthedocs.io/) for conversion. Standard signal processing for analysis.

**Browser-runnable?**: YES -- pure Python signal processing.

### 12. Behavioral Experiments

**What it measures**: Stimulus presentation timing, participant responses (button presses, reaction times), and task structure. No neural recording -- purely behavioral data organized in BIDS format for multimodal integration.

**Primary tools**: [PsychoPy](https://www.psychopy.org/) (with [Pavlovia](https://pavlovia.org/) for online experiments), [psychopy-bids](https://github.com/psych-ds/psychopy-bids) for BIDS output.

**Browser-runnable?**: YES -- PsychoPy has a web mode.

### 13. Genetic Descriptor

**What it is**: Not a recording modality but a metadata framework for linking genetic/genomic data to imaging datasets. Describes genotype files, genetic databases, and participant-level genetic information.


---

## How Brain Imaging Analysis Works -- The Big Picture

Across all modalities, data goes through a common processing chain:

```
RAW SCANNER / SENSOR OUTPUT
    |
    v
[CONVERSION] -- Transform proprietary formats into standardized BIDS files
    |
    v
[VALIDATION] -- Check that the files follow the BIDS standard
    |
    v
[QUALITY CONTROL] -- Detect artifacts, noise, signal problems
    |
    v
[PREPROCESSING] -- Remove noise, align to standard space, correct distortions
    |
    v
[FEATURE EXTRACTION] -- Measure cortical thickness, connectivity, activation patterns
    |
    v
[STATISTICAL ANALYSIS] -- Test hypotheses, classify conditions, build models
    |
    v
SCIENTIFIC CONCLUSIONS
```

Each BIDS tool handles one or more of these stages. Docker containers bundle each tool with its dependencies so you can run them without installing dozens of packages -- but every tool is built on open-source libraries that can be used independently.

The tools below are organized by functional layer. **Detailed breakdowns (with mathematical operations and browser-runnability) are provided for MRI tools. Other modalities will be expanded in subsequent versions.**


---

## LAYER 1 -- DATA CONVERTERS

Tools for converting raw scanner output into BIDS-compliant directory structures. Full list: [bids.neuroimaging.io/tools/converters.html](https://bids.neuroimaging.io/tools/converters.html)

### MRI Converters

#### 1.1 [dcm2niix](https://github.com/rordenlab/dcm2niix)

**What it does**: Converts DICOM files (the native format of MRI scanners) into NIfTI files (the standard neuroimaging format) plus JSON sidecar metadata.

**The science**: MRI scanners produce data as 2D slices acquired over time. dcm2niix reassembles these into 3D (or 4D, for time series) volumes, handling vendor-specific encoding differences (Siemens, GE, Philips all store DICOMs differently).

**The math**: Primarily coordinate transformations -- converting from scanner coordinates to a standardized patient coordinate system using affine transformation matrices (4x4 matrices encoding rotation, translation, and scaling).

**Input**: DICOM directory (.dcm files)
**Output**: NIfTI files (.nii.gz) + JSON metadata (.json)

**Browser-runnable?**: Partially. The core conversion is C code; a WASM port could work but doesn't exist yet. However, if you already have NIfTI files (as most shared datasets do), you skip this entirely.

**Python alternative**: `pip install dcm2niix` (wrapper) or use [nibabel](https://nipy.org/nibabel/) for direct NIfTI manipulation.


#### 1.2 [HeuDiConv](https://github.com/nipy/heudiconv) (Heuristic DICOM Converter)

**What it does**: Wraps dcm2niix with a heuristic system that automatically maps scanner sequences to BIDS naming conventions (e.g., "MPRAGE" becomes `sub-01/anat/sub-01_T1w.nii.gz`).

**The science**: Different labs name their scanner sequences differently. HeuDiConv lets you write rules (heuristics) that map your lab's naming to BIDS conventions.

**Input**: DICOM directory + heuristic file (Python)
**Output**: BIDS-organized dataset

**Browser-runnable?**: Yes, the heuristic logic is pure Python.

**Python alternative**: `pip install heudiconv`


#### 1.3 [BIDScoin](https://bidscoin.readthedocs.io/)

**What it does**: GUI-based converter that auto-discovers your data structure and lets you visually map it to BIDS without writing code.

**Browser-runnable?**: The GUI could be reimplemented as a web app. The backend logic is Python.


#### 1.4 [ezBIDS](https://brainlife.io/docs/using_ezBIDS/)

**What it does**: Web-based BIDS converter with no installation or programming required. Semi-automated inference and guidance for BIDS compliance. Can transfer to [OpenNeuro](https://openneuro.org/) or [brainlife.io](https://brainlife.io/).

**Browser-runnable?**: YES -- it already runs in the browser.


### Multi-Modality Converters

#### 1.5 [MNE-BIDS](https://mne.tools/mne-bids/)

**What it does**: Converts EEG, MEG, iEEG, and fNIRS data to BIDS format using [MNE-Python](https://mne.tools/).

**Browser-runnable?**: YES -- pure Python/NumPy.

#### 1.6 [phys2bids](https://phys2bids.readthedocs.io/)

**What it does**: Converts physiological recordings (heart rate, respiration, skin conductance) to BIDS format.

**Browser-runnable?**: YES -- pure Python.


---

## LAYER 2 -- VALIDATION

### 2.1 [BIDS Validator](https://bids-standard.github.io/bids-validator/)

**What it does**: Checks whether a dataset actually conforms to the BIDS specification -- correct file names, required metadata present, consistent dimensions.

**The math**: None -- this is file system inspection and JSON schema validation.

**Input**: A directory that claims to be a BIDS dataset
**Output**: List of errors and warnings

**Browser-runnable?**: YES -- **already runs in the browser** at [bids-standard.github.io/bids-validator](https://bids-standard.github.io/bids-validator/). Written in JavaScript.

**CLI alternative**: `pip install bids-validator`


---

## LAYER 3 -- QUALITY CONTROL (MRI)

### 3.1 [MRIQC](https://mriqc.readthedocs.io/) (MRI Quality Control)

**What it does**: Generates quantitative quality metrics and visual reports for structural and functional MRI data. Answers: "Is this scan usable, or is it too noisy/motion-corrupted?"

**The science**: Quality assessment based on established image quality metrics (IQMs) that quantify signal-to-noise ratio, contrast, spatial artifacts, and subject motion.

**Key metrics and their math**:

- **Signal-to-Noise Ratio (SNR)**: SNR = mu_signal / sigma_noise. Higher is better.
- **Contrast-to-Noise Ratio (CNR)**: CNR = |mu_GM - mu_WM| / sigma_noise
- **Entropy Focus Criterion (EFC)**: Shannon entropy of voxel intensities. EFC = -sum(p_i * log(p_i)). High entropy suggests ghosting.
- **Framewise Displacement (FD)**: Sum of absolute derivatives of 6 rigid-body motion parameters. FD_t = |delta_x| + |delta_y| + |delta_z| + |delta_alpha| + |delta_beta| + |delta_gamma|
- **DVARS**: Root-mean-square change in BOLD signal between consecutive volumes. DVARS_t = sqrt(mean((S_t - S_{t-1})^2))
- **Carpet plots**: 2D visualizations (voxels x time), global artifacts appear as vertical stripes.

**Input**: BIDS dataset (T1w and/or BOLD images)
**Output**: JSON quality metrics + HTML visual reports

**Browser-runnable?**: YES for the metrics -- SNR, CNR, EFC, FD, DVARS are all NumPy/SciPy operations.

**Python alternative**: [nilearn](https://nilearn.github.io/) + [nibabel](https://nipy.org/nibabel/) + custom metric functions.


---

## LAYER 4 -- PREPROCESSING (MRI)

### 4.1 [fMRIPrep](https://fmriprep.org/) (fMRI Preprocessing)

**What it does**: The dominant preprocessing pipeline for functional MRI. Takes raw BOLD time series and anatomical scans, produces cleaned, spatially normalized data ready for statistical analysis.

**The science**: Raw fMRI data is contaminated by head motion, magnetic field inhomogeneities, physiological noise, and scanner drift. fMRIPrep applies a sequence of corrections drawing from the best algorithms across FSL, ANTs, FreeSurfer, and nipype.

**The preprocessing steps and their math**:

1. **Skull stripping** -- Removes non-brain tissue. Method: ANTs brain extraction or FreeSurfer watershed. Math: Morphological operations + atlas-based template matching using diffeomorphic registration.

2. **Tissue segmentation** -- Classifies each voxel as gray matter, white matter, or CSF. Method: [FSL FAST](https://fsl.fmrib.ox.ac.uk/fsl/). Math: Hidden Markov Random Field model with Expectation-Maximization.

3. **Surface reconstruction** -- Builds 3D mesh of cortical surface. Method: [FreeSurfer](https://surfer.nmr.mgh.harvard.edu/) recon-all. Math: Deformable surface models balancing data fit against smoothness.

4. **Motion correction** -- Aligns all functional volumes to a reference. Method: FSL MCFLIRT or ANTs. Math: Rigid-body registration with 6 parameters (3 translations, 3 rotations).

5. **Susceptibility distortion correction** -- Corrects spatial warping from field inhomogeneities. Method: FSL TOPUP or SyN-SDC. Math: Voxel displacement field estimation via spline optimization.

6. **Coregistration** -- Aligns functional to anatomical images. Method: FreeSurfer bbregister. Math: Boundary-based registration maximizing intensity contrast across white matter surface.

7. **Spatial normalization** -- Warps each subject's brain into standard template space (MNI152). Method: [ANTs](http://stnava.github.io/ANTs/) SyN. Math: Diffeomorphic registration via velocity field integration.

8. **Confound estimation** -- Computes nuisance regressors. Method: CompCor. Math: PCA on WM/CSF time series.

**Input**: BIDS dataset with T1w + BOLD (+ optional fieldmaps)
**Output**: Preprocessed BOLD in template space, confound regressors, QC reports

**Browser-runnable?**: PARTIALLY. Individual operations are NumPy/SciPy. Full pipeline requires FreeSurfer (6+ hours/subject) and ANTs (large memory). Tutorial versions on downsampled data -- yes.


### 4.2 [HCP Pipelines](https://github.com/Washington-University/HCPpipelines) (Human Connectome Project)

**What it does**: Gold-standard preprocessing for high-resolution multimodal data. Requires both T1w and T2w scans. Produces CIFTI format (surface cortex + volumetric subcortex).

**Browser-runnable?**: No for full pipeline. Concepts teachable in Colab.


### 4.3 [BrainSuite](http://brainsuite.org/)

**What it does**: Integrated pipeline for structural, diffusion, and functional MRI with built-in QC at each stage. Distinctive for its iterative inspect-and-correct workflow.

**Browser-runnable?**: Partial -- QC visualization and bias field estimation work in Colab.


---

## LAYER 5 -- STRUCTURAL ANALYSIS (MRI)

### 5.1 [FreeSurfer](https://surfer.nmr.mgh.harvard.edu/) (BIDS App)

**What it does**: Cortical surface reconstruction and parcellation -- builds detailed 3D models of the cortical surface and divides it into ~70 anatomical regions.

**Key computations**:
- **Cortical thickness**: Shortest distance between white and pial surfaces at each vertex (mm). Thinning correlates with Alzheimer's, aging.
- **Parcellation**: Bayesian classification using geometric features (sulcal depth, curvature) and intensity profiles.
- **Subcortical segmentation**: Probabilistic atlas with shape priors for hippocampus, amygdala, thalamus, etc.

**Input**: BIDS dataset with T1w
**Output**: Surface meshes, parcellation labels, volume/thickness/area statistics

**Browser-runnable?**: NO for full recon-all (6-12 hours). YES for visualizing and analyzing FreeSurfer outputs with [nilearn](https://nilearn.github.io/).


---

## LAYER 6 -- CONNECTIVITY AND NETWORK ANALYSIS (MRI)

### 6.1 [giga_connectome](https://github.com/SIMEXP/giga_connectome)

**What it does**: Generates functional connectomes (correlation matrices) from [fMRIPrep](https://fmriprep.org/) outputs.

**The math**: Extract mean BOLD time series per brain region, compute pairwise Pearson correlation: r_ij = cov(ts_i, ts_j) / (sigma_i * sigma_j). Optionally apply Fisher z-transform: z_ij = 0.5 * ln((1+r_ij)/(1-r_ij)).

Result: a symmetric N x N matrix. The upper triangle, flattened, is the condensed dissimilarity vector -- a compact fingerprint of the brain's representational geometry. This connects directly to Representational Similarity Analysis (RSA) and to comparing biological brains with artificial neural networks.

**Browser-runnable?**: YES -- pure NumPy/nilearn.

**Python alternative**: `nilearn.connectome.ConnectivityMeasure` -- a few lines of code.


### 6.2 [MRtrix3_connectome](https://github.com/BIDS-Apps/MRtrix3_connectome)

**What it does**: Structural connectomes from diffusion MRI -- mapping physical white matter tracts.

**The math**: Fiber Orientation Distribution estimation via constrained spherical deconvolution, probabilistic tractography (stepping along FOD vector fields), connectome construction (counting streamlines between region pairs).

**Browser-runnable?**: PARTIAL. Matrix construction from precomputed tractography is trivial. Tractography itself is compute-intensive.


### 6.3 [Connectome Mapper 3](https://connectome-mapper-3.readthedocs.io/)

**What it does**: Full pipeline from raw data to multi-resolution connectomes (83 to 1015 regions using Lausanne parcellation).

**Browser-runnable?**: Multi-resolution concept and matrix analysis -- yes. Full pipeline -- no.


---

## LAYER 7 -- SPECIALIZED ANALYSIS (MRI)

### 7.1 [SPM](https://www.fil.ion.ucl.ac.uk/spm/) (Statistical Parametric Mapping)

**What it does**: The General Linear Model applied to every voxel independently. Identifies which brain regions activate during tasks or differ between groups.

**The math**: Y = X*beta + epsilon at each voxel. Random Field Theory for multiple comparisons correction across ~100,000 simultaneous tests.

**Browser-runnable?**: YES using [nilearn.glm](https://nilearn.github.io/stable/modules/glm.html).


### 7.2 [Hyperalignment](https://github.com/BIDS-Apps/hyperalignment)

**What it does**: Aligns brain activation patterns across subjects in high-dimensional feature space.

**The math**: Multi-subject Procrustes analysis. Find rotation R_i minimizing sum_i ||X_i * R_i - X_template||^2.

Directly relevant to comparing representational geometry across brains and artificial neural networks.

**Browser-runnable?**: YES -- linear algebra (SVD/Procrustes), pure NumPy.


### 7.3 [deepMReye](https://github.com/DeepMReye/DeepMReye)

**What it does**: Decodes eye position from fMRI data without an eye tracker, using a 3D CNN.

**Browser-runnable?**: YES for inference with a pre-trained model.


---

## LAYER 8 -- SUPPORTING TOOLS (Pure Python, No Containers)

| Tool | What it does | Browser-runnable? |
|---|---|---|
| [PyBIDS](https://bids-standard.github.io/pybids/) | Parse and query BIDS datasets | YES |
| [nilearn](https://nilearn.github.io/) | Machine learning for neuroimaging -- plotting, GLM, connectivity, decoding | YES |
| [nibabel](https://nipy.org/nibabel/) | Read/write neuroimaging file formats (NIfTI, GIFTI, CIFTI) | YES |
| [nipype](https://nipype.readthedocs.io/) | Pipeline framework wrapping FSL, ANTs, FreeSurfer, SPM | Framework is Python; wrapped tools need local install |
| [neurobagel](https://neurobagel.org/) | Cross-dataset query by demographics and imaging parameters | YES -- web interface exists |
| [MNE-Python](https://mne.tools/) | Full EEG/MEG/iEEG/fNIRS analysis stack | YES |
| [FieldTrip](https://www.fieldtriptoolbox.org/) | MEG/EEG analysis (MATLAB) | Requires MATLAB |
| [EEGLAB](https://eeglab.org/) | EEG analysis (MATLAB) | Requires MATLAB |


---

## BROWSER-RUNNABILITY SUMMARY (MRI)

### Fully runnable in Colab (no installation beyond pip):

| Function | Library | Lines of code |
|---|---|---|
| BIDS validation | [bids-validator](https://bids-standard.github.io/bids-validator/) | ~5 |
| Dataset querying | [PyBIDS](https://bids-standard.github.io/pybids/) | ~10 |
| Read/write brain images | [nibabel](https://nipy.org/nibabel/) | ~5 |
| Quality metrics (SNR, CNR, FD, DVARS) | NumPy/nibabel | ~50 |
| Tissue segmentation (basic) | [nilearn](https://nilearn.github.io/) | ~20 |
| Functional connectivity matrices | [nilearn](https://nilearn.github.io/) | ~15 |
| GLM / statistical maps | [nilearn.glm](https://nilearn.github.io/stable/modules/glm.html) | ~30 |
| Graph analysis of connectomes | [networkx](https://networkx.org/) | ~20 |
| Hyperalignment (Procrustes) | NumPy (SVD) | ~40 |
| Brain visualization | [nilearn.plotting](https://nilearn.github.io/stable/plotting/index.html) | ~5 |
| Representational similarity analysis | NumPy/SciPy | ~30 |
| Machine learning decoding | [nilearn.decoding](https://nilearn.github.io/stable/modules/decoding.html) | ~25 |
| EEG/MEG full stack | [MNE-Python](https://mne.tools/) | varies |


### Requires local/HPC (not browser-feasible):

| Function | Why |
|---|---|
| FreeSurfer recon-all | 6-12 hours, high memory |
| Full fMRIPrep pipeline | Orchestrates many heavy tools |
| Full tractography (millions of streamlines) | Computationally intensive |
| DICOM conversion from raw scanner data | Usually done at the scanner |


---

## BIDS ACADEMY -- ARCHITECTURAL BLUEPRINT

### The Vision

A browser-based learning environment where each neuroimaging analysis function comes with:

1. **Concept explainer** -- What scientific question does this answer? (2 minutes reading)
2. **Math tutorial** -- What computation is being performed? Interactive equations
3. **Interactive app** -- Run the actual analysis on sample data (Vercel/React, code hidden by default, "show code" toggle for learners)
4. **Connection map** -- How does this function relate to others in the pipeline?

### Technical Architecture

**Front end** ([Vercel](https://vercel.com/) / [GitHub Pages](https://pages.github.com/)):
- Interactive ecosystem map (React/D3 -- clickable pipeline diagram)
- Explainer pages per tool
- "Launch in Colab" buttons for extended exercises

**Interactive modules** (React apps, code runs client-side):
- Each module uses simulated or sample BIDS data
- Code hidden by default; "show code" reveals the Python/nilearn equivalent
- Parameters adjustable via sliders and toggles

**Sample dataset**: [ds000003](https://openneuro.org/datasets/ds000003) or [ds000114](https://openneuro.org/datasets/ds000114) from [OpenNeuro](https://openneuro.org/)

### Module Sequence (MRI focus, Phase 1)

```
00  What is BIDS              -- BIDS structure, PyBIDS, validation
01  Reading Brain Images       -- nibabel, NIfTI format, coordinate systems
02  Quality Control            -- SNR, CNR, FD, DVARS, carpet plots
03  Skull Stripping            -- Brain extraction, morphological operations
04  Tissue Segmentation        -- Gaussian mixtures, EM algorithm
05  Motion Correction          -- Rigid-body registration, cost functions
06  Spatial Normalization      -- Template spaces, deformation fields
07  Functional Connectivity    -- [Interactive module](https://starborn.github.io/BIDS/module-07-connectivity.html) [LIVE]
08  GLM Activation Mapping     -- General Linear Model, statistical maps
09  Structural Connectomes     -- Diffusion, tractography basics
10  Graph Analysis             -- Network metrics, modularity
11  Hyperalignment             -- Cross-subject alignment, Procrustes
12  Machine Learning Decoding  -- SVM, cross-validation
13  Dissimilarity Matrices     -- RSA, RDMs, condensed distance vectors
```

Module 07 (Functional Connectivity) Learning is built 
07  Functional Connectivity    -- [Interactive module](https://starborn.github.io/BIDS/module-07-connectivity.html) [LIVE]


### AIKR CG Contribution

This project is a case study (in progress, not live yet) for W3C AIKR CG Technical Note TN3: "Making Tool Ecosystems Machine-Readable and Human-Accessible." The BIDS Apps page has limited usefulness because it describes tools by their operational status (Docker build passing/failing) rather than by their function, input/output, and scientific basis. An AIKR-style approach would:

1. Define a tool description schema (extending [schema.org/SoftwareApplication](https://schema.org/SoftwareApplication))
2. Include fields for: scientific_function, mathematical_basis, input_format, output_format, browser_runnability, tutorial_url
3. Generate both human-readable documentation and machine-consumable metadata from the same source
4. Demonstrate this on the BIDS ecosystem as proof of concept


---

## Next Steps

TBA


---

*Document produced by [ESL](https://sites.google.com/view/paoladimaiophd) / [W3C AIKR CG](https://www.w3.org/community/aikr/), May 2026*
*License: CC BY 4.0*
