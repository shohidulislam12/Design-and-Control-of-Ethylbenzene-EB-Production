# 🏭 Ethylbenzene (EB) Production — Design and Control Process Simulation

A complete **process flowsheet simulation** for the production of **Ethylbenzene (EB)** via the **alkylation of benzene with ethylene**, modeled using **COFE (CAPE-OPEN Flowsheet Environment)** and **ChemSep**.

![COFE](https://img.shields.io/badge/Simulator-COFE-green)
![ChemSep](https://img.shields.io/badge/Separation-ChemSep-blue)
![CAPE-OPEN](https://img.shields.io/badge/Standard-CAPE--OPEN-orange)
![License](https://img.shields.io/badge/License-MIT-yellow)
![Status](https://img.shields.io/badge/Status-Converged-success)

---

# 📖 Table of Contents

- [Overview](#-overview)
- [Process Description](#-process-description)
- [Reactions](#-reactions)
- [Flowsheet](#-flowsheet)
- [Unit Operations](#-unit-operations)
- [Stream Results](#-stream-results)
- [Software Used](#-software-used)
- [How to Run](#-how-to-run)
- [Key Learnings](#-key-learnings)
- [References](#-references)
- [Author](#-author)
- [License](#-license)

---

# 🔬 Overview

**Ethylbenzene (EB, C₈H₁₀)** is one of the most important petrochemical intermediates in the chemical industry, with worldwide production exceeding **30 million tons annually**.

Its primary application is the manufacture of **styrene monomer**, which is further polymerized into:

- Polystyrene (PS)
- Acrylonitrile Butadiene Styrene (ABS)
- Styrene Acrylonitrile (SAN)
- Styrene-Butadiene Rubber (SBR)

This project simulates the **liquid-phase alkylation of benzene with ethylene** using acidic zeolite catalysts such as:

- **ZSM-5**
- **Beta Zeolite**

The simulation includes:
- Feed preparation
- Multi-stage reactor system
- Pressure control
- Benzene recycle loop
- Product purification using ChemSep

---

# ⚙️ Process Description

The process is divided into three major sections:

---

## 1️⃣ Feed Preparation & Recycle Section

- Fresh benzene is mixed with recycled benzene in **Mixer_1**
- Ethylene feed is compressed to reactor pressure
- Both streams are preheated before entering the reactor system
- Mixed feed enters the alkylation section under controlled conditions

---

## 2️⃣ Reaction Section

The reaction system consists of two reactors in series:

### 🔹 Reactor_1
- Main alkylation reactor
- Benzene reacts with ethylene to produce ethylbenzene

### 🔹 Valve_1
- Reduces pressure between reactor stages
- Helps maintain reactor control and stability

### 🔹 Reactor_2
- Secondary conversion reactor
- Enhances overall conversion
- Handles transalkylation and side reactions

---

## 3️⃣ Separation Section

The reactor effluent enters a separation train consisting of:

### 🔹 ChemSep Distillation Column_1
- Recovers unreacted benzene overhead
- Recycles benzene back to the feed section

### 🔹 ColumnFlash_2
- Separates high-purity Ethylbenzene product
- Removes heavy by-products such as:
  - p-Diethylbenzene
  - Polyethylbenzenes

---

# 🧪 Reactions

## Main Reaction — Alkylation

```math
C_6H_6 + C_2H_4 \rightarrow C_8H_{10}
```

### Product:
- **Ethylbenzene (EB)**

---

## Side Reaction — Over-Alkylation

```math
C_8H_{10} + C_2H_4 \rightarrow C_{10}H_{14}
```

### By-product:
- **p-Diethylbenzene**

---

## Reaction Characteristics

| Parameter | Value |
|---|---|
| Reaction Type | Liquid-phase alkylation |
| Catalyst | ZSM-5 / Beta Zeolite |
| Nature | Highly exothermic |
| Heat of Reaction | ΔH ≈ −114 kJ/mol |
| Operating Temperature | 320–435 K |
| Operating Pressure | 20 atm |

---

# 🧩 Flowsheet

```text
Fresh Benzene ──► Mixer_1 ──► Pump ──┐
                                     │
Recycle Benzene ◄────────────────────┘
                                     ▼
Fresh Ethylene ─► Compressor ─► Heater
                                     ▼
                                Mixer_2
                                     ▼
                                Reactor_1
                                     ▼
                                  Valve
                                     ▼
                                Reactor_2
                                     ▼
                             Distillation Column
                                     ▼
                           Flash Separation Unit
                           ├──► Ethylbenzene Product
                           └──► Heavy By-products
```

> Replace with actual process image:

```markdown
![Flowsheet](flowsheet.png)
```

---

# 🛠 Unit Operations

| Unit | Type | Function |
|---|---|---|
| **Mixer_1** | Mixer | Combines fresh + recycle benzene |
| **Pump_4** | Pump | Pressurizes benzene stream |
| **Compressor_1** | Compressor | Compresses ethylene feed |
| **HeaterCooler_3** | Heat Exchanger | Feed preheating |
| **Mixer_2** | Mixer | Combines benzene + ethylene |
| **Reactor_1** | Conversion Reactor | Primary alkylation |
| **Mixer_3** | Mixer | Stream conditioning |
| **Valve_1** | Throttling Valve | Pressure reduction |
| **Reactor_2** | Conversion Reactor | Secondary reaction stage |
| **ChemSep_1** | Distillation Column | Benzene recovery |
| **ColumnFlash_2** | Flash Separator | EB purification |
| **Pump_2 / Pump_30** | Pumps | Recycle stream handling |

---

# 📊 Stream Results

| Stream | Pressure (atm) | Temperature (K) | Flow (kmol/h) | Description |
|---|---:|---:|---:|---|
| Fresh Ethylene | 1 | 320 | 630.6 | Feed |
| Fresh Benzene | 1 | 320 | 630.6 | Feed |
| Recycle Stream | 1 | 316.67 | 969.37 | Benzene recycle |
| 4 | 20 | 317.99 | 1599.97 | Mixed benzene feed |
| 6 | 20 | 320 | 630.6 | Compressed ethylene |
| 8 | 20 | 318.97 | 2230.57 | Reactor_1 inlet |
| 9 | 20 | 328.10 | 1606.18 | Reactor_1 outlet |
| 11 | 20 | 381.96 | 1888.34 | Reactor_2 inlet |
| 13 | 19 | 422.97 | 1888.34 | Reactor_2 outlet |
| 14 | 0.3 | 432 | 1882.13 | Separation feed |
| 15 | 0.3 | 316.83 | 912.76 | Column bottoms |
| **16 (EB Product)** | **0.1** | **339.91** | **630.60** | **High-purity Ethylbenzene** |
| 17 | 0.1 | 381.13 | 282.16 | Heavy by-products |

---

✅ **Simulation converged successfully with no errors reported.**

> Full stream compositions and mole fractions are available inside the `.fsd` simulation file.

---

# 💻 Software Used

| Software | Purpose |
|---|---|
| **COCO Simulator (COFE)** | Process flowsheet simulation |
| **ChemSep LITE** | Rigorous distillation modeling |
| **TEA** | Thermodynamic property package |
| **CORN** | Reaction package |

---

## Official Websites

### COCO Simulator
https://www.cocosimulator.org/

### ChemSep
https://www.chemsep.com/

---

# 🚀 How to Run

## Step 1 — Install COCO Simulator

Download from:

```text
https://www.cocosimulator.org/index_download.html
```

Includes:
- COFE
- TEA
- CORN
- COUSCOUS

---

## Step 2 — Install ChemSep LITE

Download from:

```text
https://www.chemsep.com/downloads/index.html
```

---

## Step 3 — Clone Repository

```bash
git clone https://github.com/your-username/Ethylbenzene-Production-Simulation.git
cd Ethylbenzene-Production-Simulation
```

---

## Step 4 — Open the Simulation

1. Launch **COFE**
2. Open:
   ```text
   Design and control EB process.fsd
   ```
3. Click **Solve (▶)**

---

# 🎯 Key Learnings

- Designed a complete alkylation-based petrochemical process
- Converged recycle loops successfully
- Modeled multiple reactors in series
- Simulated rigorous distillation using ChemSep
- Applied process control concepts for stable operation
- Validated material and energy balances
- Improved understanding of CAPE-OPEN based simulators
- Gained practical experience in industrial reactor-separation systems

---

# 📚 References

1. Turton, R., Shaeiwitz, J. A., Bhattacharyya, D., & Whiting, W. B. (2018). *Analysis, Synthesis, and Design of Chemical Processes* (5th ed.). Prentice Hall.

2. Luyben, W. L. (2011). *Design and control of the ethylbenzene process*. AIChE Journal, 57(3), 655–670.

3. Perego, C., & Ingallina, P. (2002). *Recent advances in industrial alkylation of aromatics*. Catalysis Today, 73(1–2), 3–22.

4. Welch, V. A., Fallon, K. J., & Gelbke, H. P. (2005). *Ethylbenzene*. Ullmann's Encyclopedia of Industrial Chemistry.

5. Woodle, G. R. (2006). *Ethylbenzene*. Encyclopedia of Chemical Processing.

6. Degnan, T. F., Smith, C. M., & Venkat, C. R. (2001). *Alkylation of aromatics with ethylene and propylene*. Applied Catalysis A.

7. COCO Simulator Documentation  
   https://www.cocosimulator.org/

8. ChemSep Documentation  
   https://www.chemsep.com/

9. Sinnott, R. K., & Towler, G. (2020). *Chemical Engineering Design* (6th ed.). Butterworth-Heinemann.

10. Seider, W. D., Lewin, D. R., Seader, J. D., Widagdo, S., Gani, R., & Ng, K. M. (2017). *Product and Process Design Principles* (4th ed.). Wiley.

---

# 👨‍💻 Author

## MD. Shohidul Islam Sifat

Chemical Engineering Student | Process Simulation & Design Enthusiast

### Academic Background
- Department of Chemical Engineering
- Jashore University of Science and Technology (JUST)

### Connect With Me

- 🔗 LinkedIn: https://www.linkedin.com/in/shohidulislam200/
- 💻 GitHub: https://github.com/shohidulislam12

