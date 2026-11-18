# Setup

1. Install [uv](https://docs.astral.sh/uv/getting-started/installation/) and Git.

   On macOS, the easiest option is to use [Homebrew](https://brew.sh/) if you already have it installed.

   ```bash
   brew install uv git
   ```

2. Clone the repository and install the dependencies. `uv` creates `.venv` using Python 3.13 and the versions in `uv.lock`.

   ```bash
   git clone https://github.com/FeargusOG/CDS1-2.git
   cd CDS1-2
   uv sync --locked
   ```

3. Download [UVmap_Sathya_annotated.h5ad](https://drive.google.com/file/d/1-aWa10ct86mHpfFyoaDgX-v3SJIofFSt/view?usp=sharing) (about 8.2 GB) into the repository directory, beside `UVmap.ipynb`.
4. Run the notebook using either option below, from the repository directory.

   **Interactively in JupyterLab**

   ```bash
   uv run jupyter lab
   ```

   Open `UVmap.ipynb`, select the Python kernel from `.venv`, and run the cells from top to bottom. Keep the terminal running while using JupyterLab. Press Ctrl+C in the terminal to stop it.

   **Run all cells from the command line**

   ```bash
   uv run jupyter nbconvert --to notebook --execute --inplace --ExecutePreprocessor.timeout=600 UVmap.ipynb
   ```

   This runs every cell in order and saves outputs back into `UVmap.ipynb`. Execution stops if a cell fails. The timeout allows 10 minutes per cell. Open the notebook in VS Code or JupyterLab to inspect the results.

Figures are saved in `figures/`. Leave `RUN_TSNE = False` for the default workflow.

## Analyse another gene

Run the notebook through the `analyse_gene` function definition. Add a code cell below it, using the gene symbol you want to explore.

```python
cds2_summaries = analyse_gene(adata, 'CDS2')
```

Replace `CDS2` with another gene symbol present in the atlas and choose a corresponding variable name. Run the new cell. When running from the command line, save the notebook with the new cell before executing it.

Each call displays a dot plot and broad/detailed cell-type tables, and saves `dotplot_CDS2.pdf` plus five `CDS2_*.csv` summaries in `figures/`. The summaries cover cell types, stage, study and sample. The function reports an error if the gene is absent from the atlas.

The returned tables are also available in Python, for example `cds2_summaries['detailed']`. To save files elsewhere, pass `output_dir='another_folder'` to `analyse_gene`.
