<div align="center">

In Silico Organoid Twins
Automated Bioinformatics Simulation for Patient-Specific Drug Screening

![Status](https://img.shields.io/badge/Status-Prototype_Development-orange)
![Competition](https://img.shields.io/badge/Submitted_To-Young_Medicine_2025-teal)
![Institution](https://img.shields.io/badge/Institution-Bversity_School_of_Biosciences-navy)

</div>

Decision-support tool — the oncologist decides treatment. Our output informs; it does not prescribe.

---

Project Overview

In Silico Organoid Twins is a multi-scale computational platform that digitally replicates the drug response behaviour of patient-derived organoids (PDOs) — three-dimensional tumour structures cultivated from a patient's own cancer cells. Rather than growing physical organoids in a laboratory (a process requiring 4–6 weeks and over USD 10,000 per test panel), the platform computationally simulates the same biological processes from two clinical inputs: a histological biopsy image and a patient gene expression profile.

The platform was developed as a competition submission to the All-Russian Scientific School "Young Medicine" 2025 under Biomedical Engineering and Digital Health Technologies.

Institution: Bversity School of Biosciences

PDOs are currently among the most predictive preclinical cancer models available, achieving high sensitivity in treatment response prediction compared to conventional 2D culture systems. However, scalability limitations make them impractical for large-scale screening workflows. This project addresses that bottleneck computationally.

🚀 **Live Demo:** [in-silico-organoid-twins.vercel.app](https://in-silico-organoid-twins.vercel.app/)

---

Problem Statement

The oncology drug development ecosystem faces a severe translational bottleneck caused by:

• High preclinical failure rates
• Expensive laboratory organoid workflows
• Long screening timelines
• Limited accessibility of precision oncology infrastructure
• Inability to scale patient-specific screening

Current physical PDO workflows require:

| Limitation    | Current Physical PDO Workflow            |
| ------------- | ---------------------------------------- |
| Time          | 4–6 weeks per experimental cycle         |
| Cost          | More than USD 10,000 per test panel      |
| Throughput    | Limited organoid capacity                |
| Variability   | Significant batch-to-batch variability   |
| Accessibility | Restricted specialist infrastructure     |
| Scalability   | Difficult high-throughput implementation |

These limitations reduce the practical accessibility of precision oncology approaches.

---

Proposed Solution

In Silico Organoid Twins builds a computational Digital Twin platform capable of simulating patient-specific tumour behaviour and virtual drug response.

The platform integrates:

• AI-based image segmentation
• Agent-based tumour simulation
• Drug diffusion and response modelling
• GPU-accelerated virtual screening
• Browser-based clinical interaction

Simplified workflow:

INPUT → AI reconstruction → Tumour simulation → Drug screening → Response prediction

Expected turnaround time: 1–4 hours instead of multiple weeks.

---

Pipeline Architecture

Module 1 — Organoid Geometry Reconstruction

• Histopathological image segmentation using U-Net architectures
• Reconstruction of tumour topology and spatial organisation
• Generation of 3D organoid mesh structures

Module 2 — Cellular Dynamics Simulation

• Agent-Based Modeling using PhysiCell
• Cell proliferation, apoptosis, signalling, and interaction simulation
• Incorporation of transcriptomic information into virtual cell agents

Module 3 — Drug Modeling and Diffusion

• QSAR-based molecular property prediction
• PDE-driven drug diffusion and metabolic transport modelling
• Virtual IC50 prediction and dose-response estimation

Module 4 — Clinical Interface

• Streamlit-based clinician dashboard
• Real-time simulation monitoring
• PDF and CSV result generation
• GPU-accelerated inference support

---

Technologies and Tools

| Component                   | Tools                    |
| --------------------------- | ------------------------ |
| Image Segmentation          | U-Net, PyTorch, StarDist |
| Transcriptomics             | Scanpy, Seurat           |
| Agent-Based Modeling        | PhysiCell                |
| Drug Modeling               | RDKit, OpenEye           |
| PDE Simulation              | FEniCS                   |
| Hyperparameter Optimization | Optuna                   |
| Data Processing             | NumPy, SciPy, pandas     |
| Interface                   | Streamlit                |
| Containerization            | Docker, Kubernetes       |

---

Validation Strategy

The system is designed to be validated against:

• Public pharmacogenomic datasets
• Patient-derived organoid studies
• Experimental IC50 measurements
• Cross-validation benchmarking workflows

Planned metrics include:

• Pearson correlation for predicted vs experimental drug response
• AUC-ROC for classification accuracy
• Confidence interval estimation via stochastic simulation

---

Expected Outcomes

| Metric          | Physical PDO | In Silico Organoid Twin |
| --------------- | ------------ | ----------------------- |
| Cost            | High         | Significantly Reduced   |
| Turnaround Time | Weeks        | Hours                   |
| Throughput      | Limited      | High                    |
| Accessibility   | Restricted   | Scalable                |
| Infrastructure  | Wet Lab      | Computational Platform  |

The project aims to improve accessibility, scalability, and speed in precision oncology workflows.

---

Repository Contents

| File                               | Description                           |
| ---------------------------------- | ------------------------------------- |
| README.md                          | Repository overview and documentation |
| InSilico_Organoid_Twins_Final.pptx | Final competition pitch deck          |
| organoid_project.docx              | Full project documentation            |
| InSilico_OrgTwins_Brief.pdf        | Two-page project brief                |

Pipeline source code and computational modules will be added in future commits.

---

Scientific Foundation

The project is conceptually supported by prior work in:

• Patient-derived organoid systems
• Computational oncology
• Biomedical image segmentation
• Agent-based tumour modeling
• Drug-response prediction frameworks

Key references include:

• Clevers H. Cell (2016) — Organoid disease modeling
• Ronneberger et al. MICCAI (2015) — U-Net segmentation
• Ghaffarizadeh et al. PLOS Computational Biology (2018) — PhysiCell framework
• Vlachogiannis et al. Science (2018) — Organoid treatment response prediction
• Tuveson and Clevers Science (2019) — Cancer modeling using organoids

Full bibliography is available in the project documentation.

---

Roadmap

Phase 1 — Development

• Data preprocessing pipeline
• U-Net training and segmentation engine
• Agent-based simulation integration
• Drug diffusion modeling
• GPU acceleration optimization

Phase 2 — Validation

• Pharmacogenomic benchmarking
• Cross-validation workflows
• Performance analysis
• Benchmark dataset curation

Phase 3 — Deployment

• Clinical dashboard implementation
• HPC deployment
• Containerized infrastructure
• Open-source release

---

Team

| Name            | Role                                    |
| --------------- | --------------------------------------- |
| Nandini Solanki | Team Lead — Pharma and Drug Science     |
| Vidit Jain      | Data and Simulation Engineer            |
| V Subharaga     | Technical Developer and Regulatory Lead |

Contact: [solankinandini2001@gmail.com](mailto:solankinandini2001@gmail.com)

---

Disclaimer

This repository represents a research prototype and conceptual framework developed for the All-Russian Scientific School "Young Medicine" competition.

The platform is a decision-support system and is not a clinically validated diagnostic device. All treatment decisions remain under clinician supervision.

---

© 2025 Nandini Solanki, Vidit Jain, V Subharaga

Bversity School of Biosciences · Young Medicine 2025 · Biomedical Engineering and Digital Health Technologies
