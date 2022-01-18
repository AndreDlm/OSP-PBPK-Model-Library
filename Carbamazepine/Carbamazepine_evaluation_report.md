# Building and Evaluation of a PBPK Model for Carbamazepine in Adults



| Version                                         | TODO                                                         |
| ----------------------------------------------- | ------------------------------------------------------------ |
| Model file and Evaluation Report                | TODO                                                         |
| based on *Model Snapshot* and *Evaluation Plan* | 1.0<br />(https://github.com/Open-Systems-Pharmacology/Carbamazepine-Model/releases/tag/v1.0) |
| OSP Version                                     | 10.0                                                         |
| Qualification Framework Version                 | 2.1                                                          |
| Author                                          | André Dallmann ([AndreDlm](https://github.com/AndreDlm))     |



# Table of Contents
  * [1 Introduction](#1-introduction)
  * [2 Methods](#2-methods)
    * [2.1 Modeling Strategy](#21-modeling-strategy)
    * [2.2 Data](#22-data)
    * [2.3 Model Parameters and Assumptions](#23-model-parameters-and-assumptions)
  * [3 Results and Discussion](#3-results-and-discussion)
    * [3.1 Final input parameters](#31-final-input-parameters)
    * [3.2 Diagnostics Plots](#32-diagnostics-plots)
    * [3.3 Concentration-Time Profiles](#33-concentration-time-profiles)
  * [4 Conclusion](#4-conclusion)
  * [5 References](#5-references)
# 1 Introduction
Carbamazepine, sold under the trade name Tegretol<sup>®</sup> among others, is an anticonvulsant medication used primarily to treat epilepsy and neuropathic pain. Other indications include schizophrenia where it is used as an adjunctive treatment along with other medications, and bipolar disorder where it is used as a second-line agent. Carbamazepine is typically taken by mouth on empty stomach or together with meals, depending on the administered formulation. With the exception of e.g. grapefruit juice, the intake of food was generally found to have no significant impact on carbamazepine pharmacokinetics ([Tedeschi 1981](#5-References), [McLean 2001](#5-References)).

Carbamazepine is extensively metabolized by various enzymes including CYP2B6, 2C8, 3A4, and UGT2B7 ([Kerr 1994](#5-References), [Pelkonen 2001](#5-References), [Staines 2004](#5-References)). The main metabolites are carbamazepine-10,11-epoxide which is pharmacologically active and 10,11-dihydroxycarbamazepine ([Eichelbaum 1985](#5-References)). Following oral administration the major dose fraction is metabolized to carbamazepine-10,11-epoxide ([Eichelbaum 1985](#5-References), [Tomson 1983](#5-References)). This reaction is mainly catalyzed by CYP3A4, with some contribution from CYP2C8 ([Kerr 1994](#5-References)). After oral administration, a minor fraction of the dose (approximately 1 - 3%) is excreted unchanged in urine ([Bernus 1994](#5-References), [Morselli 1975](#5-References)), while approximately 1% of the dose can be recovered as unchanged drug in the bile ([Terhaag 1978](#5-References)). The primary metabolite carbamazepine-10,11-epoxide is cleared by metabolism via epoxide hydroxylase 1 (EPHX1) to its trans-diol form and by glomerular filtration ([Kitteringham 1996](#5-References)). 

Carbamazepine is classified by the U.S. Food and Drug Administration (FDA) as a strong CYP3A4 and CYP2B6 inducer (https://www.fda.gov/drugs/drug-interactions-labeling/drug-development-and-drug-interactions) and hence induces its own metabolism.

The herein presented coupled parent-metabolite PBPK model for carbamazepine and carbamazepine-10,11-epoxide represents an update of the model published by Fuhr et al. ([Fuhr 2021](#5-References)). In comparison to the published version by Fuhr et al. ([Fuhr 2021](#5-References)), the CYP3A4 induction parameters have been updated and data from additional clinical studies were used for model evaluation.
# 2 Methods


## 2.1 Modeling Strategy
The general workflow for building an adult PBPK model has been described by Kuepfer et al. ([Kuepfer 2016](#5-references)). Relevant information on the anthropometry (height, weight) was gathered from the respective clinical study, if reported. Information on physiological parameters (e.g. blood flows, organ volumes, hematocrit) in adults was gathered from the literature and has been incorporated in PK-Sim<sup>®</sup>) as described previously ([Willmann 2007](#5-references)). The  applied activity and variability of plasma proteins and active processes that are integrated into PK-Sim<sup>®</sup> are described in the publicly available 'PK-Sim<sup>®</sup> Ontogeny Database Version 7.3' ([PK-Sim Ontogeny Database Version 7.3](#5-references)).

The PBPK model was developed based on publicly available clinical data of adult healthy subjects. In a first step, a model was developed for carbamazepine-10,11-epoxide using pharmacokinetic data from three clinical studies administering carbamazepine-10,11-epoxide at an oral dose ranging from 50 to 200 mg as solution or tablet. This model includes metabolism by EPHX1 and unchanged renal excretion via passive glomerular filtration. Thereafter, a model was developed for carbamazepine that was combined with the carbamazepine-10,11-epoxide model. For the development of the parent-metabolite model, pharmacokinetic data from various clinical studies were used that covered a dosing range from 10 to 600 mg carbamazepine in different formulations (solution, immediate release and extended release formulations), administered under fasted conditions or together with food. The carbamazepine model includes metabolism by CYP2B6, 2C8, and 3A4 as well as an unspecific clearance pathway (implemented as `liver plasma clearance` process) and as minor elimination pathway unchanged renal excretion. Induction of CYP2B6, 3A4, and EPHX1 by carbamazepine was included.

Unknown parameters (see below) were identified using the Parameter Identification module provided in PK-Sim<sup>®</sup>. Structural model selection was mainly guided by visual inspection of the resulting description of data and biological plausibility. Further details on model building are been described elsewhere ([Fuhr 2021](#5-References)).

Details about input data (physicochemical, *in vitro* and clinical) can be found in [Section 2.2](#22-Data).

Details about the structural model and its parameters can be found in [Section 2.3](#23-Model-Parameters-and-Assumptions).


## 2.2 Data
### 2.2.1	In vitro / physicochemical Data

A literature search was performed to collect available information on physicochemical properties of carbamazepine and carbamazepine-10,11-epoxide. The information is summarized in the table below. 

| **Parameter**   | **Unit** | **Value**       | Source                                                       | **Description**                                 |
| :-------------- | -------- | --------------- | ------------------------------------------------------------ | ----------------------------------------------- |
| **Carbamazepine** |  |  |  |  |
| MW              | g/mol    | 236.27    | [DrugBank DB00564](#5-References) | Molecular weight                                |
| logP (calculated)                        |                          | 1.54                                   | [Austin 2002](#5-References)      | Partition coefficient between octanol and water         |
| logP (calculated)                        |                          | 2.1                                    | [DrugBank DB00564](#5-References) | Partition coefficient between octanol and water         |
| logP (calculated)                        |                          | 2.77                                   | [DrugBank DB00564](#5-References) | Partition coefficient between octanol and water         |
| Solubility (pH) | µg/mL   | 336 (6.2)                              | [Annaert 2010](#5-References) | Solubility in human intestinal fluid |
| Solubility (pH) | µg/mL | 283 (7.0)                              | [Söderlind 2010](#5-References) | Solubility in human intestinal fluid |
| Solubility (pH) | µg/mL                    | 306 (6.9)                              | [Clarysse 2011](#5-References)    | Solubility in fasted human intestinal fluid             |
| f<sub>u</sub>                            |                          | 0.25                                   | [Pynnönen 1977](#5-References)    | Fraction unbound in plasma of healthy subjects          |
| f<sub>u</sub> | | 0.243 ± 0.013 [0.225 - 0.258]<sup>a</sup> | [Morselli 1975](#5-References) | Fraction unbound in plasma of healthy male subjects |
| f<sub>u</sub>                            |                          | 0.239                                  | [Di Salle 1974](#5-References)    | Fraction unbound in plasma of normal subjects           |
| f<sub>u</sub> | | 0.237 ± 0.031<sup>b</sup> | [Vinçon 1987](#5-References) | Fraction unbound in plasma of epileptic patients |
| f<sub>u</sub>                            |                          | 0.182 ± 0.05 [0.103 - 0.297]<sup>a</sup> | [Hooper 1975](#5-References)      | Fraction unbound in plasma of normal subjects           |
| K<sub>m</sub> CYP2B6                     | µM                       | 420                                    | [Pearce 2002](#5-References)      | CYP2B6 Michaelis-Menten constant                        |
| V<sub>max</sub> CYP2B6 | pmol/min/pmol rec enzyme | 0.429                                  | [Pearce 2002](#5-References)      | in vitro metabolic rate constant for recombinant CYP2B6 |
| K<sub>m</sub> CYP2C8 | µM                       | 757                                    | [Cazali 2003](#5-References)      | CYP2C8 Michaelis-Menten constant                        |
| V<sub>max</sub> CYP2C8 | pmol/min/pmol rec enzyme | 0.673                                  | [Cazali 2003](#5-References)      | in vitro metabolic rate constant for recombinant CYP2C8 |
| K<sub>m</sub> CYP3A4<sup>c</sup> | µM                       | 282                                    | [Pearce 2002](#5-References)      | CYP3A4 Michaelis-Menten constant                        |
| K<sub>m</sub> CYP3A4 (→CBZE)<sup>d</sup> | µM                       | 248                                    | [Huang 2004](#5-References)       | CYP3A4 Michaelis-Menten constant                        |
| K<sub>m</sub> UGT2B7 | µM                       | 214                                    | [Staines 2004](#5-References)     | UGT2B7 Michaelis-Menten constant                        |
| V<sub>max</sub> UGT2B7 | pmol/min/mg mic enzyme   | 0.79                                   | [Staines 2004](#5-References)     | in vitro metabolic rate constant for microsomal enzymes |
| Microsomal UGT2B7 | pmol/mg mic protein      | 82.9                                   | [Achour 2014](#5-References)      | Content of UGT2B7 proteins in liver microsomes          |
| Intestinal permeability                  | cm/min                   | 0.0258                                 | [Lennernäs 2007](#5-References) | Transcellular intestinal permeability        |
| **Carbamazepine-10,11-epoxide** |  |  |  |  |
| MW | g/mol | 252.27 | [DrugBank DBMET00291](#5-References) | Molecular weight |
| logP (calculated) |  | 1.58 | [DrugBank DBMET00291](#5-References) | Partition coefficient between octanol and water |
| logP (calculated) |  | 1.97 | [DrugBank DBMET00291](#5-References) | Partition coefficient between octanol and water |
| Solubility (pH) | µg/mL | 1340 (7.0) | [DrugBank DBMET00291](#5-References) | Solubility |
| f<sub>u</sub> |  | 0.489 ± 0.021 [0.468 - 0.518]<sup>a</sup> | [Morselli 1975](#5-References) | Fraction unbound in plasma of healthy male subjects |
| f<sub>u</sub> | | 0.491 ± 0.042<sup>b</sup> | [Vinçon 1987](#5-References) | Fraction unbound in plasma of epileptic patients |
<sup>a</sup> denotes mean ± standard deviation [range]

<sup>b</sup> denotes mean ± standard deviation

<sup>c</sup> refers to CYP3A4-mediated reaction forming other metabolites than carbamazepine-10,11-epoxide

<sup>d</sup> refers to CYP3A4-mediated reaction forming carbamazepine-10,11-epoxide


### 2.2.2	Clinical Data

A literature search was performed to collect available clinical data on carbamazepine and carbamazepine-10,11-epoxide in healthy adult subjects.

The following studies were used for model building and evaluation:

| Publication                                                 | Arm / Treatment / Information used for model building        |
| :---------------------------------------------------------- | :----------------------------------------------------------- |
| [Barzaghi 1987](#5-References)                              | Healthy subjects receiving a single oral dose of 400 mg carbamazepine |
| [Bedada 2015](#5-References)                                | Healthy subjects receiving a single oral dose of 200 mg carbamazepine |
| [Bedada 2016](#5-References)                                | Healthy subjects receiving a single oral dose of 200 mg carbamazepine |
| [Bernus 1994](#5-References)                                | Healthy subjects receiving two oral doses of 600 mg carbamazepine |
| [Bianchetti 1987](#5-References)                            | Healthy subjects receiving a single oral dose of 400 mg carbamazepine |
| [Burstein 2000](#5-References)                              | Healthy subjects receiving a multiple oral doses of carbamazepine, starting at 100 mg and escalating to 400 mg |
| [Caraco 1995](#5-References)                                | Healthy lean subjects receiving a single oral dose of 200 mg carbamazepine |
| [Caraco 1995](#5-References)                                | Obese but otherwise healthy subjects receiving a single oral dose of 200 mg carbamazepine |
| [Cawello 2000](#5-References)                               | Healthy subjects receiving a multiple oral doses of carbamazepine, starting at 100 mg and escalating to 200 mg |
| [Cotter 1977](#5-References)                                | Healthy subject receiving a single oral dose of 800 mg carbamazepine |
| [Dalton 1985a](#5-References)                               | Healthy subjects receiving a single oral dose of 600 mg carbamazepine |
| [Dalton 1985b](#5-References)                               | Healthy subjects receiving a single oral dose of 600 mg carbamazepine |
| [Eichelbaum 1985](#5-References)                            | Healthy subjects receiving a single oral dose of 200 mg carbamazepine |
| [Elqidra 2004](#5-References)                               | Healthy subjects receiving a single oral dose of 200 mg carbamazepine |
| [European Patent Application EP 1044681 A2](#5-References)  | Healthy subjects receiving a single oral dose of 400 and 600 mg carbamazepine |
| [Gérardin 1976](#5-References)                              | Healthy subjects receiving a single oral dose of 100, 200, and 600 mg carbamazepine |
| [Gérardin 1990](#5-References)                              | Healthy subjects receiving a single oral dose of 100 mg carbamazepine concomitantly with a single intravenous dose of 10 mg carbamazepine |
| [Ji 2008](#5-References)                                    | Healthy subjects receiving a multiple oral doses of carbamazepine, starting at 200 mg and escalating to 400 mg |
| [Kayali 1994](#5-References)                                | Healthy subjects receiving a single oral dose of 200 mg carbamazepine |
| [Kim 2005](#5-References)                                   | Healthy subjects receiving a single oral dose of 200 mg carbamazepine |
| [Kovacević 2009](#5-References)                             | Healthy subjects receiving a single oral dose of 400 mg carbamazepine |
| [Levy 1975](#5-References)                                  | Healthy subjects receiving a single oral carbamazepine dose of 6 mg/kg body weight |
| [McLean 2001](#5-References)                                | Healthy subjects receiving a single oral dose of 400 mg carbamazepine |
| [Meyer 1996](#5-References)                                 | Healthy subjects receiving a single oral dose of 200 mg carbamazepine |
| [Meyer 1998](#5-References)                                 | Healthy subjects receiving a single oral dose of 200 mg carbamazepine |
| [Miles 1989](#5-References)                                 | Healthy subjects receiving a multiple oral doses of 300 and 400 mg carbamazepine |
| [Møller 2001](#5-References)                                | Healthy subjects receiving a multiple oral doses of carbamazepine, starting at 100 mg and escalating to 400 mg |
| [Morselli 1975](#5-References)                              | Healthy subjects receiving a single oral dose of 400 mg carbamazepine |
| [Pisani 1988](#5-References)                                | Healthy subjects receiving a single oral dose of 100 mg carbamazepine-10,11-epoxide |
| [Pisani 1990](#5-References)                                | Healthy subjects receiving a single oral dose of 100 mg carbamazepine-10,11-epoxide |
| [Pisani 1992](#5-References)                                | Healthy subjects receiving a single oral dose of 100 mg carbamazepine-10,11-epoxide |
| [Pynnönen 1977](#5-References)                              | Healthy subjects receiving a single oral dose of 400 mg carbamazepine |
| [Rawlins 1975](#5-References)                               | Healthy subject receiving a single oral dose of 50, 100, and 200 mg carbamazepine |
| [Saint-Salvi 1987](#5-References)                           | Healthy subjects receiving a single oral dose of 200 mg carbamazepine |
| [Stevens 1998](#5-References)                               | Healthy subjects receiving multiple oral doses of 400 mg carbamazepine |
| [Strandjord 1975](#5-References)                            | Healthy subjects receiving a single oral dose of 400 mg carbamazepine |
| [Sumi 1987](#5-References)                                  | Healthy subjects receiving single oral doses of 200 mg carbamazepine and of 150 mg carbamazepine-10,11-epoxide |
| [Tomson 1983](#5-References)                                | Healthy subjects receiving single oral doses of 200 mg carbamazepine and of 50, 100, and 200 mg carbamazepine-10,11-epoxide |
| [US Patent Application - US 2009/0169619 A1](#5-References) | Healthy subjects receiving a single oral dose of 300 mg carbamazepine |
| [US Patent Application - US 2014/0302138 A1](#5-References) | Healthy subjects receiving a single oral dose of 400 mg carbamazepine |
| [Wada 1978](#5-References)                                  | Healthy subjects receiving a single oral dose of 200 mg carbamazepine |
| [Wong 1983](#5-References)                                  | Healthy subjects receiving a single oral dose of 400 mg carbamazepine |


## 2.3 Model Parameters and Assumptions
### 2.3.1	Absorption

Absorption of carbamazepine and carbamazepine-10,11-epoxide observed in clinical studies can be fully explained by passive absorption.

### 2.3.2	Distribution

For both carbamazepine and carbamazepine-10,11-epoxide, the observed clinical data was described by choosing the partition coefficient calculation by `Rodgers and Rowlands` and cellular permeability calculation by `PK-Sim Standard`. 

### 2.3.3	Metabolism, Elimination and Induction

Carbamazepine is metabolized by CYP2B6, 2C8, 3A4, and UGT2B7 ([Kerr 1994](#5-References), [Pelkonen 2001](#5-References), [Staines 2004](#5-References)). and a minor fraction of the dose (approximately 1%) is excreted unchanged in urine ([Bernus 1994](#5-References), [Morselli 1975](#5-References)). Carbamazepine-10,11-epoxide is cleared by metabolism via epoxide hydroxylase 1 (EPHX1) and glomerular filtration ([Kitteringham 1996](#5-References)). 

Induction of CYP2B6 and 3A4 was taken into account ([Eichelbaum 1985](#5-References)) and it was assumed that carbamazepine also induces EPHX1 ([Eichelbaum 1985](#5-References)). Carbamazepine induces CYP2B6 and 3A4 via the CAR pathway ([Faucette 2007](#5-References)); therefore, the same EC<sub>50</sub> value was used in the model for induction of CYP2B6, 3A4, and EPHX1. The associated E<sub>max</sub> values were optimized.

### 2.3.4	Automated Parameter Identification

The parameter identification tool in PK-Sim<sup>®</sup> has been used to estimate selected model parameters. The result of the final parameter identification is shown in the table below:

| Model Parameter            | Optimized Value | Unit |
| -------------------------- | --------------- | ---- |
| **Carbamazepine** |  |  |
| `Lipophilicity` | 2.00   |        |
| `Specific clearance` (total hepatic clearance process) | 0.015 | 1/min |
| `kcat` (CYP3A4)<sup>a</sup>                             | 0.200           | 1/min  |
| `kcat` (→ CBZE via CYP3A4)<sup>b</sup>                  | 0.750           | 1/min  |
| `Emax` (CYP2B6)                                         | 17.0            |  |
| `Emax` (CYP3A4)                                         | 6.00            |        |
| `Emax` (EPHX1)                                          | 3.25            |        |
| `GFR fraction`                                          | 0.027           |        |
| `Dissolution time (50% dissolved)` (IR tablet, fasted)  | 200.0           | min    |
| `Dissolution shape` (IR tablet, fasted)                 | 0.740           |        |
| `Dissolution time (50% dissolved)` (IR tablet, fed)     | 100.0           | min    |
| `Dissolution shape` (IR tablet, fed)                    | 1.20            |        |
| `Dissolution time (50% dissolved)` (XR tablet, fasted) | 767.2 | min  |
| `Dissolution shape` (XR tablet, fasted) | 0.758 |   |
| `Dissolution time (50% dissolved)` (XR tablet, fed) | 436.4 | min |
| `Dissolution shape` (XR tablet, fed) | 1.159 | |
| `Dissolution time (50% dissolved)` (XR capsule, fasted) | 439.5 | min |
| `Dissolution shape` (XR capsule, fasted) | 0.794 | |
| `Dissolution time (50% dissolved)` (XR capsule, fed) | 361.4 | min |
| `Dissolution shape` (XR capsule, fed) | 2.127 | |
| **Carbamazepine-10,11-epoxide** |  | |
| `Lipophilicity` | 1.16 | |
| `Specific intestinal permeability (transcellular)` | 0.299 | cm/min |
| `Specific clearance` (EPHX1) | 0.010 | 1/min |
| `GFR fraction` | 0.213 | |
| `Dissolution time (50% dissolved)` | 200.0 | min |
| `Dissolution shape` | 0.754 | |

<sup>a</sup> refers to CYP3A4-mediated reaction forming other metabolites than carbamazepine-10,11-epoxide

<sup>b</sup> refers to CYP3A4-mediated reaction forming carbamazepine-10,11-epoxide


### 
# 3 Results and Discussion
The PBPK model for carbamazepine was developed and evaluated using publicly available clinical pharmacokinetic data from studies listed in [Section 2.2.2](#222-Clinical-Data).

The next sections show:

1. the final model parameters for the building blocks: [Section 3.1](#31-Final-Input-Parameters).
2. the overall goodness of fit: [Section 3.2](#32-Diagnostics-Plots).
3. simulated vs. observed concentration-time profiles for the clinical studies used for model building and for model verification: [Section 3.3](#33-Concentration-Time-Profiles).


## 3.1 Final input parameters
The compound parameter values of the final PBPK model are illustrated below.




### Compound: Carbamazepine

#### Parameters

Name                                             | Value          | Value Origin                                                                                                                                         | Alternative                     | Default
------------------------------------------------ | -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------- | -------
Solubility at reference pH                       | 17.7 mg/l      | Internet-Assumption-assumed water solubility                                                                                                         | DrugBank                        | False  
Reference pH                                     | 7              | Internet-Assumption-assumed water solubility                                                                                                         | DrugBank                        | False  
Solubility at reference pH                       | 336 µg/ml      | Publication-In Vitro-FaHIF (pH 5.4-7.1)                                                                                                              | Annaert 2010 - FaHIF            | False  
Reference pH                                     | 6.2            | Publication-In Vitro-FaHIF (pH 5.4-7.1)                                                                                                              | Annaert 2010 - FaHIF            | False  
Solubility at reference pH                       | 255.2 µg/ml    | Publication-In Vitro-FaSSIF (pH = ???)                                                                                                               | Annaert 2010 - FaSSIF           | False  
Reference pH                                     | 6.5            | Publication-In Vitro-FaSSIF (pH = ???)                                                                                                               | Annaert 2010 - FaSSIF           | False  
Solubility at reference pH                       | 336 µg/ml      | Parameter Identification-Parameter Identification-Value updated from '2020-01-14_' on 2020-01-15 09:37                                               | Clarysse 2011 - FaHIF           | False  
Reference pH                                     | 6.2            | Parameter Identification-Parameter Identification-Value updated from '2020-01-14_' on 2020-01-15 09:37                                               | Clarysse 2011 - FaHIF           | False  
Solubility at reference pH                       | 266 µg/ml      | Publication-In Vitro-FaSSIF                                                                                                                          | Clarysse 2011 - FaSSIF          | False  
Reference pH                                     | 6.5            | Publication-In Vitro-FaSSIF                                                                                                                          | Clarysse 2011 - FaSSIF          | False  
Solubility at reference pH                       | 170 µg/ml      | Publication-In Vitro-FaHIF (pH 6.2)                                                                                                                  | Heikkilä 2011                   | False  
Reference pH                                     | 6.2            | Publication-In Vitro-FaHIF (pH 6.2)                                                                                                                  | Heikkilä 2011                   | False  
Solubility at reference pH                       | 283 µg/ml      | Publication-In Vitro-FaHIF (pH 6.5-7.5)                                                                                                              | Söderlind 2010                  | False  
Reference pH                                     | 7              | Publication-In Vitro-FaHIF (pH 6.5-7.5)                                                                                                              | Söderlind 2010                  | False  
Solubility at reference pH                       | 236 µg/ml      | Publication-In Vitro                                                                                                                                 | Söderlind 2010 - FaSSIF         | False  
Reference pH                                     | 6.5            | Publication-In Vitro                                                                                                                                 | Söderlind 2010 - FaSSIF         | False  
Solubility at reference pH                       | 468 µg/ml      | Publication-In Vitro-pH = ???                                                                                                                        | Clarysse 2011 - Fed HIF         | False  
Reference pH                                     | 7              | Publication-In Vitro-pH = ???                                                                                                                        | Clarysse 2011 - Fed HIF         | False  
Solubility at reference pH                       | 524 µg/ml      | Publication-In Vitro                                                                                                                                 | Clarysse 2011 - FeSSIF          | False  
Reference pH                                     | 5              | Publication-In Vitro                                                                                                                                 | Clarysse 2011 - FeSSIF          | False  
Solubility at reference pH                       | 336 µg/ml      |                                                                                                                                                      | used in simulation              | True   
Reference pH                                     | 6.2            |                                                                                                                                                      | used in simulation              | True   
Lipophilicity                                    | 2.45 Log Units | Publication-In Vitro-logP                                                                                                                            | Dal Pozzo 1989                  | False  
Lipophilicity                                    | 2.1 Log Units  | Internet-logP                                                                                                                                        | AlogPS                          | False  
Lipophilicity                                    | 2.77 Log Units | Internet-logP                                                                                                                                        | ChemAxon                        | False  
Lipophilicity                                    | 2.77 Log Units | Publication-In Vitro-logD (6.5)                                                                                                                      | Annaert 2010                    | False  
Lipophilicity                                    | 2.77 Log Units | Publication-In Vitro-logD (6.5)                                                                                                                      | Clarysse 2011                   | False  
Lipophilicity                                    | 2.77 Log Units | Publication-In Vitro-logD (6.5)                                                                                                                      | Heikkilä 2011                   | False  
Lipophilicity                                    | 2.45 Log Units | Publication-In Vitro-logP, logD(7.4)                                                                                                                 | Winiwarter 1998                 | False  
Lipophilicity                                    | 2 Log Units    | Parameter Identification-Parameter Identification-Value updated from '2020-10-30_refit_no2C8-induction_CYP3A4-metabolism_EPHX1_' on 2020-11-04 10:58 | Optimized                       | True   
Fraction unbound (plasma, reference value)       | 24 %           |                                                                                                                                                      | DrugBank, FDA label             | False  
Fraction unbound (plasma, reference value)       | 25 %           |                                                                                                                                                      | Bertisson 1978                  | False  
Fraction unbound (plasma, reference value)       | 21 %           |                                                                                                                                                      | Johannessen and Strandjord 1972 | False  
Fraction unbound (plasma, reference value)       | 25 %           | Publication-In Vivo-determined froom saliva concentration                                                                                            | Pynnönen 1977                   | False  
Fraction unbound (plasma, reference value)       | 25 %           | Other-Assumption                                                                                                                                     | Optimized                       | True   
Specific intestinal permeability (transcellular) | 0.00043 cm/s   | Publication-In Vitro-Lennernaes2007                                                                                                                  | Literature Lennernaes2007       | True   
Is small molecule                                | Yes            |                                                                                                                                                      |                                 |        
Molecular weight                                 | 236.2686 g/mol | Internet-DrugBank                                                                                                                                    |                                 |        
Plasma protein binding partner                   | Albumin        |                                                                                                                                                      |                                 |        
#### Calculation methods

Name                    | Value              
----------------------- | -------------------
Partition coefficients  | Rodgers and Rowland
Cellular permeabilities | PK-Sim Standard    
#### Processes

##### Metabolizing Enzyme: CYP3A4-Huang et al 2004 - CBZ-E

Molecule: CYP3A4
Metabolite: Carbamazepine 10,11-epoxide
###### Parameters

Name                             | Value                       | Value Origin                                                                                                                                        
-------------------------------- | --------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------
In vitro Vmax/recombinant enzyme | 1 pmol/min/pmol rec. enzyme |                                                                                                                                                     
Km                               | 248 µmol/l                  | Publication-In Vitro-Huang2004                                                                                                                      
kcat                             | 0.75 1/min                  | Parameter Identification-Parameter Identification-Value updated from '2020-10-30_refit_no2C8-induction_CYP3A4-metabolism_EPHX1_' on 2020-11-04 10:58
##### Induction: CYP3A4-mean of literature

Molecule: CYP3A4
###### Parameters

Name | Value     | Value Origin                                                                                                                                        
---- | --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------
EC50 | 20 µmol/l | Publication-In Vitro-mean of literature values                                                                                                      
Emax | 6         | Parameter Identification-Parameter Identification-Value updated from '2020-10-30_refit_no2C8-induction_CYP3A4-metabolism_EPHX1_' on 2020-11-04 10:58
##### Systemic Process: Glomerular Filtration-GFR (passive reabsorption)

Species: Human
###### Parameters

Name         |       Value | Value Origin                                                                                                                                        
------------ | -----------:| ----------------------------------------------------------------------------------------------------------------------------------------------------
GFR fraction | 0.027158714 | Parameter Identification-Parameter Identification-Value updated from '2020-10-30_refit_no2C8-induction_CYP3A4-metabolism_EPHX1_' on 2020-11-04 10:58
##### Metabolizing Enzyme: CYP2C8-Cazali 2003

Molecule: CYP2C8
###### Parameters

Name                             | Value                                  | Value Origin                   
-------------------------------- | -------------------------------------- | -------------------------------
In vitro Vmax/recombinant enzyme | 0.6733452272 pmol/min/pmol rec. enzyme | Publication-In Vitro-Cazali2003
Km                               | 757 µmol/l                             | Publication-In Vitro-Cazali2003
##### Metabolizing Enzyme: UGT2B7-Staines 2004 - mean

Molecule: UGT2B7
###### Parameters

Name                                        | Value                         | Value Origin                            
------------------------------------------- | ----------------------------- | ----------------------------------------
In vitro Vmax for liver microsomes          | 0.79 pmol/min/mg mic. protein | Publication-In Vitro-Staines 2004       
Content of CYP proteins in liver microsomes | 82.9 pmol/mg mic. protein     | Publication-In Vitro-Achour et al - 2014
Km                                          | 214 µmol/l                    | Publication-In Vitro-Staines2004        
##### Metabolizing Enzyme: CYP2B6-Pearce2002

Molecule: CYP2B6
###### Parameters

Name                             | Value                           | Value Origin                    
-------------------------------- | ------------------------------- | --------------------------------
In vitro Vmax/recombinant enzyme | 0.429 pmol/min/pmol rec. enzyme | Publication-In Vitro-Pearce2002 
Km                               | 420 µmol/l                      | Publication-In Vitro-Pearce 2002
##### Induction: CYP2B6-Test

Molecule: CYP2B6
###### Parameters

Name | Value     | Value Origin                                                                                                                                        
---- | --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------
EC50 | 20 µmol/l | Other-Assumption-mean of literature values of CYP3A4                                                                                                
Emax | 17        | Parameter Identification-Parameter Identification-Value updated from '2020-10-30_refit_no2C8-induction_CYP3A4-metabolism_EPHX1_' on 2020-11-04 10:58
##### Metabolizing Enzyme: CYP3A4-Pearce et al - 2002 -  3-hydroxy

Molecule: CYP3A4
###### Parameters

Name                             | Value                           | Value Origin                                                                                                                                        
-------------------------------- | ------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------
In vitro Vmax/recombinant enzyme | 0.164 pmol/min/pmol rec. enzyme | Publication-In Vitro-Pearce2002                                                                                                                     
Km                               | 282 µmol/l                      | Publication-In Vitro-Pearce 2002                                                                                                                    
kcat                             | 0.2 1/min                       | Parameter Identification-Parameter Identification-Value updated from '2020-10-30_refit_no2C8-induction_CYP3A4-metabolism_EPHX1_' on 2020-11-04 10:58
##### Induction: EPHX1-Eichelbaum

Molecule: EPHX1
###### Parameters

Name | Value     | Value Origin                                                                                                                                        
---- | --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------
EC50 | 20 µmol/l | Other-Assumption-mean of literature values for CYP3A4 induction                                                                                     
Emax | 3.25      | Parameter Identification-Parameter Identification-Value updated from '2020-10-30_refit_no2C8-induction_CYP3A4-metabolism_EPHX1_' on 2020-11-04 10:58
##### Systemic Process: Total Hepatic Clearance-Pearce - hydroxy processes

Species: Human
###### Parameters

Name                          | Value                  | Value Origin                                                                                                                                        
----------------------------- | ---------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------
Fraction unbound (experiment) | 0.25                   |                                                                                                                                                     
Lipophilicity (experiment)    | 2.0000632456 Log Units |                                                                                                                                                     
Plasma clearance              | 0 ml/min/kg            |                                                                                                                                                     
Specific clearance            | 0.015 1/min            | Parameter Identification-Parameter Identification-Value updated from '2020-10-30_refit_no2C8-induction_CYP3A4-metabolism_EPHX1_' on 2020-11-04 10:58

### Formulation: CBZ-E_tablet

Type: Weibull
#### Parameters

Name                             | Value              | Value Origin                                                                                                                                                      
-------------------------------- | ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------
Dissolution time (50% dissolved) | 200.0000054666 min | Parameter Identification-Parameter Identification-Value updated from '2020-09-18_refit_no2C8-induction_CYP3A4-metabolism_EPHX1_onlyTegretolIR' on 2020-09-21 11:16
Lag time                         | 0 min              |                                                                                                                                                                   
Dissolution shape                | 0.7537098141       | Parameter Identification-Parameter Identification-Value updated from '2020-09-18_refit_no2C8-induction_CYP3A4-metabolism_EPHX1_onlyTegretolIR' on 2020-09-21 11:16
Use as suspension                | No                 |                                                                                                                                                                   

### Formulation: CBZ_capsuleXR_fasted (Carbatrol)

Type: Weibull
#### Parameters

Name                             | Value              | Value Origin                                                                                                                                        
-------------------------------- | ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------
Dissolution time (50% dissolved) | 439.4574099817 min | Parameter Identification-Parameter Identification-Value updated from '2020-09-15_refit_no2C8-induction_CYP3A4-metabolism_EPHX1_' on 2020-10-28 17:25
Lag time                         | 0 min              |                                                                                                                                                     
Dissolution shape                | 0.7939239247       | Parameter Identification-Parameter Identification-Value updated from '2020-09-15_refit_no2C8-induction_CYP3A4-metabolism_EPHX1_' on 2020-10-28 17:25
Use as suspension                | Yes                |                                                                                                                                                     

### Formulation: CBZ_capsuleXR_fed (Carbatrol)

Type: Weibull
#### Parameters

Name                             | Value              | Value Origin                                                                                                                                        
-------------------------------- | ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------
Dissolution time (50% dissolved) | 361.3585414973 min | Parameter Identification-Parameter Identification-Value updated from '2020-09-15_refit_no2C8-induction_CYP3A4-metabolism_EPHX1_' on 2020-10-28 17:25
Lag time                         | 0 min              |                                                                                                                                                     
Dissolution shape                | 2.1274794597       | Parameter Identification-Parameter Identification-Value updated from '2020-09-15_refit_no2C8-induction_CYP3A4-metabolism_EPHX1_' on 2020-10-28 17:25
Use as suspension                | Yes                |                                                                                                                                                     

### Formulation: CBZ_tabletIR_fasted (Tegretol)

Type: Weibull
#### Parameters

Name                             | Value   | Value Origin                                                                                                                                        
-------------------------------- | ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------
Dissolution time (50% dissolved) | 200 min | Parameter Identification-Parameter Identification-Value updated from '2020-10-30_refit_no2C8-induction_CYP3A4-metabolism_EPHX1_' on 2020-11-04 10:58
Lag time                         | 0 min   |                                                                                                                                                     
Dissolution shape                | 0.74    | Parameter Identification-Parameter Identification-Value updated from '2020-10-30_refit_no2C8-induction_CYP3A4-metabolism_EPHX1_' on 2020-11-04 10:58
Use as suspension                | Yes     |                                                                                                                                                     

### Formulation: CBZ_tabletIR_fed (Tegretol)

Type: Weibull
#### Parameters

Name                             | Value   | Value Origin                                                                                                                                        
-------------------------------- | ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------
Dissolution time (50% dissolved) | 100 min | Parameter Identification-Parameter Identification-Value updated from '2020-10-30_refit_no2C8-induction_CYP3A4-metabolism_EPHX1_' on 2020-11-04 10:58
Lag time                         | 0 min   |                                                                                                                                                     
Dissolution shape                | 1.2     | Parameter Identification-Parameter Identification-Value updated from '2020-10-30_refit_no2C8-induction_CYP3A4-metabolism_EPHX1_' on 2020-11-04 10:58
Use as suspension                | Yes     |                                                                                                                                                     

### Formulation: CBZ_tabletXR_fasted (TegretolXR)

Type: Weibull
#### Parameters

Name                             | Value              | Value Origin                                                                                                                                        
-------------------------------- | ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------
Dissolution time (50% dissolved) | 767.1608678294 min | Parameter Identification-Parameter Identification-Value updated from '2020-10-30_refit_no2C8-induction_CYP3A4-metabolism_EPHX1_' on 2020-11-04 10:58
Lag time                         | 0 min              |                                                                                                                                                     
Dissolution shape                | 0.7579087507       | Parameter Identification-Parameter Identification-Value updated from '2020-10-30_refit_no2C8-induction_CYP3A4-metabolism_EPHX1_' on 2020-11-04 10:58
Use as suspension                | Yes                |                                                                                                                                                     

### Formulation: CBZ_tabletXR_fed (TegretolXR)

Type: Weibull
#### Parameters

Name                             | Value              | Value Origin                                                                                                         
-------------------------------- | ------------------ | ---------------------------------------------------------------------------------------------------------------------
Dissolution time (50% dissolved) | 436.3502971601 min | Parameter Identification-Parameter Identification-Value updated from 'Parameter Identification 6' on 2020-11-06 10:47
Lag time                         | 0 min              |                                                                                                                      
Dissolution shape                | 1.1593235448       | Parameter Identification-Parameter Identification-Value updated from 'Parameter Identification 6' on 2020-11-06 10:47
Use as suspension                | Yes                |                                                                                                                      

### Formulation: Solution

Type: Dissolved

## 3.2 Diagnostics Plots
Below you find the goodness-of-fit visual diagnostic plots for the PBPK model performance of all data used presented in [Section 2.2.2](#222-Clinical-Data).

The first plot shows simulated versus observed plasma concentration, the second weighted residuals versus time. 


![001_plotGOFMergedPredictedVsObserved.png](images/003_3_Results_and_Discussion/002_3_2_Diagnostics_Plots/001_plotGOFMergedPredictedVsObserved.png)

![002_plotGOFMergedResidualsOverTime.png](images/003_3_Results_and_Discussion/002_3_2_Diagnostics_Plots/002_plotGOFMergedResidualsOverTime.png)

GMFE = 1.498759 

## 3.3 Concentration-Time Profiles
Simulated versus observed concentration-time profiles of all data listed in [Section 2.2.2](#222-Clinical-Data) are presented below.


![001_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/001_plotTimeProfile.png)

![002_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/002_plotTimeProfile.png)

![003_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/003_plotTimeProfile.png)

![004_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/004_plotTimeProfile.png)

![005_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/005_plotTimeProfile.png)

![006_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/006_plotTimeProfile.png)

![007_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/007_plotTimeProfile.png)

![008_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/008_plotTimeProfile.png)

![009_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/009_plotTimeProfile.png)

![010_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/010_plotTimeProfile.png)

![011_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/011_plotTimeProfile.png)

![012_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/012_plotTimeProfile.png)

![013_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/013_plotTimeProfile.png)

![014_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/014_plotTimeProfile.png)

![015_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/015_plotTimeProfile.png)

![016_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/016_plotTimeProfile.png)

![017_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/017_plotTimeProfile.png)

![018_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/018_plotTimeProfile.png)

![019_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/019_plotTimeProfile.png)

![020_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/020_plotTimeProfile.png)

![021_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/021_plotTimeProfile.png)

![022_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/022_plotTimeProfile.png)

![023_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/023_plotTimeProfile.png)

![024_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/024_plotTimeProfile.png)

![025_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/025_plotTimeProfile.png)

![026_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/026_plotTimeProfile.png)

![027_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/027_plotTimeProfile.png)

![028_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/028_plotTimeProfile.png)

![029_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/029_plotTimeProfile.png)

![030_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/030_plotTimeProfile.png)

![031_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/031_plotTimeProfile.png)

![032_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/032_plotTimeProfile.png)

![033_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/033_plotTimeProfile.png)

![034_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/034_plotTimeProfile.png)

![035_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/035_plotTimeProfile.png)

![036_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/036_plotTimeProfile.png)

![037_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/037_plotTimeProfile.png)

![038_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/038_plotTimeProfile.png)

![039_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/039_plotTimeProfile.png)

![040_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/040_plotTimeProfile.png)

![041_plotTimeProfile.png](images/003_3_Results_and_Discussion/003_3_3_Concentration-Time_Profiles/041_plotTimeProfile.png)

# 4 Conclusion
The herein presented PBPK model adequately describes the pharmacokinetics of carbamazepine after single and multiple oral administration of various doses to healthy adults. 

In conclusion, the presented carbamazepine PBPK model is well-suited to be applied in drug-drug-interaction scenarios.

# 5 References
**Achour 2014** Achour, B., Russell, M. R., Barber, J., & Rostami-Hodjegan, A. (2014). Simultaneous quantification of the abundance of several cytochrome P450 and uridine 5′-diphospho-glucuronosyltransferase enzymes in human liver microsomes using multiplexed targeted proteomics. *Drug metabolism and disposition*, *42*(4), 500-510.

**Annaert 2010** Annaert, P., Brouwers, J., Bijnens, A., Lammert, F., Tack, J., & Augustijns, P. (2010). Ex vivo permeability experiments in excised rat intestinal tissue and in vitro solubility measurements in aspirated human intestinal fluids support age-dependent oral drug absorption. *European journal of pharmaceutical sciences*, *39*(1-3), 15-22.

**Austin 2002** Austin, R. P., Barton, P., Cockroft, S. L., Wenlock, M. C., & Riley, R. J. (2002). The influence of nonspecific microsomal binding on apparent intrinsic clearance, and its prediction from physicochemical properties. *Drug Metabolism and Disposition*, *30*(12), 1497-1503.

**Barzaghi 1987** Barzaghi, N., Gatti, G., Crema, F., Monteleone, M., Amione, C., Leone, L., & Perucca, E. (1987). Inhibition by erythromycin of the conversion of carbamazepine to its active 10, 11‐epoxide metabolite. *British journal of clinical pharmacology*, *24*(6), 836-838.

**Bedada 2015** Bedada, S. K., & Nearati, P. (2015). Effect of resveratrol on the pharmacokinetics of carbamazepine in healthy human volunteers. *Phytotherapy Research*, *29*(5), 701-706.

**Bedada 2016** Bedada, S. K., Appani, R., & Boga, P. K. (2017). Effect of piperine on the metabolism and pharmacokinetics of carbamazepine in healthy volunteers. *Drug research*, *67*(01), 46-51.

**Bernus 1994** Bernus, I., Dickinson, R. G., Hooper, W. D., & Eadie, M. J. (1994). Early stage autoinduction of carbamazepine metabolism in humans. *European journal of clinical pharmacology*, *47*(4), 355-360.

**Bianchetti 1987** Bianchetti, G., Padovani, P., Thenot, J. P., Thiercelin, J. F., & Morselli, P. L. (1987). Pharmacokinetic interactions of progabide with other antiepileptic drugs. *Epilepsia*, *28*(1), 68-73.

**Burstein 2000** Burstein, A. H., Horton, R. L., Dunn, T., Alfaro, R. M., Piscitelli, S. C., & Theodore, W. (2000). Lack of effect of St John's Wort on carbamazepine pharmacokinetics in healthy volunteers. *Clinical Pharmacology & Therapeutics*, *68*(6), 605-612.

**Caraco 1995** Caraco, Y., Zylber-Katz, E., Berry, E. M., & Levy, M. (1995). Carbamazepine phakmacokinetics in obese and lean subjects. *Annals of Pharmacotherapy*, *29*(9), 843-847.

**Cawello 2010** Cawello, W., Nickel, B., & Eggert‐Formella, A. (2010). No pharmacokinetic interaction between lacosamide and carbamazepine in healthy volunteers. *The Journal of Clinical Pharmacology*, *50*(4), 459-471.

**Cazali 2003** Cazali, N., Tran, A., Treluyer, J. M., Rey, E., d’Athis, P., Vincent, J., & Pons, G. (2003). Inhibitory effect of stiripentol on carbamazepine and saquinavir metabolism in human. *British journal of clinical pharmacology*, *56*(5), 526-536.

**Clarysse 2011** Clarysse, S., Brouwers, J., Tack, J., Annaert, P., & Augustijns, P. (2011). Intestinal drug solubility estimation based on simulated intestinal fluids: comparison with solubility in human intestinal fluids. *European journal of pharmaceutical sciences*, *43*(4), 260-269.

**Cotter 1977** Cotter, L. M., Eadie, M. J., Hooper, W. D., Lander, C. M., Smith, G. A., & Tyrer, J. H. (1977). The pharmacokinetics of carbamazepine. *European journal of clinical pharmacology*, *12*(6), 451-456.

**Dalton 1985a** Dalton, M. J., Powell, J. R., & Messenheimer Jr, J. A. (1985). The Influence of Cimetidine on Single‐Dose Carbamazepine Pharmacokinetics. *Epilepsia*, *26*(2), 127-130.

**Dalton 1985b** Dalton, M. J., Powell, J. R., Messenheimer Jr, J. A., Nazario, M., & Mallet, L. (1985). Ranitidine Does Not Alter Single-Dose Carbamazepin Pharmacokinetics in Healthy Adults. *Drug intelligence & clinical pharmacy*, *19*(12), 941-944.

**Di Salle 1974** Di Salle, E., Pacifici, G. M., & Morselli, P. L. (1974). Studies on plasma protein binding of carbamazepine. *Pharmacological research communications*, *6*(2), 193-202.

**Drugbank DB00564**. URL: https://www.drugbank.ca/drugs/DB00564, accessed on 12-14-2020.

**Drugbank DBMET00291**. URL: https://www.drugbank.ca/metabolites/DBMET00291, accessed on 12-16-2020.

**Eichelbaum 1985** Eichelbaum, M., Tomson, T., Tybring, G., & Bertilsson, L. (1985). Carbamazepine metabolism in man. *Clinical pharmacokinetics*, *10*(1), 80-90.

**Elqidra 2004** Elqidra, R., Ünlü, N., Capan, Y., Sahin, G., Dalkara, T., & Hincal, A. A. (2004). Effect of polymorphism on in vitro-in vivo properties of carbamazepine conventional tablets. *Journal of Drug Delivery Science and Technology*, *14*(2), 147-153.

**European Patent Application EP 1044681 A2** European Patent Application 2000, EP 1044681 A2, Application no. 00650026.8. URL: https://patentimages.storage.googleapis.com/0c/45/b7/d2be4fa9d24371/EP1044681A2.pdf, accessed on 12-01-2022.

**Faucette 2007** Faucette, S. R., Zhang, T. C., Moore, R., Sueyoshi, T., Omiecinski, C. J., LeCluyse, E. L., ... & Wang, H. (2007). Relative activation of human pregnane X receptor versus constitutive androstane receptor defines distinct classes of CYP2B6 and CYP3A4 inducers. *Journal of Pharmacology and Experimental Therapeutics*, *320*(1), 72-80.

**Fuhr 2021** Fuhr, L. M., Marok, F. Z., Hanke, N., Selzer, D., & Lehr, T. (2021). Pharmacokinetics of the CYP3A4 and CYP2B6 Inducer Carbamazepine and Its Drug–Drug Interaction Potential: A Physiologically Based Pharmacokinetic Modeling Approach. *Pharmaceutics*, *13*(2), 270.

**Gérardin 1976** Gérardin, A. P., Abadie, F. V., Campestrini, J. A., & Theobald, W. (1976). Pharmacokinetics of carbamazepine in normal humans after single and repeated oral doses. *Journal of pharmacokinetics and biopharmaceutics*, *4*(6), 521-535.

**Gérardin 1990** Gérardin, A., Dubois, J. P., Moppert, J., & Geller, L. (1990). Absolute bioavailability of carbamazepine after oral administration of a 2% syrup. *Epilepsia*, *31*(3), 334-338.

**Hooper 1975** Hooper, W. D., Dubetz, D. K., Bochner, F., Cotter, L. M., Smith, G. A., Eadie, M. J., & Tyrer, J. H. (1975). Plasma protein binding of carbamazepine. *Clinical Pharmacology & Therapeutics*, *17*(4), 433-440.

**Huang 2004** Huang, W., Lin, Y. S., McConn, D. J., Calamia, J. C., Totah, R. A., Isoherranen, N., ... & Thummel, K. E. (2004). Evidence of significant contribution from CYP3A5 to hepatic drug metabolism. *Drug metabolism and disposition*, *32*(12), 1434-1445.

**Ji 2008** Ji, P., Damle, B., Xie, J., Unger, S. E., Grasela, D. M., & Kaul, S. (2008). Pharmacokinetic interaction between efavirenz and carbamazepine after multiple‐dose administration in healthy subjects. *The Journal of Clinical Pharmacology*, *48*(8), 948-956.

**Kayali 1994** Kayali, A., Tuglular, I., & Ertas, M. (1994). Pharmacokinetics of carbamazepine Part I: a new bioequivalency parameter based on a relative bioavailability trial. *European journal of drug metabolism and pharmacokinetics*, *19*(4), 319-325.

**Kerr 1994** Kerr, B. M., Thummel, K. E., Wurden, C. J., Klein, S. M., Kroetz, D. L., Gonzalez, F. J., & Levy, R. (1994). Human liver carbamazepine metabolism: role of CYP3A4 and CYP2C8 in 10, 11-epoxide formation. *Biochemical pharmacology*, *47*(11), 1969-1979.

**Kim 2005** Kim, K. A., Oh, S. O., Park, P. W., & Park, J. Y. (2005). Effect of probenecid on the pharmacokinetics of carbamazepine in healthy subjects. *European journal of clinical pharmacology*, *61*(4), 275-280.

**Kitteringham 1996** Kitteringham, N. R., Davis, C., Howard, N., Pirmohamed, M., & Park, B. K. (1996). Interindividual and interspecies variation in hepatic microsomal epoxide hydrolase activity: studies with cis-stilbene oxide, carbamazepine 10, 11-epoxide and naphthalene. *Journal of pharmacology and experimental therapeutics*, *278*(3), 1018-1027.

**Kovacević 2009** Kovacević, I., Parojcic, J., Homsek, I., Tubic-Grozdanis, M., & Langguth, P. (2009). Justification of biowaiver for carbamazepine, a low soluble high permeable compound, in solid dosage forms based on IVIVC and gastrointestinal simulation. *Molecular pharmaceutics*, *6*(1), 40-47.

**Kuepfer 2016** Kuepfer, L., Niederalt, C., Wendl, T., Schlender, J. F., Willmann, S., Lippert, J., ... & Teutonico, D. (2016). Applied concepts in PBPK modeling: how to build a PBPK/PD model. *CPT: pharmacometrics & systems pharmacology*, *5*(10), 516-531.

**Lennernäs 2007** Lennernäs, H. (2007). Intestinal permeability and its relevance for absorption and elimination. *Xenobiotica*, *37*(10-11), 1015-1051.

**Levy 1975** Levy, R. H., Pitlick, W. H., Troupin, A. S., Green, J. R., & Neal, J. M. (1975). Pharmacokinetics of carbamazepine in normal man. *Clinical Pharmacology & Therapeutics*, *17*(6), 657-668.

**McLean 2001** McLean, A., Browne, S., Zhang, Y., Slaughter, E., Halstenson, C., & Couch, R. (2001). The influence of food on the bioavailability of a twice‐daily controlled release carbamazepine formulation. *The Journal of Clinical Pharmacology*, *41*(2), 183-186.

**Meyer 1992** Meyer, M. C., Straughn, A. B., Jarvi, E. J., Wood, G. C., Pelsor, F. R., & Shah, V. P. (1992). The bioinequivalence of carbamazepine tablets with a history of clinical failures. *Pharmaceutical Research*, *9*(12), 1612-1616.

**Meyer 1998** Meyer, M. C., Straughn, A. B., Mhatre, R. M., Shah, V. P., Williams, R. L., & Lesko, L. J. (1998). The relative bioavailability and in vivo-in vitro correlations for four marketed carbamazepine tablets. *Pharmaceutical research*, *15*(11), 1787-1791.

**Meyer 2012** Meyer, M., Schneckener, S., Ludewig, B., Kuepfer, L., & Lippert, J. (2012). Using expression data for quantification of active processes in physiologically based pharmacokinetic modeling. *Drug Metabolism and Disposition*, *40*(5), 892-901.

**Miles 1989** Miles, M. V., & Tennison, M. B. (1989). Erythromycin effects on multiple-dose carbamazepine kinetics. *Therapeutic drug monitoring*, *11*(1), 47-52.

**Møller 2001** Møller, S. E., Larsen, F., Khan, A. Z., & Rolan, P. E. (2001). Lack of effect of citalopram on the steady-state pharmacokinetics of carbamazepine in healthy male subjects. *Journal of clinical psychopharmacology*, *21*(5), 493-499.

**Morselli 1975** Morselli, P. L., Gerna, M., De Maio, D., Zanda, G., Viani, F., & Garattini, S. (1975). Pharmacokinetic studies on carbamazepine in volunteers and in epileptic patients. In: *Clinical pharmacology of anti-epileptic drugs* (pp. 166-180). Springer, Berlin, Heidelberg.

**Nishimura 2003** Nishimura, M., Yaguti, H., Yoshitsugu, H., Naito, S., & Satoh, T. (2003). Tissue Distribution of mRNA Expression of Human Cytochrome P450 Isoforms Assessed by High-Sensitivity Real-Time Reverse Transcription PCR. *Yakugaku zasshi*, *123*(5), 369-375.

**Pearce 2002** Pearce, R. E., Vakkalagadda, G. R., & Leeder, J. S. (2002). Pathways of carbamazepine bioactivation in vitro I. Characterization of human cytochromes P450 responsible for the formation of 2- and 3-hydroxylated metabolites. *Drug metabolism and disposition*, *30*(11), 1170-1179.

**Pelkonen 2001** Pelkonen, O., Myllynen, P., Taavitsainen, P., Boobis, A. R., Watts, P., Lake, B. G., ... & Lewis, D. F. V. (2001). Carbamazepine: a 'blind' assessment of CYP-associated metabolism and interactions in human liver-derived in vitro systems. *Xenobiotica*, *31*(6), 321-343.

**Pisani 1988** Pisani, F., Fazio, A., Oteri, G., Spina, E., Perucca, E., & Bertilsson, L. (1988). Effect of valpromide on the pharmacokinetics of carbamazepine‐10, 11‐epoxide. *British journal of clinical pharmacology*, *25*(5), 611-613.

**Pisani 1990** Pisani, F., Caputo, M., Fazio, A., Oteri, G., Russo, M., Spina, E., ... & Bertilsson, L. (1990). Interaction of carbamazepine‐10, 11‐epoxide, an active metabolite of carbamazepine, with valproate: a pharmacokinetic study. *Epilepsia*, *31*(3), 339-342.

**Pisani 1992** Pisani, F., Fazio, A., Artesi, C., Oteri, G., Spina, E., Tomson, T., & Perucca, E. (1992). Impairment of carbamazepine‐10, 11‐epoxide elimination by valnoctamide, a valpromide isomer, in healthy subjects. *British journal of clinical pharmacology*, *34*(1), 85-87.

**PK-Sim Ontogeny Database Version 7.3** URL: https://github.com/Open-Systems-Pharmacology/OSPSuite.Documentation/blob/38cf71b384cfc25cfa0ce4d2f3addfd32757e13b/PK-Sim%20Ontogeny%20Database%20Version%207.3.pdf, accessed on 12-01-2022.

**Pynnönen 1977** Pynnönen, S. (1977). The pharmacokinetics of carbamazepine in plasma and saliva of man. *Acta pharmacologica et toxicologica*, *41*(5), 465-471.

**Rawlins 1975** Rawlins, M. D., Collste, P., Bertilsson, L., & Palmer, L. (1975). Distribution and elimination kinetics of carbamazepine in man. *European journal of clinical pharmacology*, *8*(2), 91-96.

**Saint-Salvi 1987** Saint-Salvi, B., Tremblay, D., Surjus, A., & Lefebvre, M. A. (1987). A Study of the Interaction of Roxithromycin with Theophylline and Carbarmazepine. *Journal of Antimicrobial Chemotherapy*, *20*(suppl_B), 121-129.

**Söderlind 2010** Söderlind, E., Karlsson, E., Carlsson, A., Kong, R., Lenz, A., Lindborg, S., & Sheng, J. J. (2010). Simulating fasted human intestinal fluids: understanding the roles of lecithin and bile acids. *Molecular pharmaceutics*, *7*(5), 1498-1507.

**Staines 2004** Staines, A. G., Coughtrie, M. W., & Burchell, B. (2004). N-glucuronidation of carbamazepine in human tissues is mediated by UGT2B7. *Journal of Pharmacology and Experimental Therapeutics*, *311*(3), 1131-1137.

**Stevens 1998** Stevens, R. E., Limsakun, T., Evans, G., & Mason, J. D. H. (1998). Controlled, multidose, pharmacokinetic evaluation of two extended‐release carbamazepine formulations (Carbatrol and Tegretol‐XR). *Journal of pharmaceutical sciences*, *87*(12), 1531-1534.

**Strandjord 1975** Strandjord, R. E., & Johannessen, S. I. (1975). A preliminary study of serum carbamazepine levels in healthy subjects and in patients with epilepsy. In: *Clinical pharmacology of anti-epileptic drugs* (pp. 181-188). Springer, Berlin, Heidelberg.

**Sumi 1987** Sumi, M., Watari, N., Umezawa, O., & Kaneniwa, N. (1987). Pharmacokinetic study of carbamazepine and its epoxide metabolite in humans. *Journal of pharmacobio-dynamics*, *10*(11), 652-661.

**Tedeschi 1981** Tedeschi, G., Cenraud, B., Guyot, M., Gomeni, R., Morselli, P. L., Levy, R. H., & Loiseau, P. (1981). Influence of food on carbamazepine absorption. In: *Advances in epileptology: XIIth epilepsy international symposium. Raven, New York* (pp. 563-567).

**Terhaag 1978** Terhaag, B., Richter, K., & Diettrich, H. (1978). Concentration behavior of carbamazepine in bile and plasma of man. *International journal of clinical pharmacology and biopharmacy*, *16*(12), 607-609.

**Tomson 1983** Tomson, T., Tybring, G., & Bertilsson, L. (1983). Single‐dose kinetics and metabolism of carbamazepine‐10, 11‐epoxide. *Clinical Pharmacology & Therapeutics*, *33*(1), 58-65.

**US Patent Application - US 2009/0169619 A1**. United States Patent Application 2009, Publication no.: US 2009/0169619 A1. https://patentimages.storage.googleapis.com/66/d4/30/f3588f44ab2b6f/US20090169619A1.pdf, accessed on 12-01-2022.

**US Patent Application - US 2014/0302138 A1**. United States Patent Application 2014, Publication no.: US 2014/0302138 A1. https://patentimages.storage.googleapis.com/57/d9/18/0d8cbfa046681d/US20140302138A1.pdf, accessed on 12-01-2022.

**Vinçon 1987** Vinçon, G., Albin, H., Demotes-Mainard, F., Guyot, M., Bistue, C., & Loiseau, P. (1987). Effects of josamycin on carbamazepine kinetics. *European journal of clinical pharmacology*, *32*(3), 321-323.

**Wada 1978** Wada, J. A., Troupin, A. S., Friel, P., Remick, R., Leal, K., & Pearmain, J. (1978). Pharmacokinetic comparison of tablet and suspension dosage forms of carbamazepine. *Epilepsia*, *19*(3), 251-255.

**Willmann 2007** Willmann, S., Höhn, K., Edginton, A., Sevestre, M., Solodenko, J., Weiss, W., ... & Schmitt, W. (2007). Development of a physiology-based whole-body population model for assessing the influence of individual variability on the pharmacokinetics of drugs. *Journal of pharmacokinetics and pharmacodynamics*, *34*(3), 401-431.

**Wong 1983** Wong, Y. Y., Ludden, T. M., & Bell, R. D. (1983). Effect of erythromycin on carbamazepine kinetics. *Clinical Pharmacology & Therapeutics*, *33*(4), 460-464.




