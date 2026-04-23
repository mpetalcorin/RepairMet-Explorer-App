# Model Card: RepairMet Explorer

## Model name

RepairMet Explorer

## Model type

Mechanistically curated, rule-based, interpretable decision-support engine for oncology research.

## Version

Current concept release

## Summary

RepairMet Explorer is a transparent scoring framework that integrates DNA repair, replication stress, and metabolic-state features into ranked mechanistic vulnerability hypotheses. It is designed for research hypothesis prioritization rather than clinical prediction.

The system accepts a compact tumour-state feature vector, derives composite biological states, compares the sample to a curated vulnerability library, applies bounded evidence weighting, and returns ranked outputs with contributor traces and suggested next-step assays.

## Availability

Web application:

https://repairmet-explorer.vercel.app/

Source code:

https://github.com/mpetalcorin/repairmet-explorer

## Intended purpose

The model is intended to help researchers answer the question:

“Given this tumour-like biological profile, which survival dependency appears most plausible, and what should be tested next?”

## Intended users

- molecular biologists

- cancer biologists

- translational researchers

- computational biologists

- biomedical data scientists

- interdisciplinary oncology teams

## Out-of-scope use

The model is not intended for:

- clinical diagnosis

- direct treatment recommendation

- risk prediction for patients

- autonomous medical decision making

- replacement of pathology review, laboratory validation, or clinical judgment

## Inputs

The current release expects ten features scored on a 0 to 100 scale:

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

Optional evidence-weighting inputs:

- pathway

- assay

- omics

- expert

## Internal representation

### Step 1

Normalize each feature to the interval from 0 to 1.

### Step 2

Compress the normalized feature vector into five composite biological states:

- repairDefect

- replicationBurden

- glycolyticAcidLoad

- mitoPlasticity

- redoxFragility

### Step 3

Compare the sample profile against curated hypothesis signatures.

### Step 4

Compute a base mechanistic score and apply a bounded evidence multiplier.

### Step 5

Rank the resulting mechanistic hypotheses.

## Outputs

For each sample, the model returns:

- normalized_features

- composite_state

- ranked_hypotheses

Each ranked hypothesis includes:

- id

- title

- mechanism

- next_step

- score

- base_score

- evidence_multiplier

- explain

## Hypothesis library

The current model includes:

1. POLQ / PARP synthetic lethality axis

2. ATR / WEE1 / CHK1 checkpoint dependence

3. LDHA / lactate export vulnerability

4. GLS / glutamine anaplerosis dependence

5. SLC7A11 / GPX4 redox defense

6. OXPHOS overload and mitochondrial stress

## Scientific assumptions

The model assumes that tumours are:

- adaptive

- stress-laden

- dependency-driven

- mechanistically organized

- representable as interpretable functional states

It also assumes that vulnerabilities emerge from interactions among:

- DNA repair capacity

- replication-stress handling

- metabolic adaptation

- oxidative and redox balance

## Strengths

- transparent scoring logic

- human-readable input space

- contributor-level explanation

- evidence-weighting support

- cohort-compatible workflow

- easy export for reports and team review

- useful for translational hypothesis generation

## Limitations

- rule-based rather than outcome-trained

- not calibrated against clinical endpoints

- no uncertainty quantification in current version

- depends on upstream interpretation of feature values

- limited current hypothesis library

- not tumour-type specific

- cannot autonomously discover new interactions

## Risks and caveats

The model may produce misleading rankings if:

- input scores are poorly estimated

- features are inconsistent across cohorts

- assays are noisy or weakly mapped to the feature layer

- the biological context falls outside the current hypothesis library

- evidence weights are assigned unrealistically

## Evaluation status

The current version is a concept-stage mechanistic prioritization engine. It has been designed for biological coherence and interpretability rather than predictive benchmarking against patient outcomes.

Illustrative use cases show biologically plausible prioritization of:

- checkpoint dependence in replication-stressed samples

- backup repair in HR-deficient samples

- glycolytic acid handling in lactate-dominant samples

Formal large-scale validation remains future work.

## Reproducibility notes

The model is reproducible at the logic level because scoring is deterministic for a given set of feature values and evidence weights. Reproducibility in practical use also depends on how upstream biological measurements are converted into the ten-feature input space. For rigorous use, analysts should document feature derivation, preprocessing, evidence-weight rationale, software version, and export date.

## Ethical and safety considerations

Because the model can generate persuasive mechanistic rankings, users should avoid overinterpreting outputs as clinical truth. Results should be treated as structured hypotheses requiring experimental validation.

## Recommended use practice

Use the model as:

- a scientific triage tool

- a discussion aid

- a hypothesis-ranking layer

- a bridge between data review and experimental planning

Do not use the model as:

- a stand-alone clinical decision engine

- a substitute for biological expertise

- a substitute for wet-lab confirmation

## Future improvements

- tumour-type-specific scoring priors

- learned parameter refinement

- formal uncertainty estimation

- assay-to-feature standardization

- larger curated vulnerability library

- external benchmarking on public and internal translational datasets

- calibration against experimental or clinical outcomes

## Maintainer

**Petalcorin, M.I.R.** (2026). RepairMet Explorer: An explainable decision-support workflow linking DNA repair, 
replication stress, and metabolic vulnerability in oncology. https://github.com/mpetalcorin/RepairMet-Explorer-App

