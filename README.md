# AI Agent Data Analysis – Mobile Sales Dataset

## Project Overview

This project demonstrates how to build a lightweight AI-assisted data analysis pipeline using Python and the OpenAI API.

Instead of sending the full dataset to the AI model, the system generates a structured metadata summary (schema, statistics, missing values, etc.) and sends only that summary for analysis. This approach:
 
- Reduces token usage  
- Improves performance  
- Minimizes unnecessary data exposure  
- Maintains scalability  

The project simulates an AI-powered data analyst that reviews dataset structure and produces business insights.

---

## Dataset

**Source:** Kaggle  
**Dataset:** Synthetic Mobile Sales 2025  

The dataset contains simulated mobile device sales data, including:

- Product information  
- Sales quantities  
- Revenue  
- Transaction dates  
- Regions  
- Additional transactional attributes  

---

## Project Architecture

The workflow follows this structure:

1. Install dependencies  
2. Download dataset from Kaggle  
3. Load dataset into Pandas  
4. Generate automated metadata summary  
5. Send structured summary to OpenAI  
6. Receive AI-generated business insights  

Only summarized metadata is transmitted to the model.

---

## Step 1: Environment Setup

Install required dependencies:

```bash
pip install kagglehub[pandas-datasets] openai pandas numpy
```

Import required libraries:

```python
import os
import json
import pandas as pd
import numpy as np
import kagglehub
from getpass import getpass
from openai import OpenAI
```

Securely load your OpenAI API key:

```python
os.environ["OPENAI_API_KEY"] = getpass("Enter your OpenAI API key: ")
client = OpenAI()
```

**Important:** Never hard-code API keys into a public repository.

---

## Step 2: Download Dataset from Kaggle

Programmatically download the dataset:

```python
path = kagglehub.dataset_download("syedaeman2212/mobile-sales-data")
```

---

## Step 3: Load Dataset

Load the CSV file into a Pandas DataFrame:

```python
df = pd.read_csv(os.path.join(path, "synthetic_mobile_sales_2025.csv"))
```

Preview the dataset:

```python
df.head()
df.info()
```

---

## Step 4: Generate Structured Data Summary

Instead of sending raw records, build a structured metadata summary:

```python
summary = {
    "shape": df.shape,
    "columns": df.columns.tolist(),
    "dtypes": df.dtypes.astype(str).to_dict(),
    "missing": df.isnull().sum().to_dict(),
    "numeric_summary": df.describe().to_dict()
}
```

Convert summary to JSON for API transmission:

```python
summary_json = json.dumps(summary, indent=2)
```

This ensures:

- Reduced token usage  
- Faster API responses  
- Improved security  
- Scalability  

---

## Step 5: Send Metadata to OpenAI

Construct a prompt that instructs the AI to analyze the dataset summary:

```python
prompt = f"""
You are a senior data analyst. Based on the following dataset metadata, provide:

1. Key insights
2. Observed trends
3. Data quality concerns
4. Potential business recommendations

Dataset Summary:
{summary_json}
"""
```

Send request to the API:

```python
response = client.responses.create(
    model="gpt-4.1-mini",
    input=prompt
)

analysis_output = response.output_text
print(analysis_output)
```

---

## Step 6: AI-Generated Insights

The AI returns:

- Business insights  
- Identified patterns  
- Anomaly detection suggestions  
- Data quality observations  
- Strategic recommendations  

This simulates an AI-powered analytical review.

---

## Design Rationale

Sending only metadata rather than full datasets:

- Reduces API token costs  
- Prevents unnecessary data sharing  
- Improves performance  
- Maintains governance standards  
- Enables production scalability  

This architecture is well-suited for enterprise AI analytics pipelines.

---

## Potential Enhancements

The project can be expanded to include:

- Automated visualizations (Matplotlib, Seaborn, Plotly)
- Correlation matrix analysis
- Outlier detection
- Feature engineering
- Machine learning model training
- Automated report generation (PDF or HTML)
- Interactive dashboard (Streamlit)
- User-uploaded dataset support

---

## Skills Demonstrated

- Data ingestion and preprocessing  
- Automated exploratory data analysis  
- Structured metadata engineering  
- API integration with OpenAI  
- Efficient token management  
- AI-assisted analytics pipeline design  
- Reproducible Python workflows  

---

## Production Considerations

For real-world deployment:

- Add environment variable management  
- Implement error handling  
- Add structured logging  
- Implement API rate limit handling  
- Containerize with Docker  
- Deploy via a cloud platform (AWS, Azure, GCP)  

---

## Use Case

This project demonstrates how to build an AI-assisted analytics system capable of reviewing datasets and generating actionable insights without exposing raw data.

It is suitable for:

- AI-driven reporting systems  
- Internal analytics assistants  
- Enterprise data governance workflows  
- Portfolio demonstration of applied AI integration  
