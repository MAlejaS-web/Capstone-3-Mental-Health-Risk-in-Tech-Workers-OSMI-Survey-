## Cross-validated AUC (higher = better)

| model   |   cv_auc |
|:--------|---------:|
| RF      | 0.734776 |
| MLP     | 0.730405 |
| LogReg  | 0.726762 |
| GBC     | 0.725994 |


## Best model — test metrics

| best_model   |   test_auc |   test_f1 |   test_precision |   test_recall |   test_accuracy |
|:-------------|-----------:|----------:|-----------------:|--------------:|----------------:|
| RF           |   0.775133 |  0.666667 |         0.646552 |      0.688073 |        0.702381 |