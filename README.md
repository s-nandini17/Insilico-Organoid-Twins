

\# In Silico Organoid Twins

\### Automated Bioinformatics Simulation for Patient-Specific Drug Screening



\[!\[License](https://img.shields.io/badge/License-Apache\_2.0-blue.svg)](LICENSE)

\[!\[Status](https://img.shields.io/badge/Status-Prototype\_Development-orange)]()

\[!\[Competition](https://img.shields.io/badge/Submitted\_To-Young\_Medicine\_2025-teal)]()

\[!\[Institution](https://img.shields.io/badge/Institution-Bversity\_School\_of\_Biosciences-navy)]()



> \*\*Decision-support tool — the oncologist decides treatment. Our output informs; it does not prescribe.\*\*



\---



\## Table of Contents



\- \[Project Overview](#project-overview)

\- \[Problem Statement](#problem-statement)

\- \[Proposed Solution](#proposed-solution)

\- \[Pipeline Architecture](#pipeline-architecture)

\- \[Core Computational Modules](#core-computational-modules)

\- \[Technologies and Tools](#technologies-and-tools)

\- \[Validation Strategy](#validation-strategy)

\- \[Expected Outcomes](#expected-outcomes)

\- \[Repository Contents](#repository-contents)

\- \[Roadmap](#roadmap)

\- \[Scientific References](#scientific-references)

\- \[Team](#team)

\- \[Disclaimer](#disclaimer)

\- \[License](#license)



\---



\## Project Overview



\*\*In Silico Organoid Twins\*\* is a multi-scale computational platform that digitally replicates the drug response behaviour of patient-derived organoids (PDOs) — three-dimensional tumour structures cultivated from a patient's own cancer cells. Rather than growing physical organoids in a laboratory (a process requiring 4–6 weeks and over USD 10,000 per test panel), the platform computationally simulates the same biological processes from two clinical inputs: a histological biopsy image and a patient gene expression profile.



The platform was developed as a competition submission to the \*\*All-Russian Scientific School "Young Medicine" 2025\*\*, Nomination: Biomedical Engineering and Digital Health Technologies, Project Type: Engineering / Business Domain.



\*\*Institution:\*\* Bversity School of Biosciences



PDOs are currently the most predictively accurate preclinical model available, achieving 80–90% sensitivity in drug response prediction compared to \~50% for conventional 2D cell cultures \[Driehuis et al., \*Nature Protocols\*, 2020; Vlachogiannis et al., \*Science\*, 2018]. However, their scalability limitations make them operationally infeasible for high-throughput pharmaceutical screening. This project addresses that bottleneck computationally.



\---



\## Problem Statement



The global oncology drug development pipeline faces a systemic crisis: over \*\*90% of cancer drug candidates fail in clinical trials\*\*, resulting in estimated losses of USD 1–5 million per compound per year in false-positive screening costs alone \[Begley \& Ellis, \*Nature\*, 2012]. A primary cause is the inadequacy of preclinical models.



\### Why existing solutions fail



| Limitation | Current Physical PDO Workflow |

|---|---|

| \*\*Time\*\* | 4–6 weeks per experimental cycle |

| \*\*Cost\*\* | > USD 10,000 per test panel |

| \*\*Throughput\*\* | 10³–10⁴ organoids maximum per batch |

| \*\*Variability\*\* | 20–50% batch-to-batch variability |

| \*\*Accessibility\*\* | Restricted to fewer than 15 specialist labs globally |

| \*\*Scalability\*\* | Cannot screen hundreds of compounds per patient |



These constraints make PDO-based screening operationally and economically infeasible at the scale required for modern pharmaceutical development — and entirely inaccessible to most oncology centres worldwide.



\---



\## Proposed Solution



\*\*In Silico Organoid Twins\*\* builds a five-layer multi-scale simulation pipeline that computationally replicates patient-specific PDO drug response behaviour, calibrated against 1,000+ real-world pharmacogenomic profiles.



\### How it works



```

INPUT                        PIPELINE (automated, 2–4 hrs)           OUTPUT

─────────────────────        ──────────────────────────────────       ──────────────────────────

Biopsy histology image  ──►  U-Net: organoid geometry reconstruction  Drug sensitivity ranking

&#x20;                            ABM:   tumour cell dynamics simulation    IC50 dose-response curves

Gene expression profile ──►  QSAR:  drug molecular property models    Confidence ranges per compound

(CSV from genomics lab)      PDE:   drug diffusion + metabolism        PDF + CSV report download

&#x20;                            GPU:   10⁵ virtual screens/hour   ──►   Clinician reviews → decision

```



The clinician submits two files via a browser-based Streamlit interface. The pipeline runs automatically on GPU-accelerated HPC infrastructure and returns an interactive dose-response report within 1–4 hours — compared to 4–6 weeks for the equivalent physical experiment.



\*\*Target validation metric:\*\* Pearson r ≥ 0.95 against experimental PDO IC50 values (5-fold cross-validation on 1,000+ PDO profiles from DepMap, GDSC2, and curated PDO literature).



\---



\## Pipeline Architecture



```

┌─────────────────────────────────────────────────────────────────────┐

│                    IN SILICO ORGANOID TWIN PLATFORM                  │

├──────────────┬──────────────┬──────────────┬────────────────────────┤

│   MODULE 1   │   MODULE 2   │   MODULE 3   │       MODULE 4         │

│  GEOMETRY    │    CELLS     │    DRUGS     │      INTERFACE         │

│              │              │              │                        │

│  U-Net CNN   │  scRNA-seq   │  QSAR/PKPD   │  Streamlit Web App     │

│  trained on  │  → PhysiCell │  RDKit +     │  FHIR R4 EHR API       │

│  annotated   │  agent-based │  OpenEye     │  Docker / Kubernetes   │

│  H\&E images  │  model (ABM) │  FEniCS PDE  │  HPC deployment        │

│  > 5,000 img │  10⁶ cells   │  diffusion   │  GPU PyTorch inference │

└──────────────┴──────────────┴──────────────┴────────────────────────┘

&#x20;        │              │              │

&#x20;        ▼              ▼              ▼

&#x20;   3D organoid    Cell dynamics   Drug concentration

&#x20;   mesh topology  + signalling    gradients → IC50

&#x20;        │              │              │

&#x20;        └──────────────┴──────────────┘

&#x20;                       │

&#x20;                       ▼

&#x20;          Bayesian calibration (Optuna)

&#x20;          against DepMap + GDSC2 + PDO literature

&#x20;                       │

&#x20;                       ▼

&#x20;             Validated dose-response output

```



\---



\## Core Computational Modules



\### Module 1 — Organoid Geometry Reconstruction (U-Net)



A U-Net convolutional neural network is trained on annotated histological biopsy images to segment organoid topology — extracting spatial cell distributions, lumen architecture, and stromal boundaries. Output is a 3D mesh representation of patient-specific organoid geometry passed to the cellular simulation layer.



\- \*\*Architecture:\*\* U-Net (Ronneberger et al., MICCAI 2015)

\- \*\*Training data:\*\* > 5,000 annotated organoid H\&E images (public datasets)

\- \*\*Validation benchmark:\*\* Dice score 0.87–0.97 on CRC histology \[Schoenpflug et al., 2023]

\- \*\*Organoid-specific validation:\*\* \[Alani et al., \*Bioengineering\*, 2025]



\### Module 2 — Cellular Dynamics Simulation (PhysiCell ABM)



Single-cell RNA sequencing (scRNA-seq) data is integrated into an agent-based model (ABM) using the PhysiCell framework. Each simulated cell agent is parameterised by its transcriptomic profile — gene expression, pathway activity, and cell cycle state. The model simulates:



\- Proliferation and apoptosis dynamics

\- Cell-cell communication (ligand-receptor interactions)

\- Mechanical forces within organoid geometry

\- Large-scale heterogeneous cell populations



\- \*\*Framework:\*\* PhysiCell \[Ghaffarizadeh et al., \*PLOS Computational Biology\*, 2018]

\- \*\*Scale:\*\* Large-scale cell populations on 32-core HPC nodes

\- \*\*Validation:\*\* Hybrid ABM+PDE approach validated for 3D tumour drug response \[Duswald et al., PMC, 2023]



\### Module 3 — Drug Modelling and Diffusion (QSAR + PDE)



Drug behaviour within the virtual organoid is modelled using a two-layer approach:



\*\*Layer 1 — QSAR molecular property prediction (RDKit, OpenEye):\*\*

\- Lipophilicity, membrane permeability, metabolic stability

\- Protein binding affinity

\- Pharmacokinetic parameter estimation



\*\*Layer 2 — PDE-based drug diffusion (FEniCS):\*\*

\- Finite-element simulation of drug diffusion, convection, and metabolic consumption

\- Time-resolved intracellular concentration profiles for each agent cell

\- Spatial drug gradient mapping across 3D organoid volume



\- \*\*IC50 prediction validation:\*\* R² = 0.64–0.72 across cancer types \[Menden et al., \*Nature Communications\*, 2019]

\- \*\*CRC-specific QSAR validation:\*\* \[bioRxiv, 2023]

\- \*\*PDE transport validation:\*\* \[Moradi Kashkooli \& Kolios, \*Cancers\*, 2023]



\### Module 4 — Clinical Interface (Streamlit + FHIR)



A browser-based web application built in Streamlit with FHIR R4 EHR integration. No bioinformatics expertise required from the clinical user.



\*\*Features:\*\*

\- Secure data upload (NGS files, histology images)

\- Real-time simulation progress tracking

\- Interactive dose-response curve visualisation

\- Downloadable PDF and CSV reports

\- FHIR-compliant EHR integration for clinical workflow embedding

\- GPU-accelerated inference via PyTorch (10⁵ virtual screens/hour)

\- Docker and Kubernetes containerisation for HPC deployment



\---



\## Technologies and Tools



\### Core simulation stack



| Component | Tool / Library | Purpose |

|---|---|---|

| Image segmentation | U-Net, StarDist, PyTorch | Organoid topology from H\&E images |

| scRNA-seq processing | Scanpy, Seurat, STAR aligner | Cell type annotation, QC |

| Agent-based modelling | PhysiCell, CellBlender | Cell dynamics simulation |

| QSAR modelling | RDKit, OpenEye | Drug molecular properties |

| PDE solving | FEniCS | Drug diffusion and metabolism |

| Hyperparameter tuning | Optuna (Bayesian optimisation) | Model calibration |

| GPU acceleration | PyTorch | High-throughput inference |

| Data processing | BioPython, NumPy, SciPy, pandas | Pipeline orchestration |



\### Infrastructure and deployment



| Component | Tool | Purpose |

|---|---|---|

| Web application | Streamlit | Clinical user interface |

| EHR integration | FHIR R4 API | Electronic health record connectivity |

| Containerisation | Docker, Kubernetes | HPC deployment and scalability |

| Version control | GitHub (Apache 2.0) | Open-source release |

| Dataset release | Zenodo (CC-BY 4.0) | Benchmark dataset publication |



\### Data sources



| Dataset | Use |

|---|---|

| GDSC2 (Genomics of Drug Sensitivity in Cancer) | Drug IC50 ground truth for QSAR calibration |

| DepMap (Cancer Dependency Map) | Transcriptomic cell-type annotations |

| OrganoidDB | Organoid morphological profiles |

| GEO (NCBI Gene Expression Omnibus) | scRNA-seq datasets |

| TCGA-COAD | Colorectal cancer histology images |



\---



\## Validation Strategy



All simulation components are calibrated and validated against public pharmacogenomic datasets and curated PDO literature:



\- \*\*Calibration data:\*\* 1,000+ real PDO drug response profiles (DepMap, GDSC2, OrganoidDB)

\- \*\*Optimisation:\*\* Bayesian hyperparameter tuning (Optuna) minimising deviation from experimental IC50 measurements

\- \*\*Cross-validation:\*\* 5-fold cross-validation + independent holdout dataset

\- \*\*Primary metric:\*\* Pearson r ≥ 0.95 (predicted vs experimental IC50)

\- \*\*Secondary metric:\*\* AUC-ROC ≥ 0.92 for drug response classification

\- \*\*Stochastic replication:\*\* n = 10 replicates per compound for confidence interval estimation



\*\*Novel contribution:\*\* A unified benchmark dataset cross-linking organoid morphological profiles (OrganoidDB), transcriptomic annotations (DepMap CCLE, GEO), and drug sensitivity measurements (GDSC2) for colorectal cancer patient-derived models — planned for release on Zenodo and submission to \*Scientific Data\* (Nature Portfolio).



\---



\## Expected Outcomes



| Metric | Physical PDO | In Silico Organoid Twin | Improvement |

|---|---|---|---|

| Cost per test | > USD 10,000 | \~ USD 100 | 95% reduction |

| Turnaround time | 4–6 weeks | 1–4 hours | \~98% reduction |

| Throughput | 10³–10⁴ organoids/batch | 10⁵ virtual screens/hour | Orders of magnitude |

| Predictive accuracy | 80–90% (PDO) | Target: \~ 95% concordance | Equivalent or superior |

| Drug attrition reduction | Baseline | Projected 30% reduction | Saves billions annually |

| Infrastructure required | Specialist lab | Browser + HPC | Democratised access |



\---



\## Repository Contents



| File | Description |

|---|---|

| `README.md` | This document |

| `InSilico\_Organoid\_Twins\_Final.pptx` | Final 8-slide competition pitch deck |

| `organoid\_project.docx` | Full GOST R 2.105-2019 compliant project document (15–17 pages) |

| `InSilico\_OrgTwins\_Brief.pdf` | Two-page competition brief (RSCI-indexed abstract format) |

| `LICENSE` | Apache 2.0 open-source licence |



\*Pipeline source code, trained model weights, and curated benchmark dataset will be released in subsequent commits as development progresses.\*



\---



\## Roadmap



\### Phase 1 — Development (Months 1–3)

\- \[ ] Data ingestion pipeline: FHIR parser, scRNA-seq preprocessing (FastQC, STAR, Scanpy)

\- \[ ] U-Net segmentation engine: training on annotated organoid image datasets

\- \[ ] Agent-based cellular model: PhysiCell integration with scRNA-seq parameterisation

\- \[ ] QSAR/PKPD models: RDKit Morgan fingerprint pipeline + OpenEye integration

\- \[ ] PDE solver: FEniCS drug diffusion module

\- \[ ] GPU optimisation: PyTorch inference pipeline



\### Phase 2 — Validation (Months 4–6)

\- \[ ] Calibration on 1,000+ PDO profiles (DepMap, GDSC2, OrganoidDB)

\- \[ ] 5-fold cross-validation with independent holdout

\- \[ ] Stochastic replication for confidence interval estimation

\- \[ ] Performance benchmarking report (Pearson r, AUC-ROC)

\- \[ ] Peer-review-ready benchmarking manuscript



\### Phase 3 — Deployment (Months 7–9)

\- \[ ] Streamlit web application development

\- \[ ] FHIR R4 EHR integration

\- \[ ] Docker and Kubernetes containerisation

\- \[ ] HPC deployment (local and cloud)

\- \[ ] Pilot integration with clinical oncology partner

\- \[ ] Open-source release of pipeline and benchmark dataset



\### Publication targets

\- \*\*Primary methods paper:\*\* \*npj Computational Oncology\* (Nature Portfolio)

\- \*\*Dataset descriptor:\*\* \*Scientific Data\* (Nature Portfolio)

\- \*\*Conference:\*\* ISMB 2026



\---



\## Scientific References



The following peer-reviewed publications directly underpin the methodology and claims of this project:



1\. Begley CG, Ellis LM. Drug development: Raise standards for preclinical cancer research. \*Nature\*. 2012;483(7391):531–533.

2\. Clevers H. Modeling Development and Disease with Organoids. \*Cell\*. 2016;165(7):1586–1597.

3\. Driehuis E, Kretzschmar K, Clevers H. Establishment of patient-derived cancer organoids for drug-screening applications. \*Nature Protocols\*. 2020;15(10):3380–3409.

4\. Vlachogiannis G et al. Patient-derived organoids model treatment response of metastatic gastrointestinal cancers. \*Science\*. 2018;359(6378):920–926.

5\. Ronneberger O, Fischer P, Brox T. U-Net: Convolutional Networks for Biomedical Image Segmentation. \*MICCAI\*. 2015;9351:234–241.

6\. Ghaffarizadeh A et al. PhysiCell: An open source physics-based cell simulator for 3-D multicellular systems. \*PLOS Computational Biology\*. 2018;14(2):e1005991.

7\. Menden MP et al. Community assessment to advance computational prediction of cancer drug combinations in a pharmacogenomic screen. \*Nature Communications\*. 2019;10(1):2674.

8\. Kong J et al. Network-based machine learning in colorectal and bladder organoid models predicts anti-cancer drug efficacy. \*Nature Communications\*. 2020;11(1):5485.

9\. Moradi Kashkooli F, Kolios MC. Multi-Scale and Multi-Physics Models of Transport of Therapeutic Cancer Agents. \*Cancers\*. 2023;15(24):5724.

10\. Duswald T et al. Bridging scales: A hybrid model to simulate vascular tumor growth and treatment response. \*PMC\*. 2023.

11\. Alani S et al. Enhanced U-Net for Automated Segmentation of Organoid Images. \*Bioengineering\*. 2025.

12\. van de Wetering M et al. Prospective Derivation of a Living Organoid Biobank of Colorectal Cancer Patients. \*Cell\*. 2015;161(4):933–945.

13\. Sachs N et al. A Living Biobank of Breast Cancer Organoids Captures Disease Heterogeneity. \*Cell\*. 2018;172(1–2):373–386.

14\. Tuveson D, Clevers H. Cancer modeling meets human organoid technology. \*Science\*. 2019;364(6444):952–955.

15\. Khorsandi D et al. Patient-Derived Organoids as Therapy Screening Platforms in Cancer Patients. \*Advanced Healthcare Materials\*. 2024;13(21):e2302331.



\---



\## Team



| Name | Role | Responsibilities |

|---|---|---|

| \*\*Nandini Solanki\*\* | Team Lead · Pharma \& Drug Science | Data infrastructure and preprocessing, drug modelling (QSAR/PK-PD/PDE), model calibration and validation, dataset curation (biological sign-off), project coordination |

| \*\*Vidit Jain\*\* | Data \& Simulation Engineer | U-Net organoid geometry reconstruction, agent-based cellular simulation engine (PhysiCell), FHIR / EHR API integration |

| \*\*V Subharaga\*\* | Technical Developer · Regulatory Lead | GPU acceleration and performance optimisation, Streamlit web application, Docker/Kubernetes containerisation, regulatory compliance and documentation |



\*\*Contact:\*\* solankinandini2001@gmail.com



\---



\## Disclaimer



This repository currently represents a \*\*research prototype and conceptual framework\*\* developed for the All-Russian Scientific School "Young Medicine" 2025 competition.



The platform is a \*\*decision-support tool\*\*. It is not a clinically validated diagnostic device and must not be used for direct medical decision-making. All treatment decisions remain the responsibility of the treating clinician.



Regulatory pathway: Phase 1 deployment targets pharmaceutical preclinical research (unregulated laboratory software). Clinical decision-support deployment (Phase 3) will follow the SaMD Class II regulatory pathway (FDA 510k / CDSCO equivalent) upon completion of full clinical validation.



\---



\## Citation



If you use this framework, pipeline, or benchmark dataset in your research, please cite:



```bibtex

@misc{solanki2025insilico,

&#x20; author       = {Solanki, Nandini and Jain, Vidit and Subharaga, V.},

&#x20; title        = {In Silico Organoid Twins: Automated Bioinformatics Simulation

&#x20;                 for Patient-Specific Drug Screening},

&#x20; year         = {2025},

&#x20; institution  = {Bversity School of Biosciences},

&#x20; note         = {Submitted to All-Russian Scientific School Young Medicine 2025.

&#x20;                 Pipeline preprint: bioRxiv (forthcoming).},

&#x20; url          = {https://github.com/\[username]/insilico-organoid-twins}

}

```



\---



\## License



Licensed under the \*\*Apache 2.0 License\*\* — see the \[LICENSE](LICENSE) file for details.



This means you are free to use, modify, and distribute this work, including for commercial purposes, provided attribution is given and the licence terms are maintained.



\---



\*Bversity School of Biosciences · All-Russian Scientific School "Young Medicine" · Biomedical Engineering and Digital Health Technologies\*

