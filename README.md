# 🩺 Physician Notetaker: Medical NLP Pipeline

## 📖 Overview
This project is an AI-driven NLP pipeline designed to process physician-patient dialogues. It automates the extraction of clinical information, analyzes patient sentiment and intent, and synthesizes structured SOAP (Subjective, Objective, Assessment, Plan) notes.

This solution is implemented in Python using the Hugging Face `transformers` ecosystem, leveraging State-of-the-Art (SOTA) models fine-tuned for biomedical contexts.

## 🚀 Features & Deliverables

### 1. Medical Named Entity Recognition (NER)
* **Objective:** Extract structured clinical entities (Symptoms, Diagnosis, Treatments).
* **Model:** `d4data/biomedical-ner-all` (RoBERTa-based).
* **Output:** Structured JSON mapping of clinical entities.

### 2. Sentiment & Intent Analysis
* **Objective:** Detect patient anxiety levels and classify communicative intent.
* **Approach:**
    * **Sentiment:** `distilbert-base-uncased-finetuned-sst-2-english`.
    * **Intent:** Zero-Shot Classification using `facebook/bart-large-mnli` to detect dynamic intents (e.g., "Seeking reassurance", "Reporting symptoms") without labeled training data.

### 3. Automated SOAP Note Generation
* **Objective:** Convert raw dialogue into a clinical documentation format.
* **Model:** `facebook/bart-large-cnn` (Summarization).
* **Logic:** Segment-based summarization mapped to standard SOAP categories.

---

## 🛠️ Architecture & Design Decisions

### Why Specialized Models?
Instead of using generic NLP models (like standard BERT), this pipeline prioritizes **Biomedical-Specific Transformers**:
* **Domain Specificity:** Medical terminology ("whiplash," "physiotherapy") requires embeddings trained on PubMed/Clinical notes. Standard models often misclassify these as generic nouns.
* **Zero-Shot Learning:** For Intent Analysis, I utilized Zero-Shot classification to ensure the system is extensible. New intents can be added to the taxonomy without retraining the model.

### Handling Ambiguity
* **Confidence Thresholds:** The pipeline is designed to filter entities with low confidence scores to prevent hallucinations in clinical data.
* **Entity Grouping:** Post-processing logic groups sub-word tokens to ensure human-readable output (e.g., removing tokenizer artifacts like `##`).

---

## 💻 Setup & Installation

### Prerequisites
* Python 3.8+
* pip / conda

### 1. Clone the Repository
```bash
# Unzip the project folder
cd Physician_Notetaker_Submission