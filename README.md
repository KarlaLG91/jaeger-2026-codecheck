# CODECHECK certificate 2026-032

This repository contains the certificate and outputs for an independent
CODECHECK by Karla Lozano Gonzalez of:

> Bastian Jaeger, Stefan Leach, and Matthew Zipple, *Consciousness and Emotions
> in Non-Human Animals: Are Laypeople More or Less Skeptical than Experts?*
> <https://doi.org/10.71240/lcyc.238674>

The authors' analysis code, data, and supplemental materials are available
from the [OSF record](https://osf.io/9v3rh/); they are not included in this
repository. See the [certificate](codecheck/codecheck.pdf) for the full
findings, caveats, and citation.

## What was checked

Tables S1-S4 of the supplemental materials were reproduced from the authors'
R analysis. Small numerical differences of up to 0.001 were observed; their
cause was not established. The comparison did not change the statistical
significance of the reported effects. The check did not cover the complete
analysis or the bootstrapped confidence intervals. R reported a convergence
warning for one model; see the certificate for details.

| Table | Model | Saved output |
| --- | --- | --- |
| S1: consciousness attribution | `model3a` | [table_S1_model3a.txt](codecheck/outputs/table_S1_model3a.txt) |
| S2: emotion attribution | `model3b` | [table_S2_model3b.txt](codecheck/outputs/table_S2_model3b.txt) |
| S3: confidence in consciousness beliefs | `model4a` | [table_S3_model4a.txt](codecheck/outputs/table_S3_model4a.txt) |
| S4: confidence in emotion beliefs | `model4b` | [table_S4_model4b.txt](codecheck/outputs/table_S4_model4b.txt) |

## Repository contents

- [codecheck.yml](codecheck.yml): certificate metadata and output manifest.
- [codecheck/codecheck.pdf](codecheck/codecheck.pdf): rendered certificate.
- [codecheck/codecheck.qmd](codecheck/codecheck.qmd): certificate source.
- [codecheck-preamble.sty](codecheck-preamble.sty): LaTeX preamble used by the certificate.
- [codecheck/outputs/](codecheck/outputs/): model summary outputs from the check.

## Repeat the checked analysis

1. Download `analysis code.R`, `data experts.csv`, `data laypeople.csv`, and
   `supplemental materials.pdf` from the [OSF record](https://osf.io/9v3rh/).
   Put the script and CSV files in the same folder and set that folder as the
   R working directory. Internet access is needed to obtain the materials.
2. Install R and the packages loaded by the script: `cowplot`, `rio`, `brms`,
   `gridExtra`, `irr`, `viridis`, `ggeffects`, `psych`, `effsize`, `ICC`,
   `lme4`, `lmerTest`, and `tidyverse`. The script also loads `grid`, which is
   included with R. The original analysis package versions are not recorded
   here; the certificate's `sessionInfo()` describes the certificate-rendering
   environment, not necessarily the original analysis environment.
3. In an interactive R session, run `analysis code.R` from the beginning
   through `summary(model4b)`, skipping every line containing a bootstrapped
   `confint()` or `confint.merMod()` call. Do not source the entire script:
   later analyses and the skipped confidence intervals were outside this
   check. In the version inspected, `summary(model4b)` is on line 812; line
   numbers may differ in other versions. The script sets its own random seed.
4. Save the four summaries from the same R session, for example:

   ```r
   dir.create("codecheck-results", showWarnings = FALSE)
   capture.output(summary(model3a), file = "codecheck-results/table_S1_model3a.txt")
   capture.output(summary(model3b), file = "codecheck-results/table_S2_model3b.txt")
   capture.output(summary(model4a), file = "codecheck-results/table_S3_model4a.txt")
   capture.output(summary(model4b), file = "codecheck-results/table_S4_model4b.txt")
   ```

5. Compare the summaries with Tables S1-S4 in `supplemental materials.pdf`
   and with the saved outputs above. The checked portion took approximately
   20 seconds on the codechecker's laptop, excluding bootstrapped intervals;
   runtime will vary by machine.

## Render the certificate

Rendering the certificate is separate from rerunning the authors' analysis.
It requires Quarto, R, a LaTeX installation with XeLaTeX, and the R packages
`codecheck`, `knitr`, `rprojroot`, `yaml`, `xtable`, `tibble`, and `readr`.
The validation steps may require network access. From the repository root:

```sh
cd codecheck
quarto render codecheck.qmd --to pdf
```

The command regenerates `codecheck/codecheck.pdf`; it does not rerun the
authors' analysis or regenerate the model summary files.

## Licensing

No license file is currently included in this repository. Check the OSF
record and contact the relevant rights holders for permissions to reuse the
authors' materials; the absence of a license here is not a grant of reuse
rights.

See the [CODECHECK community workflow guide](https://codecheck.org.uk/guide/community-workflow-author)
for the recommended documentation and repository contents.
