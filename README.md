Variant Effect Predictor Web Application

A comprehensive platform for predicting the pathogenicity of single-nucleotide variants (SNVs) in human genes using the Evo2 large language model, and for comparing these AI-driven predictions with established ClinVar annotations.

---

## Introduction

This application empowers researchers and clinicians to evaluate the potential disease impact of genetic variants. By combining high-performance inference using H100 GPUs with an intuitive web interface, users can query any SNV in selected genes and receive a detailed classification, confidence score, and comparison with ClinVar data.

---

## Features

1. **Evo2-based Variant Classification**

   * Predicts whether an SNV is *pathogenic* or *benign*.
   * Provides a confidence score for each prediction.

2. **ClinVar Annotation Comparison**

   * Retrieves existing ClinVar classifications for the same variant.
   * Displays side-by-side comparison to highlight concordance or discrepancies.

3. **Genome Assembly and Gene Selection**

   * Supports multiple human genome assemblies (e.g., hg19, hg38).
   * Allows browsing by chromosome or direct gene search (e.g., BRCA1, CFTR).

4. **Reference Sequence Retrieval**

   * Obtains full gene sequences via the UCSC Genome Browser API.
   * Enables users to visualize the exact nucleotide context of each variant.

5. **Modern Web Interface**

   * Built with Next.js, React, and TypeScript.
   * Styled using Tailwind CSS and Shadcn UI components for responsiveness and accessibility.

6. **High‑Performance Backend**

   * Python FastAPI application deployed serverlessly on Modal.
   * Utilizes H100 GPUs for ultra‑fast inference with the Evo2 model.

---

## System Architecture

```text
[Frontend] Next.js + React + Shadcn UI  <-->  [FastAPI Backend]  <-->  [Modal Serverless GPU (H100)]
                                     \
                                      └─ UCSC API (Reference Sequences)
                                      └─ NCBI ClinVar API (Variant Annotations)
```

1. **Frontend** serves the user interface and communicates with the backend over REST.
2. **Backend** handles requests for variant prediction, calls the Evo2 model, and fetches external data.
3. **Modal GPU Environment** executes the Evo2 model in a serverless H100 instance for scalable performance.

---

## Installation and Deployment

### Prerequisites

* Python 3.10 or higher
* Node.js 16 or higher
* Modal CLI (for serverless GPU deployment)

### Repository Setup

```bash
git clone https://github.com/your-org/variant-effect-predictor.git --recurse-submodules
cd variant-effect-predictor
```

### Backend Configuration

```bash
cd backend
python -m venv venv
source venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
modal setup            # Initialize Modal project configuration
modal run main.py      # Run and test locally on CPU/GPU
modal deploy main.py   # Deploy FastAPI service to Modal serverless GPU
```

### Frontend Configuration

```bash
cd ../frontend
npm install
npm run dev            # Start development server at http://localhost:3000
```

---

## Usage

1. Open the web application in your browser.
2. Select a genome assembly (e.g., hg38).
3. Browse chromosomes or search for a specific gene.
4. View the reference nucleotide sequence for the selected gene region.
5. Enter an SNV (e.g., chr17:43044295 A>T) or choose from known variants.
6. Submit the query to receive:

   * Evo2 prediction (pathogenic/benign) and confidence score.
   * Corresponding ClinVar classification and supporting metadata.

---

## References

* **Evo2 Model Publication**: \[[Link to peer-reviewed paper](https://github.com/ArcInstitute/evo2)]
* **ClinVar API Documentation**: [https://www.ncbi.nlm.nih.gov/clinvar/](https://www.ncbi.nlm.nih.gov/clinvar/)
* **UCSC Genome Browser API**: [https://genome.ucsc.edu/](https://genome.ucsc.edu/)

---


