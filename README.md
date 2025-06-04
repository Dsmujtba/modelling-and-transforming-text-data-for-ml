# Feature Engineering Pipeline for ML with Text Embeddings & Vector Database (AWS & PostgreSQL)

This project demonstrates my ability to engineer a complete data pipeline to process raw text and structured data, generate text embeddings via an external ML model API, and prepare datasets for machine learning applications. I developed a solution to transform the Amazon Reviews dataset, focusing on feature engineering for numerical, categorical, and textual data, and ultimately storing these features—including high-dimensional text embeddings—in a PostgreSQL database configured with the `pgvector` extension.

## Key Achievements & Skills Demonstrated:

* **End-to-End Feature Engineering Pipeline:**
    * Designed and implemented a pipeline to ingest raw JSON data (Amazon reviews and product metadata) from S3.
    * Developed comprehensive Python functions for data cleaning, transformation, and feature creation.
    * Prepared and stored multiple structured datasets suitable for ML model training and vector similarity searches.
* **Advanced Feature Engineering Techniques:**
    * **Text Processing:** Implemented robust text cleaning functions (lowercasing, removing punctuation/special characters, stripping excess whitespace) for review and product information fields.
    * **Numerical Feature Scaling:** Applied `StandardScaler` from `scikit-learn` for standardizing numerical features like price and sales rank. Calculated new ratio-based numerical features (e.g., `helpful_ratio`).
    * **Categorical Feature Encoding:** Utilized `OneHotEncoder` for low-cardinality categorical features (`sales_category`) and **Frequency Encoding** for high-cardinality features (`brand`), demonstrating an understanding of different encoding strategies.
* **Text Embedding Generation & API Integration:**
    * Successfully consumed an external **ML model API** (a sentence transformer model like `all-MiniLM-L6-v2`) to generate 384-dimensional text embeddings for product descriptions and customer reviews.
    * Managed API calls efficiently, processing data in batches to handle potentially large datasets.
* **Vector Database Implementation & Similarity Search:**
    * Configured a **PostgreSQL database on AWS RDS** to function as a vector database by enabling and utilizing the **`pgvector` extension**.
    * Designed table schemas to store text embeddings alongside their source data (product ASINs, reviewer IDs).
    * Implemented functionality to perform **vector similarity searches** (nearest neighbor using L2 distance) directly within PostgreSQL, demonstrating a practical application of embeddings.
* **AWS Cloud & Data Services:**
    * Worked within an AWS environment, utilizing **Amazon S3** for raw data storage and interacting with services like **AWS RDS** for the database.
    * Managed AWS credentials and configurations (e.g., for S3, RDS, and the ML model API endpoint).
* **Python for Data Engineering:**
    * Extensive use of **Pandas** for data manipulation and transformation.
    * Utilized libraries like **`psycopg2`** for PostgreSQL interaction, **`boto3`** for AWS SDK operations, `requests` for API calls, and `scikit-learn` for feature scaling/encoding.

## Project Workflow & Technical Highlights:

1.  **Data Ingestion & Initial Processing:**
    * Loaded sample Amazon Review and Product Metadata JSON files from an S3 bucket into Pandas DataFrames.
    * Performed initial data exploration to understand schema and identify features for processing.
    * Developed Python functions (`process_review`, `process_metadata`) to perform initial cleaning, type conversion (e.g., Unix timestamps to datetime), and extraction of nested data (e.g., helpful votes, sales rank).
    * Merged review and metadata DataFrames based on product ASIN.

2.  **Advanced Feature Engineering:**
    * **Textual Data:** Implemented a custom `clean_text` function (lowercasing, removing punctuation/special characters) and consolidated product information from titles and descriptions.
    * **Numerical Data:** Standardized features like price and sales rank; created new ratio features for review helpfulness.
    * **Categorical Data:** Applied One-Hot Encoding and Frequency Encoding based on feature cardinality.

3.  **Data Structuring for Embeddings:**
    * Strategically split the processed data into three distinct DataFrames: one for review texts, one for product information texts (to avoid redundant embedding generation), and one for the remaining engineered features.

4.  **Embedding Generation & Storage:**
    * For both review texts and product information texts:
        * Iterated through data in manageable **chunks**.
        * Called the external ML model API using the `requests` library to obtain 384-dimensional embeddings for each text chunk.
        * Stored the original text, relevant IDs, and generated embeddings into dedicated PostgreSQL tables (`review_embeddings`, `product_embeddings`) configured with `pgvector`.

5.  **Storage of Other Engineered Features:**
    * Inserted the final set of non-embedding features (numerical, encoded categorical) into a separate PostgreSQL table (`review_product_transformed`).

6.  **Similarity Search Demonstration:**
    * Showcased the utility of stored embeddings by performing k-nearest neighbor searches using the L2 distance operator (`<->`) in `pgvector` to find similar items or reviews based on a query text/embedding.

## Technologies Used:

* **Cloud Platform:** AWS (S3, RDS, EC2 for ML model endpoint - consumed)
* **Database:** PostgreSQL with `pgvector` extension
* **Programming Language:** Python
* **Key Python Libraries:**
    * Data Manipulation: Pandas, NumPy
    * ML/Feature Engineering: scikit-learn (`StandardScaler`, `OneHotEncoder`)
    * Database Interaction: `psycopg2` (with `pgvector.psycopg2`)
    * AWS Interaction: `boto3`
    * API Interaction: `requests`
    * File Handling: `smart_open`, `gzip`, `json`
    * Environment Management: `python-dotenv`
* **Data Formats:** JSON (source), Pandas DataFrame (in-memory)
* **ML Concepts Applied:** Feature Engineering, Text Embeddings, Vector Databases, API Consumption.

---

Future work could involve building a full ML model using these engineered features, or deploying this pipeline using AWS Step Functions and Lambda for automation.
