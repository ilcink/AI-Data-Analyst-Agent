# AI Data Analyst Agent

A Python-based AI agent for exploratory analysis of CSV datasets. Users can ask questions in natural language, and the agent selects Python tools to inspect the data, calculate statistics, and generate visualizations.

The project uses OpenAI's GPT-OSS-20B model through the Groq API. The language model handles tool selection and explanations, while pandas, NumPy, and Matplotlib perform the actual calculations and plotting.

## Features

- Dataset inspection, including column types and missing values
- Descriptive statistics and distribution analysis
- Pearson and Spearman correlations
- Grouped aggregations (sum, mean, count, min, max)
- Bar charts, histograms, scatter plots, and daily time-series charts
- LLM function calling with argument validation and execution logging
- Automated tool-selection and numerical checks across two datasets

## Tech Stack

- Python
- Google Colab
- Groq API with `openai/gpt-oss-20b`
- pandas and NumPy
- Matplotlib

## How It Works

The agent exposes nine Python functions to the language model:

| Tool | Purpose |
|------|---------|
| `inspect_data` | Dataset structure and missing values |
| `calculate_statistics` | Descriptive statistics |
| `group_and_aggregate` | Grouped calculations |
| `analyze_distribution` | Distribution statistics and skewness |
| `calculate_correlation` | Pearson and Spearman correlations |
| `create_bar_chart` | Category comparisons |
| `create_histogram` | Numerical distributions |
| `create_scatter_plot` | Relationships between variables |
| `create_line_chart` | Daily time-series visualization |

For each question, the model can request one or more tool calls. The agent validates the arguments, executes the corresponding Python functions, and returns the results to the model for interpretation.

Charts and statistical calculations are produced by Python, not generated directly by the language model.

## Datasets

The notebook generates two reproducible synthetic CSV datasets.

**Sales data** (`sales_data.csv`)

200 records with product category, region, quantity, unit price, and revenue. Three missing region values are included to test data inspection and missing-value handling.

**Customer support data** (`customer_support_operations.csv`)

300 records covering ticket dates, issue types, priorities, teams, resolution times, satisfaction scores, and reopened tickets. The dataset includes four missing resolution times and three missing satisfaction scores.

Both datasets are synthetic and contain no personal or confidential information.

## Evaluation

The notebook includes eight agent test scenarios, four per dataset. These cover tool selection, distribution analysis, correlation, visualization, and invalid-column handling.

Results from the recorded evaluation run:

| Metric | Result |
|--------|--------|
| Test scenarios | 8 |
| Expected tool-selection checks | 8/8 passed |
| Numerical checks | 6/6 passed |
| Tool execution errors | 0 |

Numerical outputs are compared with independently calculated pandas results. Tool-selection checks verify that the required tools were called; they do not evaluate the full quality of the final response.

The numerical checks cover distributions, correlations, revenue aggregation, and daily ticket totals. Invalid-column scenarios are included in the tool-selection tests but do not contribute to the numerical score.

These results are from a small evaluation suite using synthetic data. They should not be interpreted as a general accuracy benchmark.

The notebook can save detailed test results to `evaluation_results.csv`.

## Running the Notebook

1. Open `AI_Data_Analyst_Agent.ipynb` in Google Colab.
2. Create a Groq API key at [Groq Console](https://console.groq.com/).
3. Add the key to Colab Secrets under `GROQ_API_KEY` and enable notebook access.
4. Run the notebook cells in order. Required Python packages are installed in the setup section.
5. Choose a dataset using the `DATASET` variable.

Available options:

```python
DATASET = "sales"
DATASET = "support"
DATASET = "upload"
```

The `upload` option prompts for a custom CSV file.

Run the demonstration cell to submit a question to the agent. Change `demo_question` to try a different analysis.

To run the automated cross-dataset evaluation, set:

```python
RUN_API_EVALUATION = True
```

This runs the eight test scenarios on both synthetic datasets and writes `evaluation_results.csv`.

Groq API requests are subject to rate limits and the provider's pricing rules.

## Limitations

- Tool selection and natural-language interpretations may vary between runs.
- The final written analysis is not automatically fact-checked.
- Numerical validation covers selected outputs, not every possible calculation.
- Time-series charts use daily sums. Missing dates are filled with zero only for the `tickets` column.
- The agent does not provide a general-purpose data-cleaning pipeline.
- Uploaded data is processed locally in Colab, but tool results and dataset metadata can be sent to the Groq API.
- The system is intended for exploratory analysis rather than automated high-stakes decisions.

## Possible Extensions

- Larger evaluation datasets and additional test scenarios
- Automated checks of generated interpretations
- More flexible time-series analysis
- Support for multiple datasets and file formats
- Interactive interface
