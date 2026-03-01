# AI Agent Data Analysis – Mobile Sales Dataset

## Project Overview

This project demonstrates a lightweight AI-assisted data analysis workflow built with Python and the OpenAI API. The objective is to efficiently analyze a dataset by generating a structured metadata summary and sending only that summary to the AI model rather than the full dataset.

This approach reduces token usage, improves performance, and minimizes unnecessary data exposure while still producing meaningful analytical insights.

The project simulates the workflow of an AI-powered data analyst reviewing a dataset and providing business recommendations.

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
- Additional transaction attributes  

---

## Technical Workflow

### 1. Environment Setup

Install required dependencies:

```bash
pip install kagglehub[pandas-datasets] openai
