Here is the complete table as a Markdown (.md) file. You can copy the code block below and save it as `bids_ecosystem_funding.md`.

```markdown
# BIDS Ecosystem: Software, Tools, and Funding

*Last updated: May 11, 2026*

---

## 1. Data Conversion & Curation (Raw Data to BIDS)

| Software/Tool | Description & Key Features | Verified Funding & Development |
| :--- | :--- | :--- |
| **BIDScoin** | A tool that provides an intuitive GUI for converting neuroimaging data to BIDS. Good for users who prefer not to use a command line. | **Funding**: ❌ *No specific funding information found in available search results.* <br><br>**Developers/Affiliations**: Not specified in available sources. |
| **Heudiconv** | A flexible Python-based tool for converting DICOMs to BIDS. Requires some scripting knowledge. | **Funding**: ❌ *No specific funding information found in available search results.* <br><br>**Developers/Affiliations**: Cited in the context of the Neurodesk platform only. |
| **dcm2niix** | A popular, fast tool for converting DICOM files to NIfTI format. Often the first step in creating BIDS datasets. | **Funding**: ❌ *No specific funding information found in available search results.* <br><br>**Developers/Affiliations**: Cited in the context of the Neurodesk platform only. |
| **Clinica** | A software platform facilitating neuroimaging studies with "BIDS Converters" for various databases. | **Funding**: ❌ *No specific funding mentioned in the available abstract.* <br><br>**Developers/Affiliations**: Matthieu Joulot, Nicolas Gensollen, Ghislain Vaillant, Ninon Burgos, Olivier Colliot (affiliated with INRIA). |
| **LSLAutoBIDS** | A Python package for LabStreamingLayer (LSL) studies. Automates integration of EEG, eye-tracking, and other data into BIDS. | **Funding**: ❌ *No specific funding mentioned in the available paper.* <br><br>**Developers/Affiliations**: Developed and actively used by the **Computational Cognitive Science Lab at the University of Stuttgart** (Manpa Barman, Jan Range, Benedikt Valerian Ehinger). |

---

## 2. Reproducible Processing Pipelines (BIDS Apps)

| Software/Tool | Description & Key Features | Verified Funding & Development |
| :--- | :--- | :--- |
| **fMRIPrep** | Robust, easy-to-use pipeline for preprocessing functional MRI (fMRI) data. Designed for minimal manual intervention. | **Funding** (via `fMRIPrep Lifespan` preprint, 2025): <br> • **5T32DC000038** (NIDCD) – S.L.M. <br> • **5R24MH117179** (NIMH) – C.J.M. <br> • Courtois Neuromod – F.P. <br> • FRQ-S – P.B. <br><br>**Note**: Base fMRIPrep funding not found; these are author-specific. |
| **mriqc** (MRI Quality Control) | BIDS App that generates visual and numerical reports to assess MRI data quality. | **Funding**: ❌ *No specific funding information found in available search results.* |
| **ASLprep** | Preprocessing pipeline specifically for Arterial Spin Labeling (ASL) MRI data (cerebral blood flow). | **Funding**: ❌ *No specific funding information found in available search results.* |
| **dMRIPrep** | Pipeline for preprocessing diverse diffusion MRI (dMRI) data (white matter tracts). | **Funding**: ❌ *No specific funding information found in available search results.* |

---

## 3. Data Management, Versioning, and Publishing

| Software/Tool | Description & Key Features | Verified Funding & Development |
| :--- | :--- | :--- |
| **DataLad** | Version control system built on Git and git-annex for handling large files. Foundational for managing terabyte-sized datasets. | **Funding**: ✅ **Confirmed** <br> • **NSF 1429999** (US National Science Foundation) <br> • **BMBF 01GQ1411** (German Federal Ministry of Education and Research) <br> • **NIH 1P41EB019936-01A1** (ReproNim project) |
| **OpenNeuro** | Free, open-source platform for sharing and analyzing BIDS-compliant neuroimaging data. Hosts 600+ public datasets. | **Funding**: ✅ **Confirmed** <br> • National Science Foundation (unspecified grant) <br> • National Institute of Mental Health (unspecified grant) <br> • National Institute on Drug Abuse (unspecified grant) <br> • Laura and John Arnold Foundation |
| **Dataverse** | Repository platform providing DOIs and access controls. Used by LSLAutoBIDS for automated archiving and publishing. | **Funding**: ❌ *No specific funding information found in available search results.* |

---

## 4. Integrated Analysis Environments

| Software/Tool | Description & Key Features | Verified Funding & Development |
| :--- | :--- | :--- |
| **Neurodesk** | Community-driven platform providing containerized access to 100+ neuroimaging tools (BIDScoin, fMRIPrep, MRIQC, DataLad). | **Funding**: ✅ **Confirmed** <br> • Wellcome Trust (**313306/Z/24/Z**) – CZI/EOSS Cycle 6 <br> • Australian Research Data Commons (ARDC) <br> • National Imaging Facility (NIF) – Australia <br> • NSF **#2005506** (Jetstream2 Cloud credits) |

---

## Legend

| Symbol | Meaning |
| :--- | :--- |
| ✅ **Confirmed** | Funding agency and/or grant number found in official documentation, papers, or acknowledgements. |
| ❌ *Not found* | Searched available results (including tool websites, papers, and funding databases within this session) but no specific funding information was located. |

---

## Notes for Discussion / Verification

- **BIDScoin, Heudiconv, dcm2niix, Clinica, mriqc, ASLprep, dMRIPrep, Dataverse** – No funding data located in this search.
- **fMRIPrep** – Only indirect funding via a preprint about a related project (`fMRIPrep Lifespan`), not the main tool itself.
- For tools with ❌, this may mean truly unfunded, or simply that funding information was not publicly documented or accessible in this search.

---

*Generated for discussion and verification purposes.*
```

You can paste this directly into a `.md` file and open it with any Markdown viewer (GitHub, VS Code, Typora, etc.). Let me know if you'd like me to adjust the formatting or add a column for specific researcher names.
