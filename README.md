![image](https://github.com/user-attachments/assets/7f226b55-0a55-4c57-9ce6-802a8bd29a3e)

# GCNN-RNN-SGSIM — Risk-Aware Ore-Waste Classification with Drift Learning and Conditional Geostatistical Simulation

**Author:** Keyumars Anvari  
**Supervisor:** Professor Jörg Benndorf  
**Affiliation:** Institute of Mine Surveying and Geodesy, TU Bergakademie Freiberg, Freiberg, Germany

---

## 📄 Project Description

This repository contains a compact, method-focused implementation of **GCNN-RNN-SGSIM**, a hybrid workflow for block-support grade modelling, uncertainty quantification, and risk-aware ore-waste classification.

The workflow combines two complementary components. First, a **GCNN-RNN drift model** is used to learn systematic spatial structure from grouped drillhole data. Second, **Sequential Gaussian Simulation** is applied to the residual component so that conditional spatial uncertainty is preserved through multiple block realizations. The resulting outputs are intended for decision-oriented resource modelling in settings where both local estimates and uncertainty-aware classification are required.

---

## 🛠️ Features

- **Hybrid drift-plus-simulation workflow**
- **Block-support grade modelling**
- **Grouped borehole validation for leakage-safe drift learning**
- **Residual conditional simulation in normal-score space**
- **Probability of ore estimation**
- **Decision-oriented block summaries**
- **Single-script configuration through a dataclass**
- **Runnable fallback path when external files are not provided**

---

## 🗺️ Workflow Overview

1. Load sample, block, and optional zone tables  
2. Prepare coordinates, grade values, and grouping information  
3. Transform grades to log space and normal-score space  
4. Train the GCNN-RNN drift model using grouped borehole splits  
5. Estimate residual spatial continuity  
6. Run conditional simulation of the residual component  
7. Reconstruct block realizations in grade space  
8. Compute block-wise summaries and ore probabilities  
9. Export reproducible outputs for downstream analysis  

---

## 📥 Input Format

### Sample table
Required columns:
- `x`
- `y`
- `z`
- `grade`
- `borehole`

Optional column:
- `zone`

### Block table
Required columns:
- `x`
- `y`
- `z`

Optional column:
- `zone`

### Zone table
Required columns:
- `x`
- `y`
- `z`
- `zone`

---

## 📤 Output Files

The script writes the following files to the selected output directory:

- `summary.csv`
- `block_estimates.csv`
- `realizations.npy`
- `config.json`

---

## 📚 Dependencies

Install requirements with:

```bash
pip install -r requirements.txt
```

**Main libraries used:**
- `numpy`
- `pandas`
- `scikit-learn`
- `tensorflow`

---

## 🚀 How to Run

Run with external input files:

```bash
python main.py --samples path/to/samples.csv --blocks path/to/blocks.csv --zones path/to/zones.csv --output-dir results
```

Run without external input files:

```bash
python main.py
```

Optional arguments:

```bash
--seed
--n-realizations
--output-dir
```

---

## 📁 Repository Structure

```text
GCNN-RNN-SGSIM/
│
├── main.py
├── requirements.txt
├── LICENSE
├── README.md
└── results/
```

---

## ⚠️ Notes

- The workflow is written for transparent and reproducible execution.
- If zone labels are not supplied for samples or blocks, they are inferred from the zone table by nearest-neighbor assignment.
- When no user files are provided, the script runs through an internal fallback path so that the workflow remains directly executable.
- The repository is intended to present the method clearly and compactly, without embedding a study-specific dataset in the code base.
- An explicit **open-source LICENSE file** should be included in the repository before journal submission.

---

## 📬 Contact

> Keyumars Anvari  
> Institute of Mine Surveying and Geodesy  
> TU Bergakademie Freiberg  
> Email: keyumarsanvari@gmail.com  
> Email: Keyumars.Anvari@doktorand.tu-freiberg.de
