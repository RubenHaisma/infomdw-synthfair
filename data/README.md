# Data sources

Downloaded 3 November 2026. Input bytes are unchanged from the sources; cleaning is performed in the notebook.

- Adult: https://archive.ics.uci.edu/static/public/2/adult.zip (`adult.data`, `adult.test`). UCI dataset DOI: https://doi.org/10.24432/C5XW20.
- German Credit: https://archive.ics.uci.edu/static/public/144/statlog+german+credit+data.zip (`german.data`). UCI dataset DOI: https://doi.org/10.24432/C5NC77.
- COMPAS: https://raw.githubusercontent.com/propublica/compas-analysis/c062fbb5fa84f6c99d82f432c46b405f3a0ca5ec/compas-scores-two-years.csv. Filtering follows https://github.com/propublica/compas-analysis/blob/c062fbb5fa84f6c99d82f432c46b405f3a0ca5ec/Compas%20Analysis.ipynb.

German Credit uses the paper's age boundary (40 years) and compares personal-status codes A91/A93/A94 to A92/A95, following the partition used by the benchmark implementation. The corrected codebook explains that the field mixes sex and marital status. The experiment therefore interprets these as code groups, not men and women. Both age and the personal-status field are excluded from predictors. [Corrected codebook](https://doi.org/10.24432/C5QG88).

SHA-256:

- `adult.data`: `5b00264637dbfec36bdeaab5676b0b309ff9eb788d63554ca0a249491c86603d`
- `adult.test`: `a2a9044bc167a35b2361efbabec64e89d69ce82d9790d2980119aac5fd7e9c05`
- `compas-scores-two-years.csv`: `c451db85908b2f7fef1d83203bedf6b71ecda0d5af468d82ae62178f91d0cc7d`
- `german.data`: `b21f3d81db8071257d5ff1deaeba1fd4303b62712e6fcc9715c7a86202cb5871`
