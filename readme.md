# Parametrize

Put all of the parameters of the notebook with their default values in the first cell. In Jupyter, this cell needs to be tagged with `parameters`. See [here](https://papermill.readthedocs.io/en/latest/usage-parameterize.html) for how to do tagging.

The example is the first cell in the `test.ipynb` notebook.

# Run

Run the notebook with `papermill` with default parameters:

```bash
papermill test.ipynb test2.ipynb
```

Note that papermill modifies the notebook `test.ipynb` and the output can (and should) be saved in a different file `test2.ipynb`. However, it can also be the same notebook.

Run the notebook with `papermill` with custom parameters:

```bash
papermill test.ipynb test2.ipynb -p param1 10 -p param2 20
```

Run the notebook with `papermill` with custom parameters from a file:

```bash
papermill test.ipynb test2.ipynb -f params.yaml
```

Useful flags:

`--log-output`: log the outputs of the cells in the command line

Try:

```bash
papermill test.ipynb test2.ipynb --log-output
```

# Take note

When parameters are provided in a file or in the command line, papermill adds them in a cell right below the cell with the default parameters (examine `test2.ipynb` after running `papermill test.ipynb test2.ipynb -f params.yaml`). If the output is the same notebook, the next executions with the parameters will not work (they will be overwritten with the parameters from the previous run). To avoid this, use a different output notebook, which can then be purged, if needed. **The source of truth is the original notebook and it should not be modified.**