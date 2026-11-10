# SynthFair on Adult, German Credit and COMPAS

This notebook tests Strategy 1 of Hattatoğlu et al.'s [SynthFair paper](https://doi.org/10.1007/978-3-031-85856-7_26). It compares two random forests on the same people in each test split. One forest also sees synthetic training records. The settings follow the [authors’ implementation](https://github.com/bendiste/Algorithmic-Fairness/tree/e3d343f18ef98f67ad99e616ec389f215c41d12a/Implementation), with the choices below.

## Run the notebook

Use Python 3.13 (tested with 3.13.1). Start in the directory containing `assignment_4.ipynb`. The complete ZIP includes the four data files. For the GitHub checkout, first download them using the commands below. On macOS or Linux:

```sh
python3.13 -m venv .venv
. .venv/bin/activate
python -m pip install -r requirements.txt
python -m ipykernel install --sys-prefix --name dw-synthfair
python -m nbconvert --to notebook --execute --inplace --ExecutePreprocessor.kernel_name=dw-synthfair --ExecutePreprocessor.timeout=1800 assignment_4.ipynb
```

## Data for a GitHub checkout

```sh
mkdir -p data
curl -fL 'https://archive.ics.uci.edu/static/public/2/adult.zip' -o data/adult.zip
unzip -o data/adult.zip adult.data adult.test -d data
curl -fL 'https://archive.ics.uci.edu/static/public/144/statlog+german+credit+data.zip' -o data/german.zip
unzip -o data/german.zip german.data -d data
curl -fL 'https://raw.githubusercontent.com/propublica/compas-analysis/c062fbb5fa84f6c99d82f432c46b405f3a0ca5ec/compas-scores-two-years.csv' -o data/compas-scores-two-years.csv
```

Sources, hashes and the German Credit group coding are in [data/README.md](data/README.md). Once the inputs and dependencies are present, the experiment runs offline.

## Experimental choices

The primary split uses seed 42; seeds 43 and 44 repeat the comparison. Each 70/30 split is stratified on demographic group and recorded outcome. Numeric scaling, one-hot encoding and the two-dimensional FAMD projection for fuzzy clustering are fitted on training rows. Adult, German Credit and COMPAS use 6, 3 and 5 clusters respectively. The notebook applies one-neighbour SMOTE within each cluster and occupied group–outcome combination. The two forests use 100 trees and at least five observations per leaf.

The authors’ third strategy selects eligible cluster models using a joint group–outcome code at prediction time. Strategy 1 uses one pooled forest and can predict from features alone. The comparison preserves the original outcome frequencies when splitting Adult. German Credit uses the age-40 threshold in Table 3 and the published status-code partition; this field cannot establish a gender gap.

## Outputs

The notebook creates `results/` and saves:

| File | What it contains |
| --- | --- |
| `metrics.csv` | Original and held-out group sizes and positive rates, DP difference, DIR, consistency and predictive performance. |
| `cluster_counts.csv` | Counts in each cluster, group and outcome before and after training augmentation. |
| `runs.csv` | Real and synthetic training sizes, test sizes, moved singletons and fuzzy partition coefficient. |
| `comparison.csv` | Changes in the absolute positive-rate gap, accuracy and consistency for each paired split. |
| `main_decisions.csv` | Main-split counts of favourable outcomes and prediction switches by demographic group. |
| `split_comparison.png` | The nine changes in the absolute group gap shown in the report. |
