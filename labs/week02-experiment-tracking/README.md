# Week 02 Lab

## Reflection

Best run was n_estimators=200, max_depth=None — 0.9722 accuracy, vs 0.8306 on
the baseline (10/3). That's about 14 points better.

I think it won because removing the depth cap let the trees actually grow out
fully and fit the digit patterns properly. Run 2 (100 trees, max_depth=2) barely
beat the baseline at all, which shows it was depth that mattered, not just
throwing more trees at it  a shallow tree stays shallow no matter how many
of them you have.

Of the four legs of reproducibility (code, data, environment, config), today's
MLflow setup covers config — before this, hyperparameters and results only
ever printed to the terminal and disappeared. Now every run's params and
metrics are actually logged and comparable.
