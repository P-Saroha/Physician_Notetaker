# Physician Notetaker AI

## 📋 Overview
This project is an NLP-based application designed to assist physicians by automating the documentation process. It processes patient-physician transcripts to extract key medical details, analyze patient sentiment, and generate structured clinical notes (SOAP format).

## ⚙️ Features
1.  **Medical NER (Named Entity Recognition):**
    * Uses the `d4data/biomedical-ner-all` model to identify symptoms and treatments.
    * **Hybrid Approach:** Includes custom Regex (Regular Expression) logic to capture specific details (like patient names and prognosis) that models sometimes miss, ensuring higher accuracy.
2.  **Sentiment & Intent Analysis:**
    * Uses `distilbert` to classify whether a patient is Anxious or Reassured.
    * Uses Zero-Shot Classification (`bart-large-mnli`) to detect specific intents like "Reporting symptoms" or "Seeking reassurance."
3.  **Automated SOAP Note:**
    * Summarizes the conversation using `bart-large-cnn` and maps the output into Subjective, Objective, Assessment, and Plan sections.

## 🛠️ Tech Stack
* **Language:** Python 3
* **Libraries:** Hugging Face `transformers`, `torch`, `re` (Regex)

## 🚀 Setup & Execution

### 1. Install Dependencies
Ensure you have Python installed, then install the required libraries:
```bash
pip install -r requirements.txt

### 2. Run the Application
```bash
python physician_notetaker.py


3. Expected Output
The script will output three JSON blocks to the console:

Extraction Data: JSON containing Patient Name, Diagnosis, Symptoms, etc.

Sentiment Analysis: JSON containing Sentiment Label and Confidence Score.

SOAP Note: JSON containing the structured clinical note.