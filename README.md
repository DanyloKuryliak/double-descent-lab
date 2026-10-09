# Double Descent Lab

A controlled synthetic regression experiment showing how test error can rise near interpolation and fall again as a model grows wider.

## Result

Across 50 seeds, median test MSE peaks at **14.19 at width 101**. Median training MSE first reaches numerical zero at **width 105**; test MSE then falls to **0.17 at width 640**. The model has a frozen random ReLU hidden layer and a minimum-norm least-squares output layer. Noise is added only to training targets.

The experiment isolates the phenomenon; it is not evidence that every dataset or end-to-end-trained network will show the same curve. For research context, see [Belkin et al.](https://pmc.ncbi.nlm.nih.gov/articles/PMC6689936/) and [Nakkiran et al.](https://arxiv.org/abs/1912.02292).

| Hidden width | Median train MSE | Median test MSE |
| ---: | ---: | ---: |
| 101 (risk peak) | 0.00010 | 14.19 |
| 105 (interpolation) | ~0 | 5.44 |
| 640 | ~0 | 0.17 |

[Open the executed notebook](double-descent-lab.ipynb) to see the full experiment and plots.

## Run

All experiment code, plots, and findings are in the notebook. From this folder:

```bash
uv venv
uv pip install --python .venv/bin/python -r requirements.txt
uv run --python .venv/bin/python jupyter nbconvert --to notebook --execute --inplace double-descent-lab.ipynb
```

The experiment generates its own data; no dataset download is needed. Result CSVs are saved under `results/`, which is ignored by Git. The curves and summary are also displayed in notebook outputs.
