# Setup

1. Install [uv](https://docs.astral.sh/uv/getting-started/installation/) and Git.
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
