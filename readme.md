# Parametrize

Put all of the parameters of the notebook with their default values in the first cell. In Jupyter, this cell needs to be tagged with `parameters`. See [here](https://papermill.readthedocs.io/en/latest/usage-parameterize.html) for how to do tagging.

The example is the first cell in the `test.ipynb` notebook.

# Run

Usage: `papermill [OPTIONS] NOTEBOOK_PATH [OUTPUT_PATH]`

Run the notebook with `papermill` with default parameters:

```bash
papermill test.ipynb test_modified.ipynb
```

Note that during the run the notebook will be modified (just like when running a notebook manually). Papermill can (and should, see [below](#take-note)] save the modified notebook in a different file, in the example above it is `test_modified.ipynb`.

Run the notebook with `papermill` with custom parameters:

```bash
papermill test.ipynb test_modified.ipynb -p param1 10 -p param2 20
```

Run the notebook with `papermill` with custom parameters from a file:

```bash
papermill test.ipynb test_modified.ipynb -f params.yaml
```

Useful flags:

`--log-output`: log the outputs of the cells in the command line

Try:

```bash
papermill test.ipynb test_modified.ipynb -f params.yaml --log-output
```

# Take note

When parameters are provided in a YAML file or the command line (with `-p` flag), upon execution `papermill` will add them in a new cell below the cell with the default parameters (examine `test_modified.ipynb` after running `papermill test.ipynb test_modified.ipynb -f params.yaml`). So if the output notebook is the same as the source notebook, this cell will be added to the original notebook. In this case, the next executions with the parameters will not work, because they will be overwritten with the parameters from the previous run. To avoid this, always use an output notebook, never overwrite the original. The output notebook can then be purged, if needed. In other words, **the source of truth is the original notebook and it should not be modified when running with `papermill`.**