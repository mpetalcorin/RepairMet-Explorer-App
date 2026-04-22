# RepairMet-Explorer-App
RepairMet Explorer is an explainable scientific software platform for oncology decision support. It integrates DNA repair, replication stress, and metabolic vulnerability into a structured workflow that ranks mechanistic hypotheses and suggests practical next-step assays.
<img width="1237" height="539" alt="RepairMet" src="https://github.com/user-attachments/assets/ae9e5e43-093f-4d45-b276-0be37a6e4e14" />
# RepairMet Explorer

RepairMet Explorer is an explainable scientific software platform for oncology decision support. It integrates DNA repair, replication stress, and metabolic vulnerability into a structured workflow that ranks mechanistic hypotheses and suggests practical next-step assays.

## Overview

Cancer samples often show multiple overlapping biological features at the same time, including homologous recombination deficiency, unstable replication forks, checkpoint dependence, glycolytic rewiring, oxidative stress, and mitochondrial plasticity. These signals are frequently examined in separate spreadsheets, pathway outputs, and notes, making it difficult to decide which biological liability is most worth testing first.

RepairMet Explorer addresses that problem by converting a compact, human-readable feature set into:

- composite biological state variables
- ranked vulnerability hypotheses
- top contributing features
- evidence-adjusted prioritization
- cohort summaries
- exportable sample and cohort reports

The platform is designed as an explainable reasoning layer, not as a black-box prediction system.

## Software availability

Web application:
https://repairmet-explorer.vercel.app/

Source code:
https://github.com/mpetalcorin/repairmet-explorer

## Core idea

The app assumes that tumours are adaptive, stress-laden, dependency-driven systems whose vulnerabilities emerge from the interaction of DNA repair, replication stress, and metabolic state.

The workflow:

1. Accept interpretable tumour-state features.
2. Normalize values to a common scale.
3. Compress them into composite biological states.
4. Compare the sample against a curated vulnerability library.
5. Apply bounded evidence weighting.
6. Return ranked hypotheses and suggested next assays.

## Feature set

The platform currently uses ten input features scored on a 0 to 100 scale:

- hrd
- fork
- repStress
- atr
- glycolysis
- oxphos
- glutamine
- ros
- redox
- lactate

These correspond to:

- homologous recombination deficiency
- fork instability
- replication stress
- ATR-CHK1 signaling
- glycolysis reliance
- oxidative phosphorylation competence
- glutamine dependence
- reactive oxygen species pressure
- redox buffering
- lactate handling

## Current hypothesis library

The current release includes six mechanistic hypotheses:

- POLQ / PARP synthetic lethality axis
- ATR / WEE1 / CHK1 checkpoint dependence
- LDHA / lactate export vulnerability
- GLS / glutamine anaplerosis dependence
- SLC7A11 / GPX4 redox defense
- OXPHOS overload and mitochondrial stress

## Main outputs

For each sample, the platform returns:

- normalized feature vector
- composite state scores
- ranked hypotheses
- base mechanistic score
- evidence multiplier
- final priority score
- top contributors
- recommended next-step assay ideas

## Frontend features

The web application currently supports:

- interactive single-sample scoring
- evidence weighting sliders
- output reactive graph
- state map bar chart
- feature geometry radar chart
- explanation of analysis
- ranked hypotheses display
- cohort CSV upload
- cohort table export
- current output export
- sample HTML report export

## Technology stack

Frontend:
- React
- Vite
- Recharts
- Framer Motion

Backend:
- FastAPI
- Pydantic
- Uvicorn

## Local project structure

```text
RepairMetExplorer/
  backend/
    main.py
    models.py
    scoring.py
    requirements.txt
  frontend/
    src/
      App.jsx
      api.js
      main.jsx
      styles.css
    package.json
```
## Example CSV
sample_name,hrd,fork,repStress,atr,glycolysis,oxphos,glutamine,ros,redox,lactate
BRCA_like_1,92,76,82,74,84,28,58,68,62,80
Checkpoint_1,54,82,94,91,46,34,42,58,48,38
Metabolic_Plastic_1,38,44,52,48,64,70,88,54,66,52

## Data validation rules

The app expects:

* non-empty sample_name
* all required feature columns present
* numeric values for all features
* no missing feature entries within a row
* feature values intended for the 0 to 100 range

Invalid rows may produce upload failure or misleading rankings.

## Output data schema

For each scored sample, the platform returns:

* sample_name
* normalized_features
* composite_state
* ranked_hypotheses

### normalized_features

Dictionary of input features converted to 0 to 1 scale.

### composite_state

Contains:

* repairDefect
* replicationBurden
* glycolyticAcidLoad
* mitoPlasticity
* redoxFragility

### ranked_hypotheses

List of ranked vulnerability objects. Each object contains:

* id
* title
* mechanism
* next_step
* score
* base_score
* evidence_multiplier
* explain

### explain

Top contributing feature list for that hypothesis. Each contributor contains:

* label
* score

## Data provenance considerations

Because the platform accepts interpreted feature scores, provenance should be tracked outside the app whenever possible. For rigorous research use, users should record:

* the source assay or dataset
* preprocessing steps
* normalization method
* scoring rationale
* analyst or reviewer identity
* date and version of the exported result

## Data quality considerations

The app works best when the feature layer is:

* biologically interpretable
* consistently scaled
* quality controlled
* comparable across samples
* derived from documented evidence streams

The app may work poorly when:

* features are loosely estimated without rationale
* cohorts have major batch effects
* different samples use incompatible scoring schemes
* the biology is forced into the wrong feature space

## Data limitations

This project does not yet ship with:

* a single benchmark dataset
* a clinical outcomes dataset
* tumour-type-specific reference cohorts
* probabilistically calibrated training labels

The current version is designed around structured mechanistic interpretation, not supervised clinical prediction.

## Reproducibility and documentation

For a publication-quality or team-shared cohort, record at minimum:

* project name
* sample source
* tumour type or model type
* feature derivation method
* evidence-weight rationale
* software version
* export date
* downstream decisions or assay follow-up

For rigorous reuse, pair each exported result with the exact software release and the specific feature-to-assay mapping used to generate the inputs.

## Privacy and sensitivity

If real patient-linked samples are used upstream, users are responsible for ensuring that all exported files and uploaded cohort tables are handled according to local ethical, privacy, and data-governance requirements.

## Maintenance notes

As the hypothesis library expands, the expected feature space may grow. This datasheet should be versioned alongside the software so that users know which inputs and outputs correspond to which release.

## Version 1.0

Current concept release

## Citation
**Petalcorin, M.I.R. (2026). RepairMet Explorer: An explainable decision-support workflow linking DNA repair, 
replication stress, and metabolic vulnerability in oncology. https://github.com/mpetalcorin/RepairMet-Explorer-App
