# Two-Layer Intracellular Protein Surveillance

**Version:** v0.3 exploratory research note — 7 November 2026

**Status:** Computational hypothesis only; no experimental, biochemical, or clinical validation.

**Contributions:** Concept and research direction: Altuğ Kuran. Mathematical framing, critical review and drafting assistance: OpenAI GPT-6 (AI assistant, not a human co-author).

## Abstract
The proposal compares two hypothetical channels supplementing natural cellular quality control. A monitors mRNA/translation-associated early-warning signals; B independently samples downstream protein and cellular-context evidence. Four computational arms are compared: natural surveillance N, N+A, N+B, and N+A+B. Risk scores are synthetic and are not probabilities of cancer.

## Concept and architecture
The initial synthetic-ribosome pre-check concept was reformulated as an early-warning observer because protein danger cannot reliably be inferred from sequence alone. B provides a separate observation channel and can operate without A. False alarms, benign variation, sampling costs and missed hazards are essential outcomes, not afterthoughts.

## Observer A
Illustrative uncalibrated thresholds: 0.65 for a natural quality-control alert; 0.75 for a temporary translation-slowdown request; 0.90 for a strong alert requiring B corroboration. No actual synthetic ribosome or biological translation controller has been demonstrated.

## Observer B
Illustrative uncalibrated thresholds: 0.60 for increased surveillance; 0.75 for reversible-action verification; 0.95 for a joint candidate-decision review. The present computational approximation uses independent sampling opportunities, not explicit three-dimensional Brownian trajectories.

## Mathematical hypotheses
- Hidden hazard state: H in {0,1}; benign variation and normal physiological cell death are distinct.
- Synthetic observer scores: r_A and r_B, not calibrated probabilities.
- Transient A signal: dS/dt = Q_A(t) - k_d S, with k_d = ln(2)/t_half.
- Characteristic signal length: ell = sqrt(D/k_d). The provisional criterion ell >= 0.2 L uses the characteristic *linear* cell dimension L; it is not a 20% volume criterion or guaranteed delivery.
- Independent equal sampling opportunities: P(at least one sample) = 1 - (1-p)^N_B. Crowding and correlation can invalidate this expression.
- Joint candidate flag: C = 1[r_A >= 0.90] * 1[r_B >= 0.95] * 1[message detected], with additional coverage and sampling conditions. C is **not** an actual apoptosis command.
- Proposed hysteresis: S_on > S_off; a complete dynamic switching state machine remains unimplemented.

## Computational comparisons
Compare N, N+A, N+B and N+A+B on matched virtual-cell samples. Outcomes include sensitivity, false alarms, missed hazards, candidate-decision frequency, and resource burden. All results are synthetic, not measurements. Observer errors may be correlated, undermining apparent corroboration benefits.

## Limitations and falsifiability
There is no evidence that the proposed A/B organelles, selective messaging, universal protein-risk assessment, or safe translation/apoptosis control can be implemented. Protein function depends on folding, modifications, cell state, and environment. A B veto may reduce false positives while increasing missed hazards. Reject or revise the model if realistic calibrated parameters under matched resource budgets show no meaningful benefit over natural surveillance, or intervention costs outweigh benefits.

## Research roadmap
Implement spatial Brownian motion and reaction-diffusion, dynamic hysteresis, time-resolved B alarms, correlated observers, matched-resource budgets, uncertainty analysis, and independent expert review. Experimental calibration would be required before any biological claims.

## Selected background references
1. Brandman O, Hegde RS. Ribosome-associated protein quality control (2016). https://doi.org/10.1038/nsmb.3147
2. Karamyshev AL et al. Inefficient SRP interaction with a nascent chain triggers a mRNA quality control pathway (2014). https://doi.org/10.1016/j.cell.2014.02.053
3. Turing AM. The chemical basis of morphogenesis (1952). https://doi.org/10.1098/rstb.1952.0012
4. Elmore S. Apoptosis: A Review of Programmed Cell Death (2007). https://doi.org/10.1080/01926230701320337
5. Snijder B, Pelkmans L. Origins of regulated cell-to-cell variability (2011). https://doi.org/10.1038/nrm3044

These references are background, not validation of this proposed architecture. Verify bibliographic details before formal publication.
