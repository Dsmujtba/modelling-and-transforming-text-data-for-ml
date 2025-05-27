# Amazon Reviews Feature Engineering & Vector Database Pipeline

## Overview

This project demonstrates a complete pipeline for transforming raw Amazon Reviews and product metadata into structured datasets suitable for machine learning (ML) applications. It includes feature engineering for numerical, categorical, and textual data, generation of text embeddings using a Sentence Transformer model, and storage of the resulting features and vectors in a PostgreSQL vector database for efficient similarity search.

---

## Table of Contents

- [Project Structure](#project-structure)
- [Features](#features)
- [Setup Instructions](#setup-instructions)
- [Usage](#usage)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)
- [References](#references)

---

## Project Structure

```
C4_W2_Assignment.ipynb      # Main Jupyter notebook with all code and documentation
src/
    env                     # Environment variables for DB connection
data/
    reviews_Toys_and_Games_sample.json.gz
    meta_Toys_and_Games_sample.json.gz
```

---

## Features

- **Data Loading:** Efficiently loads and explores large JSON datasets from S3.
- **Feature Engineering:**
  - Cleans and standardizes text, numerical, and categorical features.
  - Handles missing values and outliers.
  - Encodes categorical variables using frequency and one-hot encoding.
- **Text Embeddings:** 
  - Generates 384-dimensional embeddings for review and product texts using a REST API to a Sentence Transformer model.
  - Processes data in batches to optimize memory and API usage.
- **Database Integration:**
  - Stores embeddings and metadata in PostgreSQL with the `pgvector` extension for similarity search.
  - Supports efficient nearest neighbor queries using L2 distance.
- **Reproducibility:** All steps are documented and parameterized for easy reruns and adaptation.

---

## Setup Instructions

1. **Clone the Repository**
    ```bash
    git clone <your-repo-url>
    cd <repo-folder>
    ```

2. **Set Up Python Environment**
    ```bash
    python3 -m venv venv
    source venv/bin/activate  # On Windows: venv\Scripts\activate
    pip install -r requirements.txt
    ```

3. **Configure Environment Variables**
    - Edit `src/env` and set your PostgreSQL credentials and endpoint.

4. **Download Data**
    - Ensure you have access to the required S3 buckets or place the sample data in the `data/` directory.

5. **Run the Notebook**
    - Open `C4_W2_Assignment.ipynb` in VS Code or JupyterLab.
    - Execute cells sequentially, following the instructions and markdown explanations.

---

## Usage

- **Data Exploration:** Inspect the raw review and metadata samples.
- **Feature Engineering:** Run the provided functions to clean and transform the data.
- **Embedding Generation:** Use the provided API endpoint to generate embeddings for text fields.
- **Database Storage:** Store processed features and embeddings in PostgreSQL for downstream ML or analytics.
- **Similarity Search:** Query the vector database for nearest neighbors using L2 distance.

---

## Best Practices

- **Modular Code:** Use functions for each transformation step for clarity and reusability.
- **Batch Processing:** Always process large datasets and API calls in manageable batches.
- **Error Handling:** Wrap API/database operations in try/except blocks and log errors.
- **Environment Management:** Store credentials in environment files, never in code.
- **Documentation:** Use markdown cells and inline comments to explain logic and assumptions.
- **Testing:** Validate outputs at each step (e.g., check embedding dimensions, DB row counts).
- **Resource Cleanup:** Always close database connections and cursors after use.
- **Reproducibility:** Set random seeds where applicable and document all parameters.

---

## Troubleshooting

- **API Connection Errors:** Ensure the embedding API endpoint is running and accessible. Reboot the EC2 instance if needed.
- **Database Issues:** Confirm the `vector` extension is enabled in PostgreSQL and credentials are correct.
- **Memory Issues:** Reduce batch sizes for embedding generation or database inserts.
- **Missing Data:** Check for missing or malformed records after each transformation step.

---

## References

- [Sentence Transformers Documentation](https://www.sbert.net/)
- [pgvector: Open-source vector similarity search for Postgres](https://github.com/pgvector/pgvector)
- [scikit-learn: Preprocessing](https://scikit-learn.org/stable/modules/preprocessing.html)
- [Pandas Documentation](https://pandas.pydata.org/)

---

## License

This project is for educational purposes. See [LICENSE](LICENSE) if provided.

---

*For questions or contributions, please open an issue or pull request.*
