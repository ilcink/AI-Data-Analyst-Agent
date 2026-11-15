# AI Data Analyst Agent

A Python-based AI agent for exploring CSV datasets using natural-language questions. GPT-OSS-20B, accessed through the Groq API, selects analytical tools. Python performs the calculations and creates charts.

**Workflow:** CSV → Question → LLM selects tools → Python analyzes data → LLM explains results

## Features

- Nine tools for data inspection, descriptive statistics, grouping, distributions, correlations, and charts.
- Bar charts, histograms, scatter plots, and daily line charts.
- Two reproducible synthetic datasets: sales (200 rows) and customer support (300 rows).
- Custom CSV upload through a Jupyter file-selection button.
- Chart exports to `charts/<dataset>/` as PNG files (existing filenames are overwritten).
- Tool execution trace and independent numerical checks.

## Setup

Requires Python 3.12 (or a compatible Python 3 version), VS Code with the Python and Jupyter extensions, and a Groq API key.

From the project folder, run:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
```

Create a `.env` file in the project folder:

```text
GROQ_API_KEY=your_groq_api_key
```

Do not publish `.env` or an actual API key.

## Run

1. Open `AI_Data_Analyst_Agent.ipynb` in VS Code and select the `.venv` Python kernel.
2. Run the setup and dataset-generation cells.
3. In section 3, select `DATASET = "sales"` or `"support"`, then run the remaining analysis cells in order.
4. For a custom CSV, use **Upload CSV** near the end of the notebook, select a file, then run the following **Analyze Uploaded CSV** cell. The original dataset is restored afterward.

The notebook includes a live demonstration, offline checks, and eight API-based evaluation scenarios. `RUN_API_EVALUATION = True` runs the evaluation and consumes Groq API quota. Results are saved to `evaluation_results.csv`.

The saved charts are organized by dataset under `charts/`. The optional `sample_cafe_sales_80.csv` is a synthetic example for testing custom uploads.

## Recorded Evaluation

In the saved notebook run, **8/8 tool-selection checks** and **6/6 numerical checks** passed, with **0 tool execution errors**. These are small tests, not an estimate of general model accuracy.

## Limitations

The model may choose incorrect tools or misinterpret results. Python calculations are checked in selected scenarios, but final written explanations are not automatically fact-checked. Daily line charts use sums, not forecasts. Dataset metadata and tool results may be sent to Groq; avoid uploading sensitive data without appropriate safeguards.

**Note:** Jupyter upload buttons are interactive in supported notebook environments, not on GitHub's static notebook preview. Saved code outputs and charts can still be viewed on GitHub.
