# AI Data Analyst Agent

An AI-powered data analysis assistant built with Python,
Groq API, pandas, NumPy, and Matplotlib.

The agent analyzes CSV datasets through natural-language
questions, autonomously selects analytical tools, performs
statistical calculations, generates visualizations, and
provides data-driven interpretations.

## Features

- CSV dataset inspection and missing-value detection
- Descriptive statistics
- Distribution analysis, including skewness
- Pearson and Spearman correlation analysis
- Grouping and aggregation (sum, mean, count, min, max)
- Automatic generation of bar charts, histograms,
  scatter plots, and line charts
- Autonomous tool selection using LLM function calling
- Tool execution logging and error handling
- Automated evaluation against independent pandas calculations
- Cross-dataset testing and performance reporting

## Technology Stack

- Python
- Google Colab
- Groq API
- OpenAI GPT-OSS-20B (open-weight language model hosted by Groq)
- pandas and NumPy
- Matplotlib

## AI Model

The agent uses GPT-OSS-20B, an open-weight large language
model developed by OpenAI and accessed through the Groq API.

The model interprets user questions, selects appropriate
Python tools, determines their arguments, and generates
natural-language explanations based on tool outputs.

All statistical calculations and visualizations are
performed by Python functions rather than the LLM itself.

The model is explicitly selected in the API request
and is not automatically chosen by Groq.

## Architecture

User question
    |
    v
Groq API / GPT-OSS-20B
    |
    v
LLM-based tool selection (function calling)
    |
    v
Python analytical tools
    |
    v
pandas / NumPy / Matplotlib
    |
    v
Tool results returned to the LLM
    |
    v
Natural-language analytical report

## Available Analytical Tools

The agent currently provides nine Python tools:

1. inspect_data
   Inspects dataset structure, column types, and missing values.

2. calculate_statistics
   Calculates descriptive statistics for numerical variables.

3. group_and_aggregate
   Performs grouped calculations using sum, mean,
   count, minimum, and maximum.

4. create_bar_chart
   Visualizes aggregated data across categories.

5. create_histogram
   Visualizes numerical distributions.

6. create_scatter_plot
   Visualizes relationships between numerical variables.

7. create_line_chart
   Visualizes time-series data.

8. analyze_distribution
   Calculates distribution statistics, including skewness.

9. calculate_correlation
   Calculates Pearson or Spearman correlation coefficients.

The LLM selects tools according to the user's request,
while calculations and plotting are executed in Python.

## Datasets

Two independent synthetic datasets were generated and
used to evaluate the agent.

### 1. Synthetic Sales Dataset

Contains 200 simulated sales records with five variables:

- product_category
- region
- quantity
- unit_price
- revenue

Revenue is calculated as quantity multiplied by unit price.

Three missing values were intentionally introduced
into the region column.

The dataset is used to evaluate:

- Revenue aggregation
- Categorical comparisons
- Price distributions
- Correlation analysis
- Data quality inspection
- Automated visualization

### 2. Synthetic Customer Support Operations Dataset

Contains 300 simulated customer support tickets
with eight variables:

- ticket_date
- issue_type
- priority
- team
- resolution_hours
- satisfaction_score
- reopened
- tickets

Missing values were intentionally introduced:

- 4 missing values in resolution_hours
- 3 missing values in satisfaction_score

The dataset is used to evaluate:

- Operational performance analysis
- Resolution time comparisons
- Distribution analysis
- Correlation analysis
- Time-series visualization
- Missing-value detection

Both datasets are fully synthetic and contain
no confidential or personally identifiable information.

## Automated Agent Evaluation

The agent was evaluated using eight test scenarios
across two independent synthetic datasets.

Each dataset was tested using four scenarios,
including analytical calculations, tool selection,
visualization tasks, and invalid-column handling.

### Evaluation Results

| Metric | Result |
|--------|--------|
| Datasets evaluated | 2 |
| Total test scenarios | 8 |
| Tool selection checks passed | 8/8 (100%) |
| Numerical correctness checks passed | 5/5 (100%) |
| Tool execution errors | 0 |

### Evaluation Methodology

Tool selection was evaluated by checking whether
the agent invoked the expected analytical tools.

Numerical correctness was evaluated by comparing
selected tool outputs against independent pandas calculations.

The evaluation accounts for tools that internally
perform additional analytical operations.

For example, create_bar_chart performs aggregation
internally, so a separate group_and_aggregate call
is not required.

Invalid-column scenarios were included to examine
the agent's response to unavailable variables.

The agent's tool execution history was recorded
to support debugging and performance assessment.

### Interpretation of Results

All eight expected tool-selection checks passed,
and all five implemented numerical checks passed
during the reported evaluation run.

These results represent preliminary smoke tests
on two synthetic datasets.

They do not establish general agent accuracy,
reliability, or the correctness of every generated
natural-language interpretation.

The evaluation does not automatically validate
all numerical statements, statistical conclusions,
or visualization interpretations in the final reports.

## Error Handling Improvements

During development, the LLM occasionally generated
unexpected arguments for parameter-free functions,
such as inspect_data().

This initially caused tool execution errors.

The agent implementation was updated to:

- Validate tool arguments before execution
- Ignore unnecessary arguments for parameter-free tools
- Handle unsupported or malformed tool calls
- Record tool execution results and errors
- Allow recovery from certain tool-calling failures

After these improvements, the reported cross-dataset
evaluation completed with zero tool execution errors.

## Known Limitations

- LLM-generated interpretations may contain unsupported claims.
- Tool selection can vary across repeated requests.
- The automated evaluation suite is relatively small.
- Numerical validation covers only selected outputs.
- Chart interpretations are not automatically verified.
- Some malformed tool arguments require fallback handling.
- Time-series charts aggregate observations by date.
- Dates without observations are not automatically filled.
- The agent does not perform comprehensive data cleaning.
- The current implementation supports CSV-based analysis.
- The system is designed for exploratory analysis rather
  than high-stakes automated decision-making.

## Running the Project

1. Open AI_Data_Analyst_Agent_Clean.ipynb in Google Colab.
2. Create a Groq API account.
3. Generate a Groq API key.
4. Store the key in Colab Secrets as GROQ_API_KEY.
5. Enable notebook access to the secret.
6. Install the required Python dependencies.
7. Run the notebook cells in order.
8. Select a dataset or upload a CSV file.
9. Ask analytical questions in natural language.

### Dataset Selection

Use the DATASET variable to select a dataset.

For the synthetic sales dataset:

    DATASET = "sales"

For the customer support dataset:

    DATASET = "support"

For a custom CSV file:

    DATASET = "upload"

### Running Automated Evaluation

Set:

    RUN_API_EVALUATION = True

The evaluation automatically processes both
synthetic datasets and generates:

- evaluation_results.csv

Evaluation requires Groq API requests and is subject
to the provider's usage limits and applicable pricing.

## Security

The Groq API key is stored securely using Google Colab Secrets.

The API key is never hardcoded into the project.

Do not upload API credentials, private datasets,
or confidential information to public repositories.

## Future Improvements

- Expanded automated evaluation across diverse datasets
- More comprehensive numerical and statistical validation
- Improved detection of unsupported LLM-generated claims
- More robust tool argument validation
- Advanced time-series aggregation and missing-date handling
- Additional visualization and analytical tools
- Support for multiple connected datasets
- Interactive web interface using Streamlit

## Project Purpose

This project demonstrates practical experience in:

- LLM integration through an external API
- AI agent development
- Function calling and tool orchestration
- Python-based data analytics
- Statistical analysis and data visualization
- Error handling and debugging
- Automated agent evaluation
- Reproducible analytical workflows
