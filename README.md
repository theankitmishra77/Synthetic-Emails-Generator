# Synthetic-Emails-Generator

# Synthetic Email Generator

## Overview
This project generates synthetic email data from the Enron email dataset while preserving the structure and variability of real-world emails. It ensures de-identification of personally identifiable information (PII) and creates a dataset suitable for fine-tuning large language models (LLMs) like GPT-4.

## Dataset Link
Download the Enron Email Dataset here:
https://www.kaggle.com/datasets/wcukierski/enron-email-dataset

## Features
1. **Email Parsing**: Extracts fields such as `Message-ID`, `From`, `To`, `Subject`, `Date`, and `Body` from raw email messages.
2. **PII De-identification**: Uses `spaCy` for entity recognition and `Faker` for generating synthetic replacements for names, organizations, locations, and other sensitive data.
3. **Synthetic Transformation**: Leverages LangChain with GPT-4 to rewrite email subjects and bodies in a realistic and professional manner.
4. **Similarity Evaluation**: Computes cosine similarity between original and synthetic emails using `SentenceTransformer` to ensure contextual preservation.

## Requirements
- Python 3.8+
- Required Libraries:
  - `pandas`
  - `spacy`
  - `faker`
  - `langchain`
  - `openai`
  - `sentence-transformers`

## Setup

### 1. Clone the Repository
```bash
git clone <repository-link>
cd <repository-folder>
```

### 2. Install Dependencies
Install the required libraries:
```bash
pip install -r requirements.txt
```

### 3. Configure Environment Variables
Create a `.env` file in the root directory (already included) and add your OpenAI API key:
```env
# .env
OPENAI_API_KEY=your_openai_api_key_here
```
Replace `your_openai_api_key_here` with your actual OpenAI API key.

### 4. Download the Dataset
Place the `emails.csv` file containing the Enron email dataset in the project directory. Ensure the dataset contains a column named `message` with raw email content.

## How to Run

### 1. Parse and Transform Emails
Run the script to parse the emails, replace PII, and generate synthetic versions:
```bash
python Synthetic_Email_Generator.py
```

### 2. Output Files
- **`synthetic_emails_with_subject_and_body.csv`**: Contains original, de-identified, and synthetic email subjects and bodies.
- **`synthetic_emails.csv`**: Includes the synthetic emails along with similarity scores.

## Detailed Workflow

### 1. Parsing Emails
- Extracts structured fields (`Message-ID`, `From`, `To`, `Subject`, `Date`, `Body`) using regular expressions.

### 2. PII De-identification
- `spaCy` identifies entities like `PERSON`, `ORG`, `GPE`, `EMAIL`, and `DATE`.
- `Faker` generates realistic replacements for identified entities.

### 3. Synthetic Transformation
- LangChain processes subjects and bodies separately using:
  - **Subject Prompt**: Rewrites the subject line to maintain its intent and professional tone.
  - **Body Prompt**: Transforms the body, adapting context while preserving structure and realism.

### 4. Similarity Evaluation
- Uses `SentenceTransformer` to calculate cosine similarity between embeddings of original and synthetic email bodies.
- Similarity scores ensure contextual integrity.

## Example Output

### Input Email:
```plaintext
Subject: Approval of the DPR Accelerated Put transaction

Dear Andrew,

Attached is the DASH for the approval of the DPR Accelerated Put transaction. This partial divestiture allows us to put $11 million of our equity interest back to DPR Holding Company, LLC...
```

### Synthetic Email:
```plaintext
Subject: Approval for the GPR Strategic Yield initiative

Dear Amit,

Attached is the document for the approval of the GPR Strategic Yield initiative. This strategic adjustment allows us to divest ₹88 crore of our equity interest back to GPR Agro Holdings Private Limited...
```
