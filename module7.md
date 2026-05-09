BIDS Academy -- Module 07     

DRAFT

Functional Connectivity
How correlated brain activity reveals the architecture of neural networks -- from raw time series to dissimilarity matrices, using BIDS tools without Docker.

Interactive module: starborn.github.io/BIDS/module-07-connectivity.html

Ecosystem map: starborn.github.io/BIDS

Full tutorial: ToolsGuideTutorial.md
Version 0.2 -- May 2026 | ESL / W3C AIKR CG | CC BY 4.0


Part 1: Introduction to Brain Connectivity
What is brain connectivity?
The brain is not a collection of independent regions working in isolation. It is a network. Different areas communicate constantly -- the visual cortex talks to the motor cortex when you reach for something you see, memory regions talk to decision-making regions when you draw on past experience to make a choice. Brain connectivity is the study of these communication patterns.
Two kinds of connectivity
Structural connectivity maps the physical wiring -- the white matter fibers (axon bundles) that physically connect one region to another, like cables between buildings. Functional connectivity maps coordinated activity -- regions that consistently activate and deactivate together over time, whether or not they are directly wired to each other. This module focuses on functional connectivity.
What are brain regions?
A raw fMRI scan contains about 100,000 tiny measurement points called voxels, each roughly 2-3mm across. Individual voxels are noisy. To make the data manageable, we divide the brain into larger regions (parcels) using an atlas -- a pre-defined map that groups voxels into anatomically or functionally meaningful areas. Common atlases define between 100 and 1,000 regions. This module uses 20 regions for clarity.
What is a time series?
During an fMRI scan, the scanner takes a snapshot of the whole brain every 1-2 seconds (the repetition time, or TR). For each brain region, we get a sequence of numbers -- one value per snapshot -- representing that region's activity level over time. This sequence is a time series. If the scan lasts 5 minutes with a TR of 2 seconds, you get 150 numbers per region.
What does the BOLD signal measure?
fMRI does not measure neural activity directly. It measures blood oxygenation. When neurons fire, they consume oxygen, triggering a local increase in blood flow that overshoots the demand. This hemodynamic response changes the ratio of oxygenated to deoxygenated hemoglobin, which has different magnetic properties -- and that is what the scanner detects. The signal is called BOLD: Blood-Oxygen-Level-Dependent.
What is correlation?
Correlation measures how similarly two signals fluctuate over time. The Pearson correlation coefficient (r) quantifies this on a scale from -1 to +1. These are its bounds -- r can never go below -1 or above +1. A value of r = 1 means the two signals move in perfect lockstep, r = -1 means they move in perfect opposition, and r = 0 means no linear relationship. "Linear co-fluctuation" simply means the two signals tend to rise and fall together (or in opposition) in a proportional way.
What is a connectivity matrix?
If you compute the correlation between every possible pair of brain regions, you get a symmetric matrix -- a grid where rows and columns are regions and each cell contains the correlation between that pair. The diagonal is always 1. This matrix is the functional connectome. It captures the full pattern of which regions co-activate with which others.
What is a dissimilarity matrix?
A simple transformation -- d = 1 - r -- converts correlations into distances. High correlation becomes small distance (representationally similar regions). The upper triangle of this matrix, flattened into a single vector, is a compact fingerprint of the brain's representational geometry. These fingerprints can be compared across people, or between a brain and an artificial neural network.



Part 2: Connectivity in BIDS
BIDS itself does not compute connectivity. BIDS is the filing system -- it standardizes how brain data is organized on disk so that analysis tools can find what they need automatically.
The pipeline
Raw scan (DICOM) --> Converter (dcm2niix) --> BIDS dataset --> fMRIPrep (preprocessing) --> BIDS Derivatives --> Connectivity analysis (YOU ARE HERE)
Step 1 -- BIDS organizes the raw data
Your fMRI scan comes off the scanner as a collection of DICOM files. BIDS converters (dcm2niix, HeuDiConv, ezBIDS) transform these into a standardized directory structure with NIfTI files and JSON metadata sidebands. Without BIDS, every lab stores data differently. With BIDS, any tool can automatically locate the functional scan and read the TR.
Step 2 -- BIDS Apps preprocess it
fMRIPrep (a BIDS App) takes the standardized input and produces preprocessed BOLD data -- motion-corrected, spatially normalized, with confound regressors computed. The output follows BIDS Derivatives conventions.
Step 3 -- Connectivity analysis consumes BIDS Derivatives
Tools like giga_connectome or nilearn take the preprocessed BOLD file, apply a parcellation atlas, extract regional time series, and compute the correlation matrix. PyBIDS finds the right files automatically: no manual path configuration needed.
BIDS Apps for connectivity
giga_connectome -- Takes fMRIPrep derivatives, applies parcellation, computes connectivity matrices. The most direct BIDS-to-connectome tool.
Connectome Mapper 3 -- Full pipeline from raw BIDS to multi-resolution connectomes (83 to 1015 regions).
nilearn -- Python library (pip install, no Docker). Parcellation, time series extraction, connectivity matrices, visualization. Runs in Colab.
PyBIDS -- Query engine for BIDS datasets. Finds files by subject, task, space. The bridge between BIDS organization and analysis code.
Without Docker?
Every tool listed above is installable with pip install. The Docker containers are convenience packaging. For connectivity analysis, you need only: pip install nilearn nibabel pybids. That is what the interactive tutorial demonstrates.



Part 3: Using the Interactive Tutorial
The interactive module is available at: starborn.github.io/BIDS/module-07-connectivity.html
Loading data
Load simulated data: Click this button to generate a simulated dataset with 20 brain regions organized into four networks (Visual, Motor, Default Mode, Frontoparietal). This is the fastest way to start exploring.
Upload CSV: Upload a pre-computed correlation matrix (N x N, comma or tab separated) or raw time series (timepoints x regions). The module auto-detects which format you have provided.
Export matrix as CSV: Download the current connectivity matrix for use in other tools (R, MATLAB, Python).
The heatmap
The main visualization is a correlation matrix. Rows and columns are brain regions. Each cell's color represents the correlation strength: warm/orange for positive correlation, blue for negative, dark for near-zero. The colored brackets on the left mark network modules. Click any cell to select a region pair.
The time series plot
Below the heatmap, two overlaid lines show the BOLD time series for the selected pair. When lines track each other, correlation is high. When they move independently, correlation is low. The Pearson r value is displayed.
The four-step walkthrough
Four buttons walk through the analysis stages: Extract (averaging voxels into regions), Correlate (computing pairwise Pearson r), Fisher z-transform (normalizing for statistics), and Dissimilarity (converting to distance). Each step shows the science, the math, and toggleable Python code -- both the simulated version and the real BIDS version.
Parameter controls
Time points (TRs): Drag from 20 to 500. With few time points, the matrix is noisy. With many, the block structure becomes crisp. This demonstrates why longer scans give more reliable estimates.
Random seed: Each seed generates a different simulated subject. Same network architecture, different noise. This shows individual variation.
Fisher z-transform: Toggle on to see how the scale changes. Values can now exceed 1. This is the transformation needed for valid group-level statistics.
Network metrics
Below the interactive area, four graph-theoretic metrics are computed from the current matrix: average degree (connections per region above a threshold), clustering coefficient (how much neighbors connect to each other), density (fraction of possible edges present), and mean correlation. These characterize the brain's network architecture.
The dissimilarity vector
The bottom panel shows how the correlation matrix converts to a condensed dissimilarity vector (d = 1 - r for each pair, upper triangle flattened). For 20 regions: 190 values. This compact fingerprint enables comparison across subjects or between biological brains and artificial neural networks.


BIDS Academy -- Module 07 of 13 -- Epistemic Systems Lab / W3C AIKR CG -- CC BY 4.0
